# Cheat Sheet — Design Patterns (foco entrevista LLD / Code Craft)

Regra de ouro da entrevista: **resolva o problema primeiro, nomeie o padrão depois**
— e só se ele realmente encaixar. Padrão forçado é over-engineering e derruba nota.
Interviewer quer ver julgamento: por que esse, qual o custo, quando você NÃO usaria.

---

## Tabela de reconhecimento (o que você mais vai usar na hora)

| Sintoma no problema                                          | Padrão                    |
|--------------------------------------------------------------|---------------------------|
| `if/else` ou `switch` sobre comportamentos intercambiáveis   | **Strategy**              |
| Criar objetos com lógica condicional / esconder o `new`      | **Factory**               |
| Objeto com muitos campos opcionais / construção passo a passo| **Builder**               |
| Integrar uma API/lib com interface incompatível              | **Adapter**               |
| Adicionar comportamento empilhável em runtime                | **Decorator**             |
| Comportamento depende do estado + transições bagunçadas      | **State**                 |
| Vários componentes reagem a um evento                        | **Observer**              |
| Pipeline de handlers; cada um trata ou passa adiante         | **Chain of Responsibility**|
| Ação com undo/redo, enfileirar/agendar operações             | **Command**               |
| Algoritmo com esqueleto fixo e passos que variam             | **Template Method**       |
| Tratar item único e grupo de forma uniforme (árvore)         | **Composite**             |
| Uma instância global (CUIDADO — ver abaixo)                  | **Singleton**             |

---

# CREATIONAL

## Factory
Encapsula a decisão de QUAL objeto criar, tirando o `new` condicional do cliente.

```java
class RuleSetFactory {
    static List<PayRule> forMarket(String market) {
        return switch (market) {
            case "peak" -> List.of(new BasePayRule(), new PeakZoneBonus(), new MinimumGuarantee(10));
            case "base" -> List.of(new BasePayRule());
            default     -> throw new IllegalArgumentException("mercado: " + market);
        };
    }
}
```
Gatilho: "monte o conjunto de regras conforme o mercado/tier do Dasher."
Cuidado: se não há variação real de criação, é abstração vazia. Não crie factory pra `new` simples.

## Builder
Construção legível e imutável sem construtor telescópico (5 params na ordem certa = bug).

```java
class Order {
    private final String id; private final double tip; private final String note;
    private Order(Builder b) { id = b.id; tip = b.tip; note = b.note; }
    static class Builder {
        private String id; private double tip; private String note = "";
        Builder id(String v)   { this.id = v;   return this; }
        Builder tip(double v)  { this.tip = v;  return this; }
        Builder note(String v) { this.note = v; return this; }
        Order build()          { return new Order(this); }
    }
}
Order o = new Order.Builder().id("A1").tip(3.0).build();
```
Cuidado: `record` já cobre muito caso de "objeto imutável simples". Builder ganha valor com muitos opcionais/validação.

## Singleton (na entrevista, trate como quase-anti-pattern)
Uma instância única e ponto de acesso global.

```java
enum Config { INSTANCE;                 // enum = melhor singleton em Java (thread-safe, serializable)
    final double peakBonus = 2.0;
}
Config.INSTANCE.peakBonus;
```
Cuidado: estado global escondido mata testabilidade e injeta acoplamento. Em quase todo caso de entrevista, **injeção de dependência** é a resposta melhor. Se citar Singleton, cite o custo junto.

---

# STRUCTURAL

## Adapter
Traduz uma interface incompatível na interface que teu domínio espera. Direto pro "chamar o serviço upstream".

```java
interface OrderSource { List<Order> fetch(LocalDate day); }   // o que o domínio quer

class LegacyClientAdapter implements OrderSource {
    private final LegacyApi legacy;                            // interface incompatível
    LegacyClientAdapter(LegacyApi legacy) { this.legacy = legacy; }
    public List<Order> fetch(LocalDate day) {
        return legacy.getRawOrders(day.toString()).stream()   // traduz o formato externo
                     .map(this::toDomain).toList();
    }
}
```
É a cola entre o mundo externo e o domínio. Peça-chave da arquitetura hexagonal.

## Decorator
Embrulha um objeto pra adicionar comportamento sem alterar o original. Empilhável.

```java
interface PayRule { double apply(DasherDay d, double total); }

class SurgeMultiplier implements PayRule {      // envolve outra PayRule
    private final PayRule inner; private final double mult;
    SurgeMultiplier(PayRule inner, double mult) { this.inner = inner; this.mult = mult; }
    public double apply(DasherDay d, double t) { return inner.apply(d, t) * mult; }
}
// uso: new SurgeMultiplier(new BasePayRule(), 1.25)
```
Cuidado: muitas camadas viram difícil de debugar. Bom pra comportamento opcional composável.

