# Java Live-Coding Cheat Sheet — reaquecimento rápido

Foco: sair do piloto automático do IDE e ter a sintaxe/API na ponta dos dedos.
Isso NÃO é cola pra hora da prova — é pra treinar na quarta até virar reflexo.

---

## 0. O boilerplate que todo mundo esquece

```java
System.out.println("texto");
System.out.printf("%.2f%n", valor);   // %n = newline portável
System.out.printf("Dasher %s ganhou %.2f%n", nome, pay);
```

Classe mínima executável (caso peçam do zero num arquivo só):

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("go");
    }
}
```

---

## 1. Collections — declaração

```java
Map<String, String>  m      = new HashMap<>();
Map<String, Integer> counts = new HashMap<>();
List<String>         list   = new ArrayList<>();
Set<String>          set    = new HashSet<>();
Deque<Integer>       stack  = new ArrayDeque<>();   // push / pop / peek
Deque<Integer>       queue  = new ArrayDeque<>();   // offer / poll / peek
TreeMap<String,Integer> sorted = new TreeMap<>();   // chaves ordenadas
LinkedHashMap<String,Integer> ordered = new LinkedHashMap<>(); // ordem de inserção
```

Inicialização literal (útil pra fixtures de teste):

```java
List<String> xs = List.of("a", "b", "c");          // IMUTÁVEL
Map<String,Integer> mm = Map.of("a", 1, "b", 2);   // IMUTÁVEL
List<String> mutable = new ArrayList<>(List.of("a", "b"));
```

ArrayList vs LinkedList: use `ArrayList` por padrão. `ArrayDeque` pra pilha/fila
(mais rápido que `Stack` e `LinkedList`, e `Stack` é legado — evite).

---

## 2. Métodos de Map que economizam 10 linhas

```java
m.getOrDefault(key, 0)                              // sem NPE
m.putIfAbsent(key, val)
counts.merge(key, 1, Integer::sum)                  // contador clássico
m.computeIfAbsent(key, k -> new ArrayList<>()).add(x);  // multimap
m.containsKey(key);  m.remove(key);
```

Padrão "agrupar coisas por chave" (aparece MUITO em problemas de logística):

```java
Map<String, List<Order>> byZone = new HashMap<>();
for (Order o : orders) {
    byZone.computeIfAbsent(o.zone(), z -> new ArrayList<>()).add(o);
}
```

---

## 3. Iteração

```java
for (String s : list) { ... }

for (Map.Entry<String, Integer> e : counts.entrySet()) {
    String k = e.getKey();
    int v = e.getValue();
}

for (String k : m.keySet())   { ... }
for (String v : m.values())   { ... }

for (int i = 0; i < arr.length; i++) { ... }

Iterator<Order> it = list.iterator();   // remoção manual durante iteração
while (it.hasNext()) { if (bad(it.next())) it.remove(); }
```

---

## 4. Strings — parsing de input (validar formato de pedido, etc.)

```java
String s = "A1,downtown,5.00,3.00";
String[] parts = s.split(",");
String[] limit  = s.split(",", 4);   // no máx 4 pedaços

s.trim();  s.strip();                 // strip é unicode-aware
s.isEmpty();  s.isBlank();            // blank = só espaços
s.toLowerCase();  s.contains("x");
s.startsWith("A");  s.endsWith("00");
s.substring(0, 2);  s.charAt(0);  s.indexOf(",");
s.replace(",", ";");

Integer.parseInt(parts[0].trim());
Double.parseDouble(parts[2]);
String.join(",", list);              // junta lista em CSV
String.valueOf(42);

StringBuilder sb = new StringBuilder();
sb.append("x").append(y);
sb.toString();

// text block (Java 15+) — bom pra JSON/fixtures multi-linha
String json = """
    {"id": "A1", "zone": "downtown"}
    """;
```

---

## 5. Números / Math

```java
Math.max(a, b);  Math.min(a, b);  Math.abs(x);
Math.round(x);   Math.ceil(x);    Math.floor(x);
Math.pow(2, 10); Math.sqrt(x);

int div = 7 / 2;        // 3  (divisão inteira trunca!)
int rem = 7 % 2;        // 1
double d = 7.0 / 2;     // 3.5 — precisa de UM double na conta

Integer.MAX_VALUE;  Integer.MIN_VALUE;   // cuidado com overflow em somas
long big = (long) a * b;                 // faça cast ANTES de estourar int

Integer.parseInt("42");  Double.parseDouble("4.2");
Integer.compare(a, b);   Double.compare(a, b);
```

---

## 6. Arrays

```java
int[] a = new int[5];          // zeros
int[] b = {1, 2, 3};
int[][] grid = new int[3][4];
a.length;                      // atributo, não método

