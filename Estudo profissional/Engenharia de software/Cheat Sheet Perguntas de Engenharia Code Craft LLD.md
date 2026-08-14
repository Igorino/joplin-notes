# Cheat Sheet — Perguntas de Engenharia (Code Craft / LLD)

Perguntas que o entrevistador solta ENQUANTO você resolve, pra sondar tua
maturidade. Cada resposta é curta de propósito — é pra você falar em voz alta,
não recitar parágrafo. Sempre que der, ancore no problema (payout / dispatch).

Regra geral: eles não querem que você recite padrões. Querem ver **julgamento** —
por que essa escolha, qual o trade-off, quando você NÃO faria assim.

---

## 1. Princípios de design (os que resolvem o "a regra muda no fim")

**P: Como garante que adicionar uma regra de pagamento nova não quebre as existentes?**
R: Open/Closed Principle — aberto pra extensão, fechado pra modificação. Cada regra
implementa uma interface `PayRule` e entra numa lista. Regra nova = classe nova +
uma linha, sem tocar no que já funciona nem re-testar o resto.

**P: Por que uma interface aqui em vez de uma classe concreta?**
R: Dependency Inversion — a engine depende da abstração `PayRule`, não de regras
concretas. Isso me dá testabilidade (mock/stub fácil), troca de implementação e
extensão sem editar a engine. É o que desacopla o "o quê" do "como".

**P: Onde está o Single Responsibility no teu design?**
R: Separei três responsabilidades que costumam virar uma bola só: parsing/I/O
(ler o input), as regras de negócio (cada uma isolada), e a orquestração (a engine
que soma). Cada uma muda por um motivo diferente, então cada uma é uma unidade.

**P: Composição ou herança aqui?**
R: Composição. A engine COMPÕE uma lista de regras em vez de herdar comportamento.
Herança acopla forte e quebra com hierarquia profunda; composição deixa eu montar
e reordenar regras em runtime. Herança só quando há um "é-um" real e estável.

**P: Como você pensa em coesão e acoplamento neste código?**
R: Alta coesão dentro de cada regra (faz uma coisa só) e baixo acoplamento entre
elas (nenhuma regra conhece as outras; só recebem o total corrente). Isso é o que
permite a mudança de última hora ser barata.

**P: E os outros dois do SOLID (Liskov, Interface Segregation)?**
R: Liskov: qualquer `PayRule` pode substituir outra sem quebrar a engine, porque
todas honram o mesmo contrato (recebe total, devolve total). ISP: a interface tem
um método só — ninguém é forçado a implementar coisa que não usa.

---

## 2. Padrões — saiba nomear DEPOIS de resolver, e só se encaixar

**P: Que padrão é esse teu design de regras?**
R: Strategy — comportamentos intercambiáveis atrás de uma interface comum,
eliminando um `if/else` gigante. Se as regras formassem um pipeline com
possibilidade de "parar aqui", seria Chain of Responsibility.

**P: E se eu quiser escolher o conjunto de regras por tipo de Dasher/mercado?**
R: Factory — uma `RuleSetFactory` que, dado o contexto (mercado, tier), devolve a
lista de regras montada. Mantém a decisão de "quais regras" fora da engine.

**P: Como modelaria o ciclo de vida do pedido (created → picked up → delivered)?**
R: State pattern ou uma máquina de estados com enum. O enum guarda as transições
válidas; tentativa de transição inválida lança. Evita flags booleanas espalhadas.

**P: Quero adicionar um multiplicador que embrulha o cálculo em runtime.**
R: Decorator — envolve uma `PayRule` com outra que ajusta o resultado, sem alterar
a original. Bom pra comportamento opcional empilhável.

**P: Preciso notificar outros serviços quando o pagamento é calculado.**
R: Observer — a engine publica um evento e os interessados (auditoria, notificação)
se inscrevem. Desacopla o cálculo das reações a ele.

**P: E se o objeto de configuração tiver muitos campos opcionais?**
R: Builder — construção legível e imutável, sem telescoping de construtores.

**P: Qual padrão você NÃO usaria aqui?**
R: Singleton pra regra — vira estado global escondido e mata testabilidade. E não
forço padrão nenhum: se um `for` sobre uma lista resolve, é isso. Padrão que não
paga o próprio custo de abstração é over-engineering.

---

## 3. Estruturas de dados e complexidade (justifique a escolha)

**P: Por que HashMap aqui?**
R: Lookup por chave em O(1) médio, que é o acesso dominante (buscar Dasher/zona por
id). Se eu precisasse iterar em ordem de chave, `TreeMap` (O(log n), ordenado); se
precisasse manter ordem de inserção, `LinkedHashMap`.

**P: E pra atribuir o pedido ao Dasher mais próximo?**
R: PriorityQueue (min-heap) por distância — `poll()` me dá o mais próximo em
O(log n). Varrer uma lista seria O(n) por atribuição.

**P: Custo das operações que você está usando?**
R: HashMap get/put O(1) médio; ArrayList get O(1), contains O(n), add amortizado
O(1); ordenar O(n log n); heap offer/poll O(log n). Escolho a estrutura pelo acesso
mais frequente, não pelo mais raro.

