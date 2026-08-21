# Cheat Sheet — Arquitetura Hexagonal (Ports & Adapters)

Ideia central em uma frase: **a lógica de negócio fica no meio, sem saber nada de
framework, banco ou HTTP; tudo que é tecnologia concreta é plugado por fora através
de interfaces que o próprio domínio define.**

Na entrevista, esta é a resposta pra "como isso viraria um serviço de verdade?".

---

## O diagrama

```
   DRIVING side (primary)                              DRIVEN side (secondary)
   quem CHAMA o domínio                                o que o domínio CHAMA

   REST controller ─┐                              ┌─► JPA / Mongo repository
   CLI / cron      ─┼─► [primary port] ─► DOMÍNIO ─► [secondary port] ─┼─► HTTP client (upstream)
   fila / consumer ─┘    (interface IN)   (core)     (interface OUT)   └─► publisher de eventos
   teste           ─┘

   └── inbound adapters ──┘                         └── outbound adapters ──┘
```

Fluxo: adapter inbound traduz o mundo externo → chama um **primary port** →
domínio executa a regra → quando precisa de algo externo, chama um **secondary
port** → um adapter outbound implementa esse port com a tecnologia real.

---

## Vocabulário (não confunda os pares)

- **Domínio / core**: entidades, value objects, regras. ZERO import de framework.
- **Port**: uma interface. Quem a define é o domínio.
  - **Primary / driving port** (IN): a API do domínio — o que o mundo pode pedir a ele (um use case).
  - **Secondary / driven port** (OUT): o que o domínio precisa do mundo — ex.: buscar dados, persistir, publicar.
- **Adapter**: implementação concreta na borda.
  - **Inbound / primary adapter**: traduz entrada externa (HTTP, CLI, mensagem) em chamada ao primary port.
  - **Outbound / secondary adapter**: implementa o secondary port com JPA, cliente HTTP, Kafka, etc.

Mnemônico: **port = interface, adapter = implementação**. Primary = quem me chama;
secondary = quem eu chamo.

---

## A regra de dependência (o coração de tudo)

**Todas as setas apontam pra dentro.** O domínio não conhece nenhum adapter. Os
adapters conhecem o domínio (dependem dos ports). Isso se sustenta via Dependency
Inversion: o domínio declara a interface `OrderDataProvider`; o adapter HTTP a
implementa. O domínio nunca importa a classe HTTP — recebe ela injetada como o tipo
da interface.

Resultado prático: você troca REST por gRPC, Postgres por Mongo, o upstream real por
um fake — **sem tocar em uma linha de regra de negócio**.

---

## Mapeando no problema de payout da DoorDash

| Papel                  | No payout service                                          |
|------------------------|-----------------------------------------------------------|
| Domínio / core         | `PayEngine` + `PayRule`s + value objects (`Money`, `DasherDay`) |
| Primary port (IN)      | `CalculatePayout` (use case)                              |
| Inbound adapter        | `PayoutController` (recebe HTTP, chama o use case)        |
| Secondary port (OUT)   | `OrderDataProvider` (o que o domínio precisa do upstream) |
| Outbound adapter       | `HttpOrderDataProvider` (chama o serviço upstream real)   |
| Adapter de teste       | fake in-memory implementando `OrderDataProvider`          |

---

## Estrutura de pacotes (referência)

```
com.doordash.payout
├── domain                      // puro: sem Spring, sem JPA, sem HTTP
│   ├── PayEngine.java
│   ├── PayRule.java
│   ├── Money.java
│   └── DasherDay.java
├── application
│   ├── PayoutService.java      // implementa o primary port, usa o secondary port
│   └── port
│       ├── in
│       │   └── CalculatePayout.java     // primary port
│       └── out
│           └── OrderDataProvider.java   // secondary port
└── adapter
    ├── in
    │   └── web
    │       └── PayoutController.java    // inbound adapter
    └── out
        └── http
            └── HttpOrderDataProvider.java // outbound adapter
```

---

## Código — o esqueleto que prova o conceito