Arrays.sort(b);
Arrays.fill(a, -1);
int[] copy = Arrays.copyOf(b, b.length);
Arrays.asList(1, 2, 3);        // wrapper de TAMANHO FIXO (cuidado)
Arrays.toString(b);            // pra debug
Arrays.stream(b).sum();
```

---

## 7. Ordenação / Comparator (peak-pay por zona, ordenar por tempo, etc.)

```java
list.sort(Comparator.comparingInt(Order::getTime));
list.sort(Comparator.comparingDouble(Order::getPay).reversed());
list.sort(Comparator.comparing(Order::getName)
                    .thenComparing(Order::getId));

Collections.sort(list);              // ordem natural (se Comparable)

// Comparable na sua própria classe:
class Order implements Comparable<Order> {
    public int compareTo(Order o) { return Integer.compare(time, o.time); }
}
```

---

## 8. PriorityQueue / Heap (dispatch: motorista mais próximo, deadline mais cedo)

```java
// min-heap por padrão (menor sai primeiro)
PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.offer(5);  pq.poll();   // remove e retorna o MENOR
pq.peek();                 // olha sem remover

// motorista mais próximo primeiro
PriorityQueue<Driver> byDist =
    new PriorityQueue<>(Comparator.comparingDouble(Driver::distance));

// max-heap (maior sai primeiro)
PriorityQueue<Integer> max = new PriorityQueue<>(Comparator.reverseOrder());
```

Uso típico: "atribua cada pedido ao Dasher livre mais próximo" → heap por distância.

---

## 9. Optional (a dependência upstream pode vir nula)

```java
Optional<Order> maybe = repo.find(id);
maybe.isPresent();
maybe.orElse(defaultOrder);
maybe.orElseThrow(() -> new IllegalStateException("pedido sumiu"));
maybe.map(Order::tip).orElse(0.0);
Optional.ofNullable(x);   // embrulha valor que talvez seja null
```

---

## 10. Exceptions, validação e try-with-resources (malformed input — eles TESTAM)

```java
if (units < 0)
    throw new IllegalArgumentException("units negativo: " + units);

Objects.requireNonNull(order, "order não pode ser nulo");

try {
    int n = Integer.parseInt(raw);
} catch (NumberFormatException e) {
    // pula a linha malformada / loga / ou repropaga — decida e verbalize
}

// fecha recurso automaticamente, mesmo com exceção
try (var reader = new BufferedReader(new FileReader("in.txt"))) {
    reader.readLine();
}

// exceção de domínio própria (mostra intenção)
class InvalidOrderException extends RuntimeException {
    InvalidOrderException(String msg) { super(msg); }
}
```

Checked (obriga try/catch, ex. IOException) vs unchecked (RuntimeException, ex.
IllegalArgumentException). Em regra de negócio, prefira unchecked com mensagem clara.

---

## 11. Modelagem — records e enums (deixa o código limpo em segundos)

```java
// Java 16+: DTO imutável com equals/hashCode/toString de graça
record Order(String id, String zone, double basePay, double tip) {
    // compact constructor: validação na construção
    Order {
        if (tip < 0) throw new IllegalArgumentException("tip negativo");
    }
}

Order o = new Order("A1", "downtown", 5.0, 3.0);
o.basePay();   // acesso: nome do campo, SEM "get"

enum Status {
    CREATED, PICKED_UP, DELIVERED;
    boolean isTerminal() { return this == DELIVERED; }   // enum pode ter método
}

// máquina de estados = switch limpo
Status next = switch (s) {
    case CREATED   -> Status.PICKED_UP;
    case PICKED_UP -> Status.DELIVERED;
    case DELIVERED -> Status.DELIVERED;
};
```

---

## 12. Objeto como chave de Map / elemento de Set — o gotcha silencioso

```java
// Classe custom como CHAVE de HashMap ou item de HashSet
// PRECISA de equals + hashCode, senão vira lookup quebrado.
// record já faz isso de graça:
record OrderId(String value) {}          // seguro como chave

// Sem record, sobrescreva os dois JUNTOS:
@Override public boolean equals(Object o) {
    if (this == o) return true;
    if (!(o instanceof Point p)) return false;   // pattern matching (Java 16+)
    return x == p.x && y == p.y;
}
@Override public int hashCode() { return Objects.hash(x, y); }
```

---

## 13. Interface vs classe abstrata (pergunta clássica — saiba justificar)

```java
// INTERFACE: contrato ("o quê"), múltipla implementação, sem estado mutável
interface PayRule { double apply(DasherDay d, double total); }

interface Notifier {
    void send(String msg);
    default void sendAll(List<String> msgs) { msgs.forEach(this::send); } // default
    static Notifier noop() { return msg -> {}; }                         // static
}