**P: Como isso se comporta com 1 milhão de pedidos?**
R: O gargalo seria qualquer operação O(n) dentro de loop. Meu cálculo é uma passada
linear pelas regras × pedidos, então O(n·r) com r pequeno e fixo. Sem estrutura
aninhada quadrática. Se precisasse, agruparia por zona uma vez em vez de re-filtrar.

---

## 4. Correção e robustez (onde eles cutucam de propósito)

**P: E se o mesmo evento de pagamento chegar duas vezes?**
R: Idempotência — cada cálculo é chaveado por um id idempotente (ex.: delivery id +
dia). Reprocessar produz o mesmo resultado, não paga em dobro. Guardo os já
processados num set/map e ignoro duplicata. (DoorDash valoriza muito isso.)

**P: E se rodar em várias threads?**
R: O cálculo em si é sem estado, então é seguro se as regras forem imutáveis. Estado
compartilhado (cache de processados, contadores) vira `ConcurrentHashMap` /
`AtomicInteger`. Prefiro imutabilidade a lock sempre que dá.

**P: Como trata input malformado?**
R: Decisão explícita e verbalizada: para dado corrompido eu falho rápido com
exceção de domínio clara (`InvalidOrderException`) se for crítico; se for tolerável,
pulo a linha e registro. O que não faço é engolir em silêncio e propagar lixo.

**P: null ou Optional?**
R: `Optional` no retorno de busca que pode não achar (deixa a ausência explícita no
tipo e força o chamador a tratar). Não uso `Optional` em campo nem parâmetro — lá
prefiro `Objects.requireNonNull` e falhar cedo.

**P: E a precisão do dinheiro?**
R: `double` acumula erro de ponto flutuante; em produção seria `BigDecimal` com
escala e `RoundingMode` definidos, comparado por `compareTo`. Em live-coding uso
`double` pela velocidade mas deixo o TODO explícito.

---

## 5. Modelagem de domínio

**P: Esse `Order` é entidade ou value object?**
R: `OrderId` é value object (imutável, igualdade por valor — `record`). O pedido em
si, se tem identidade e ciclo de vida próprio, é entidade (igualdade por id). A
distinção guia equals/hashCode e imutabilidade.

**P: Por que imutável?**
R: Previsibilidade e thread-safety de graça — ninguém muda o objeto por baixo. Uso
`record` pra ganhar isso sem boilerplate. Muto criando cópia, não alterando estado.

**P: Por que enum em vez de String/constante pro status?**
R: Type safety — o compilador barra estado inválido, o `switch` fica exaustivo, e o
enum pode carregar comportamento (transições válidas). String mágica não dá nada
disso e vaza typo pra runtime.

---

## 6. Testes

**P: O que você testaria aqui?**
R: Caso base (uma regra, valor esperado), composição (regras somam na ordem certa),
e os edge cases: lista vazia → 0, gorjeta negativa rejeitada, mínimo acionado quando
a soma fica abaixo do piso, e o mínimo NÃO acionado quando fica acima.

**P: Como testa que o design é extensível?**
R: Cada regra é testável isolada, sem a engine. E adiciono uma regra fake no teste
pra provar que a engine a incorpora sem alteração. Se testar extensão exige mexer na
engine, o design falhou.

**P: Unit ou integration?**
R: Unit pras regras e pra engine (rápido, determinístico). Integration só na borda
que chama a dependência upstream, com o cliente mockado. A regra de negócio não
deve precisar de I/O pra ser testada.

---

## 7. Trade-offs e meta (mostram senioridade)

**P: Por que não otimizou isso?**
R: Legibilidade primeiro; otimizo quando um número justifica. Micro-otimizar cedo
esconde intenção e raramente é o gargalo real. Deixo claro onde otimizaria se o
perfil de carga pedisse.

**P: Se tivesse mais tempo, o que melhoraria?**
R: Trocar `double` por `BigDecimal`, extrair a montagem de regras pra uma factory
configurável, adicionar idempotência persistente, e cobrir concorrência se o serviço
for chamado em paralelo. Digo isso em voz alta mesmo sem implementar — mostra que sei
a diferença entre protótipo de entrevista e código de produção.

**P: Como isso viraria um serviço de verdade?**
R: A engine fica no core (sem dependência de framework); parsing e a chamada upstream
ficam nas bordas (adapters). É basicamente Ports & Adapters — o domínio não sabe se o
input veio de REST, fila ou arquivo. (Esse é o teu terreno; use.)

---

## Colinha de 30 segundos antes de abrir o editor

- Clarificar → modelar tipos → separar regra de I/O → caso base → testes → narrar.
- Toda regra atrás de uma interface, numa lista. OCP é a estrela do show.
- Nomeie o padrão DEPOIS de usá-lo, e só se encaixar de verdade.
- Fale os trade-offs: dinheiro, null, concorrência, idempotência, complexidade.
- Quando ele mudar a regra: sorria, é o teste. Uma classe nova, uma linha na lista.