```java
// application/port/in — PRIMARY PORT: o que o mundo pode pedir ao domínio
public interface CalculatePayout {
    Money forDasher(String dasherId, LocalDate day);
}

// application/port/out — SECONDARY PORT: o que o domínio precisa do mundo externo
public interface OrderDataProvider {
    List<OrderActivity> activitiesFor(String dasherId, LocalDate day);
}

// application — use case: implementa o primary port, DEPENDE do secondary port (não da impl)
public class PayoutService implements CalculatePayout {
    private final OrderDataProvider orders;   // injetado; não sabe que é HTTP
    private final PayEngine engine;

    public PayoutService(OrderDataProvider orders, PayEngine engine) {
        this.orders = orders;
        this.engine = engine;
    }

    public Money forDasher(String id, LocalDate day) {
        var activities = orders.activitiesFor(id, day);
        return engine.calculate(new DasherDay(activities));
    }
}

// adapter/out/http — OUTBOUND ADAPTER: implementa o secondary port com tecnologia real
public class HttpOrderDataProvider implements OrderDataProvider {
    private final HttpClient client;
    public List<OrderActivity> activitiesFor(String id, LocalDate day) {
        var raw = client.get("/orders?dasher=" + id + "&day=" + day);
        return map(raw);   // traduz o DTO externo pro modelo de domínio, na borda
    }
}

// adapter/in/web — INBOUND ADAPTER: traduz HTTP em chamada ao primary port
public class PayoutController {
    private final CalculatePayout calculate;
    public PayoutController(CalculatePayout calculate) { this.calculate = calculate; }
    public HttpResponse handle(HttpRequest req) {
        var pay = calculate.forDasher(req.param("dasher"), req.date("day"));
        return HttpResponse.ok(pay.toJson());
    }
}
```

E o pagamento da arquitetura — testar o domínio sem rede nenhuma:

```java
@Test
void calculaPayoutSemInfra() {
    OrderDataProvider fake = (id, day) -> List.of(new OrderActivity(/* ... */));
    var service = new PayoutService(fake, new PayEngine(rules));
    assertEquals(Money.of(15.00), service.forDasher("d1", LocalDate.now()));
}
```

---

## Vantagens (por que vale o custo)

- **Testabilidade**: o core roda em teste unitário, sem banco, sem HTTP, sem Spring.
- **Trocar infra sem tocar no core**: REST→gRPC, Postgres→Mongo, upstream real→mock.
- **Adiar decisões**: começa com adapter in-memory, pluga o banco depois.
- **Fronteiras explícitas**: onde termina o negócio e começa a tecnologia fica óbvio.

---

## Armadilhas (o que separa quem entende de quem só desenhou o hexágono)

- **Domínio anêmico**: se toda regra vaza pros "services" e as entidades viram sacos
  de getter/setter, você tem hexágono por fora e transaction script por dentro. O
  domínio precisa ter comportamento.
- **Framework vazando pro core**: anotação `@Entity`/`@Autowired` na classe de
  domínio já quebrou a ideia. O core não importa Spring nem JPA.
- **Over-engineering**: CRUD trivial não precisa de hexágono completo. A abstração
  tem que pagar o próprio custo — julgue o problema.
- **Mapeamento excessivo**: três modelos (DTO web, domínio, entidade de persistência)
  às vezes é demais. Adicione tradução quando os modelos divergem de fato, não por dogma.
- **DTO externo entrando no domínio**: traduza na borda. O formato do upstream não
  pode contaminar o core.

---

## Hexagonal vs Clean vs Onion (se perguntarem)

São primos — mesma tese central: dependências apontam pra dentro, domínio isolado.
- **Hexagonal (Ports & Adapters)**: enfatiza a simetria driving/driven e as interfaces nas bordas.
- **Clean Architecture**: camadas nomeadas (entities → use cases → interface adapters
  → frameworks) + a Dependency Rule explícita.
- **Onion**: camadas concêntricas com o domínio no centro.
Diferença é de ênfase e vocabulário, não de princípio. Diga isso e não perca tempo.

---

## Explicação de 30 segundos (decore o formato, não as palavras)

"Coloco a regra de negócio num core sem dependência de framework. O que o mundo
externo chama passa por uma interface — o primary port. O que o meu domínio precisa
do mundo externo é outra interface que ele mesmo declara — o secondary port. As
tecnologias concretas (REST, banco, o serviço upstream) são adapters plugados nessas
interfaces. Ganho testar o domínio sem infra e trocar tecnologia sem tocar na regra."

---

## Versão MÍNIMA pra 45 min de Code Craft

Você não vai montar pacote-por-pacote numa prova curta. O hexágono em miniatura que
cabe no tempo e já responde "como vira produção":

1. Mantenha a `PayEngine` **sem I/O** — só recebe dados e devolve o valor.
2. Esconda a chamada upstream atrás de **uma interface** (`OrderDataProvider`).
3. Na prova, implemente essa interface com um **fake in-memory**; mencione que em
   produção seria um adapter HTTP.
4. Teste a engine passando o fake.

Isso é Ports & Adapters em escala de bolso — e demonstra exatamente a maturidade que
o avaliador procura, sem gastar os 45 minutos em estrutura de diretório.