// CLASSE ABSTRATA: estado + esqueleto de comportamento compartilhado ("como")
abstract class BaseRule implements PayRule {
    protected final String name;
    BaseRule(String name) { this.name = name; }
    abstract double compute(DasherDay d);          // subclasse preenche
    public double apply(DasherDay d, double total) { return total + compute(d); }
}
```

Regra de bolso: interface pro contrato, composição pra reuso. Herança só quando
há "é um" real. Prefira interface + composição a hierarquias profundas.

---

## 14. Generics (classe e método genérico + wildcards)

```java
// classe genérica
class Repository<T> {
    private final Map<String, T> store = new HashMap<>();
    void save(String id, T item) { store.put(id, item); }
    Optional<T> find(String id)  { return Optional.ofNullable(store.get(id)); }
}
Repository<Order> repo = new Repository<>();

// método genérico
static <T> T firstOrNull(List<T> list) {
    return list.isEmpty() ? null : list.get(0);
}

// bounded + wildcards — mnemônico PECS: Producer Extends, Consumer Super
double sumPay(List<? extends Order> src) { ... }   // só LÊ de src
void drainInto(List<? super Order> sink) { ... }   // só ESCREVE em sink
<T extends Comparable<T>> T maxOf(List<T> xs) { ... }
```

---

## 15. Functional interfaces + method references (Java 8+, caem sempre)

```java
Function<Order, Double>          toPay   = Order::basePay;       // T -> R
Supplier<Order>                  factory = Order::new;           // () -> T
Consumer<Order>                  log     = System.out::println;  // T -> void
Predicate<Order>                 valid   = o -> o.tip() >= 0;    // T -> boolean
BiFunction<Double,Double,Double> add     = Double::sum;          // (T,U) -> R
UnaryOperator<Double>            round2  = x -> Math.round(x*100)/100.0; // T -> T

toPay.apply(o);   valid.test(o);   factory.get();   log.accept(o);   add.apply(1.0,2.0);

// 4 formas de method reference:
Order::basePay        // método de instância de objeto arbitrário do tipo
System.out::println   // método de instância de objeto específico
Order::new            // construtor
Math::max             // método estático
```

---

## 16. Streams — com moderação

Em live-coding, loop explícito costuma ser mais fácil de narrar. Mas domine estes:

```java
int total = list.stream().mapToInt(Order::getUnits).sum();

List<Order> big = list.stream()
    .filter(o -> o.tip() > 2.0)
    .collect(Collectors.toList());       // ou .toList() no Java 16+

Map<String, List<Order>> byZone = list.stream()
    .collect(Collectors.groupingBy(Order::zone));

Map<String, Double> payByZone = list.stream()
    .collect(Collectors.groupingBy(Order::zone,
             Collectors.summingDouble(Order::basePay)));

double sum = list.stream().mapToDouble(Order::tip)
                 .reduce(0, Double::sum);   // reduce genérico
long n = list.stream().filter(o -> o.tip() > 0).count();
Optional<Order> maxTip = list.stream().max(Comparator.comparingDouble(Order::tip));
boolean any = list.stream().anyMatch(o -> o.tip() < 0);
```

---

## 17. Datas / janelas de entrega (delivery windows)

```java
Instant now = Instant.now();
Instant deadline = now.plus(Duration.ofMinutes(30));
now.isBefore(deadline);  now.isAfter(deadline);

long mins = Duration.between(start, end).toMinutes();
Duration.ofSeconds(90);  Duration.ofMinutes(15);

LocalDateTime dt = LocalDateTime.now();
LocalTime peakStart = LocalTime.of(17, 0);
time.isAfter(peakStart);   // ex.: aplicar peak-pay em janela de horário
```

---

## 18. Dinheiro — o detalhe que pontua no payout service

```java
// double perde precisão com dinheiro. Mencione isso em voz alta.
BigDecimal base = new BigDecimal("5.00");   // use String, NUNCA new BigDecimal(5.0)
BigDecimal tip  = new BigDecimal("3.25");
BigDecimal pay  = base.add(tip);
pay = pay.setScale(2, RoundingMode.HALF_UP);
pay.compareTo(minimo) < 0;   // compare com compareTo, NUNCA com == nem equals
```

Regra prática: code com `double` pela agilidade se quiser, mas **verbalize** o trade-off.

---

## 19. Collections — utilitários que salvam

```java
Collections.reverse(list);
Collections.sort(list);
Collections.max(list);  Collections.min(list);
Collections.frequency(list, x);
Collections.emptyList();  Collections.singletonList(x);

list.removeIf(o -> o.tip() < 0);        // remoção segura durante "iteração"
List<Integer> copy = new ArrayList<>(original);   // cópia defensiva

set.retainAll(other);   // interseção
set.addAll(other);      // união
set.removeAll(other);   // diferença
```

---

## 20. var, ternário, varargs e açúcar sintático

```java
var counts = new HashMap<String, Integer>();   // inferência (só em locais)
var order  = new Order("A1", "z", 5, 3);