## Composite
Trata item individual e grupo pela mesma interface. Estruturas em árvore.

```java
interface LineItem { double total(); }
class Product implements LineItem { public double total() { return price; } }
class Bundle implements LineItem {
    private final List<LineItem> items;
    public double total() { return items.stream().mapToDouble(LineItem::total).sum(); }
}
```
Gatilho: "um pedido pode conter combos que contêm itens." Recursão uniforme.

## (Menções rápidas)
- **Facade**: uma interface simples na frente de um subsistema complexo.
- **Proxy**: substituto que controla acesso (lazy load, cache, permissão) mantendo a mesma interface.

---

# BEHAVIORAL

## Strategy — a estrela do Code Craft
Comportamentos intercambiáveis atrás de uma interface comum. Mata o `if/else` gigante.

```java
interface PayRule { double apply(DasherDay d, double total); }

class BasePayRule    implements PayRule { public double apply(DasherDay d, double t){ return t + d.base(); } }
class PeakZoneBonus  implements PayRule { public double apply(DasherDay d, double t){ return t + d.peakOrders()*2.0; } }

class PayEngine {
    private final List<PayRule> rules;               // estratégias compostas
    PayEngine(List<PayRule> rules){ this.rules = rules; }
    double calculate(DasherDay d){
        double t = 0; for (PayRule r : rules) t = r.apply(d, t); return t;
    }
}
```
Este É o padrão que responde à mudança de regra de última hora (Open/Closed).

## Chain of Responsibility
Handlers em sequência; cada um trata e/ou passa adiante. Bom pra pipeline de validação.

```java
abstract class Validator {
    private Validator next;
    Validator linkTo(Validator n){ this.next = n; return n; }
    final void validate(Order o){
        check(o);
        if (next != null) next.validate(o);
    }
    abstract void check(Order o);
}
// new NotNull().linkTo(new PositiveTip()).linkTo(new KnownZone());
```
Diferença pra Strategy: aqui a ordem importa e um handler pode interromper a cadeia.

## Observer
Um sujeito notifica múltiplos inscritos quando algo muda. Desacopla evento das reações.

```java
interface OrderListener { void onStatusChange(Order o, Status s); }

class Order {
    private final List<OrderListener> listeners = new ArrayList<>();
    private Status status;
    void subscribe(OrderListener l){ listeners.add(l); }
    void setStatus(Status s){
        this.status = s;
        listeners.forEach(l -> l.onStatusChange(this, s));   // notifica auditoria, push, etc.
    }
}
```
Gatilho: "quando o pedido muda de status, avise notificação + auditoria + ETA."

## State
O comportamento muda conforme o estado; transições ficam explícitas (não flags soltas).

```java
enum OrderState {
    CREATED   { OrderState next(){ return PICKED_UP; } },
    PICKED_UP { OrderState next(){ return DELIVERED; } },
    DELIVERED { OrderState next(){ throw new IllegalStateException("estado terminal"); } };
    abstract OrderState next();
}
```
Gatilho: ciclo de vida do pedido/entrega. Transição inválida lança em vez de virar bool bagunçado.

## Command
Encapsula uma ação como objeto — permite undo/redo, fila, agendamento, log.

```java
interface Command { void execute(); void undo(); }

class AssignDasher implements Command {
    private final Order order; private final Dasher dasher;
    AssignDasher(Order o, Dasher d){ order = o; dasher = d; }
    public void execute(){ order.assign(dasher); }
    public void undo()   { order.unassign(); }
}
```
Gatilho: "preciso desfazer uma atribuição" ou "enfileirar operações de dispatch."

## Template Method
Esqueleto fixo do algoritmo na superclasse; subclasse preenche os passos variáveis.

```java
abstract class PayoutJob {
    final void run() {                    // esqueleto imutável
        var data = fetch();
        var pay  = calculate(data);
        persist(pay);
    }
    abstract Data   fetch();
    abstract double calculate(Data d);
    abstract void   persist(double pay);
}
```
Cuidado: usa herança (acopla). Em muitos casos, Strategy por composição é preferível.

---

## Como usar isto na prova

1. Resolve o problema com o design mais simples que funciona.
2. Se surgir um dos sintomas da tabela, aplique o padrão — e diga o nome DEPOIS.
3. Sempre verbalize o trade-off: "usei Strategy aqui porque as regras variam e o
   requisito pode crescer; o custo é uma interface a mais, que se paga na primeira
   regra nova."
4. Saiba dizer um que você NÃO usaria e por quê. Isso separa sênior de quem decorou.

Os que quase sempre aparecem em problema de logística estilo DoorDash:
**Strategy** (regras), **Factory** (montar regras), **State** (ciclo do pedido),
**Observer** (mudança de status), **Adapter** (upstream). Domine esses cinco.