int x = cond ? 1 : 0;                           // ternário

// varargs — número variável de argumentos
static double total(double... vals) {
    double s = 0; for (double v : vals) s += v; return s;
}
total(1, 2, 3);   total();

// enhanced switch com yield pra lógica de vários passos
int score = switch (status) {
    case CREATED   -> 1;
    case DELIVERED -> { yield compute(); }
    default        -> 0;
};
```

---

## 21. Gotchas de OO e tipos (perguntas-pegadinha)

```java
// overloading (compile-time): mesmo nome, assinaturas diferentes
double pay(Order o) { ... }
double pay(Order o, double bonus) { ... }

// overriding (runtime): subclasse redefine método da super — use @Override
@Override public double apply(DasherDay d, double t) { ... }

// AUTOBOXING: == compara REFERÊNCIA em wrappers, não valor
Integer a = 1000, b = 1000;
a == b;          // false! (fora do cache -128..127)
a.equals(b);     // true  — SEMPRE equals pra Integer/Long/Double
int p = a;       // unboxing OK; cuidado com NPE se 'a' for null

// final: constante / não sobrescrevível / não herdável
static final double PEAK_BONUS = 2.0;
```

---

## 22. Concorrência / thread-safety (se perguntarem "e se for multi-thread?")

```java
// HashMap NÃO é thread-safe. Sob acesso concorrente:
Map<String,Integer> safe = new ConcurrentHashMap<>();
safe.merge(key, 1, Integer::sum);          // atômico

AtomicInteger counter = new AtomicInteger();
counter.incrementAndGet();                 // sem lock, atômico

synchronized (lock) { /* seção crítica */ }

// A melhor defesa: imutabilidade. Objeto imutável (record) é thread-safe de graça.
```

---

## 23. Testes rápidos sem framework (se não tiver JUnit no ambiente)

```java
static void check(String label, boolean cond) {
    System.out.println((cond ? "PASS " : "FAIL ") + label);
}

check("gorjeta baixa aciona minimo", pay == 10.0);
check("zona sem peak nao ganha bonus", bonus == 0.0);
check("lista vazia retorna 0", calc(List.of()) == 0.0);
```

Se tiver JUnit:

```java
@Test
void gorjetaBaixaAcionaMinimo() {
    assertEquals(10.0, engine.calculate(day), 0.001);
}
```

---

## 24. Edge cases pra perguntar ANTES de codar (os 2-3 min iniciais)

- Lista/dataset vazio?
- Valores negativos ou zero (gorjeta negativa? tempo zero?)
- Chaves/IDs duplicados?
- Ordem dos eventos garantida ou preciso ordenar?
- Concorrência importa ou é single-threaded?
- A dependência upstream pode falhar / vir nula?
- Precisão de dinheiro / arredondamento?
- Input malformado: pular, logar ou lançar?

---

## 25. O ritual (decore a sequência, não a solução)

1. **Clarifica** (2-3 min) — requisitos + edge cases acima.
2. **Modela os tipos** — records/enums pras entidades. Interface pras regras.
3. **Separa regra de I/O** — cada regra de pagamento = uma unidade isolada
   (método, estratégia, ou entrada numa lista). Assim, quando ele mudar uma
   regra no fim, você adiciona/edita UMA coisa, não reescreve tudo.
4. **Resolve o caso base** — o exemplo mais simples do enunciado.
5. **Testa** — 3 casos, incluindo um edge case, sem pedirem.
6. **Narra os trade-offs** o tempo todo. Silêncio = ponto perdido.

---

## Esqueleto extensível pra regras de pagamento (o padrão que vence)

```java
interface PayRule {
    double apply(DasherDay day, double runningTotal);
}

class BasePayRule implements PayRule {
    public double apply(DasherDay d, double total) {
        return total + d.baseForAllOrders();
    }
}

class PeakZoneBonus implements PayRule {
    public double apply(DasherDay d, double total) {
        return total + d.ordersInPeakZones() * 2.0;
    }
}

class MinimumGuarantee implements PayRule {
    private final double floor;
    MinimumGuarantee(double floor) { this.floor = floor; }
    public double apply(DasherDay d, double total) {
        return Math.max(total, floor);  // aplica por ÚLTIMO
    }
}

// A engine só orquestra. Adicionar regra nova = adicionar na lista.
class PayEngine {
    private final List<PayRule> rules;
    PayEngine(List<PayRule> rules) { this.rules = rules; }
    double calculate(DasherDay day) {
        double total = 0;
        for (PayRule r : rules) total = r.apply(day, total);
        return total;
    }
}
```

Quando o entrevistador disser "agora adiciona um bônus de chuva", você adiciona
uma classe `RainBonus` e uma linha na lista. É isso que eles querem ver.
