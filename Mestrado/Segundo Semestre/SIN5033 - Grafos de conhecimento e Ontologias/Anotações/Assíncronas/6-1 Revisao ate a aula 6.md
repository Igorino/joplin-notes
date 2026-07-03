# Aula 01 - Conceitos Básicos: Dos dados ao conhecimento

É um aula "Filosófica" que prepara pro resto da matéria. Coisa principal: **Pirâmide DIKW** (Data -> Information -> Knowledge -> Wisdom)

- **Dados** são como os ingredientes de uma cozinha: "37, "molhado", "p". Sozinhos eles não conseguem dizer nada.
- **Informação** é quando você organiza esses dados de uma forma útil: "a temperatura é 37 graus Célsius".
- **Conhecimento** é saber o que isso significa: "37 graus de febre indica que a pessoa está doente". A informação foi enriquecida com a *semântica*.
- **Sabedoria** é decidir o que fazer depois disso. Exemplo: "Levar ao médico se a febre for 37 graus Célsius". É a capacidade de fazer bons julgamentos.

A aula também martela um ponto: **significado depende de contexto**. O exemplo clássico que é usado no slide é a frase "O jaguar parece elegante". Podemos estar falando do carro ou do animal.

A mesma sequência de símbolos muda de sentido conforme o entorno. É por isso que o curso inteiro vai atrás de formas de deixar o significado **explícito e sem ambiguidade**, primeiro para nós humanos e depois para as máquinas.

# Aula 02 - Web Semântica: Introdução
Aqui entra o problema central do curso. A web de hoje é como uma **biblioteca gigante onde os livros estão escritos, mas o bibliotecário (o computador) não sabe ler ela de forma eficiente**. Ele só consegue pegar o livro pela capa e pelas palavras-chave. Ele não entende que "Lisa Davenport é fisioterapeuta".

A Web Semântica quer dar **olhos de leitura pra máquina**. As três tecnologias principais para isso são:
1. **Grafos rotulados** como modelos de dados. Objetos viram nós, relações viram setas. O formalismo é o **RDF** (Resource Description Framework), que faz frases simples no formato **sujeito -> predicado -> objeto** (ou, uma "tripla"): Lisa -> Trabalha para -> EmpresaA. É praticamente uma frase de criança: sujeito, verbo e complemento.
2. **URIs** (Uniform Resource Identifier). São endereços únicos globais pra identificar cada coisa (como um CPF pra conceitos, em vez de só "Lisa", que seria meio ambíguo).
3. **Ontologias**. Que são vocabulários hierárquicos que dizem como que as coisas *são* e *como se relacionam*.

A aula apresenta o famoso **"Bolo de camadas"**: na base, o **XML** (sintaxe). Acima dele, **RDF** (fatos), e **RDF Schema** (Ontologia simples). E no topo de tudo, o **OWL** (Ontology Web Language, que é uma linguagem ontológica robusta).

Por que subir até o OWL? Porque o RDFS é fraquinho: ele não sabe dizer "ninguém pode ser Homem e Mulher ao mesmo tempo" ou "uma pessoa tem no máximo 1 nome". O OWL traz cardinalidade, disjunção, equivalência de classes, etc. É a diferença entre um dicionário de bolso e uma enciclopédia com regras de inferência.

# Aula 03 - Evolução da Web Semântica

Essa aula é a aula "árvore genealógica". Ela mostra que a Web Semântica não nasceu do nada, ela é o último ramo de uma evolução:

**Memex (1945) -> Hipertexto (1965) -> Hipermídia -> Web (1990) -> Web Semântica (2001) -> Web de dados / Linked Data (2006) -> Grafos de Conhecimento (2012)**

O coração da aula são os **Princípios dos Dados Ligados (Berners-Lee, 2006)** que funcionam como um "manual de boas maneiras" pra publicar dados:
- Use **URIs HTTP** como nomes pras coisas (não só pras páginas);
- Forneça informação útil em RDF quando alguém acessar a URI;
- **Inclua links pra outras URIs**, pra que os dados se conectem.

⭐⭐⭐⭐⭐
É o tal de **Esquema das 5 estrelas**: quanto mais aberto e interligado o dado, mais estrelas. A filosofia é *bottom-up*: em vez de discutir linguagens perfeitas, o foco é basicamente em **conectar dados estruturados na web**, como costurar ilhas de informação numa rede. 

O resultado: a "Nuvem LOD" saltou de 570 datasets (2014) pra mais de 1300 datasets e 16.000 links (2020)

# Aula 03.1, 03.2 e 03.3 - As três leituras acadêmicas

Esses três PDFs são artigos científicos que aprofundam a aula 03 sob ângulos diferentes. 

## 03.1 - Knowledge Graphs *(Gutierrez & Sequeda, Communications of the ACM, 2021)*
Esse conta a história de amor conturbada entre dados e conhecimento. É a saga de dois irmãos, a lógica (raciocínio) e a estatística (dados, padrões), que ora se ignoram e ora se abraçam.

Momentos marcantes: o workshop "Logic and Data Bases" (Toulouse, 1977) que casou lógica com bancos de dados. O Datalog (um subconjunto do Prolog pra dados). O boom dos sistemas especialistas nos anos 80, com tanto hype que viraram a "estrela a IA", até o "Inverno da IA" quando se descobriu que eram caros, difíceis de mantes e quebradiços (o famoso gargalo de aquisição de conhecimento).

A grande lição: integrar lógica e dados precisa ser um casamento bem amarrado, não só empilhar uma coisa sobre a outra. E o termo "Knowledge Graph" que a Google popularizou em 2012? É na verdade uma ideia antiga! Já aparecia numa tese de 1982, ela só encontrou finalmente o hardware e o momento certo.

## 03.2 - A Review of the Semantic Web Field (Pascal Hitzler, CACM, 2021)
Isso aí é como uma "Foto aérea do campo". É um balanço maduro de duas décadas. Um artigo da Scientific American de 2001 pelo GOAT Berners-Lee é frequentemente apontado como o marco de nascimento do campo.

O artigo divide a história em eras:
- **Era das Ontologias** (inícios dos anos 2000): muita empolgação, ontologias ricas, mas por volta de meados dos anos 2000, expectativas exageradas deram lugar a puma perspectiva mais sóbria, porque ontologias eram difíceis de manter e reutilizar.
- **Era do Linked Data** (2006 em diante): abordagem mais simples e prática. Conectar grafos RDF. DBpedia, extraída da Wikipedia, é um dos datasets mais conhecidos dessa época, cobrindo cerca de 6 milhões de entidades.
- **Era dos Grafos de Conhecimento** (puxada pela indústria)

O fio condutor são os três padrões da W3C que servem como uma "Língua franca": RDF, OWL e SPARQL (conhecido como o "SQL dos grafos")

## 03.3 - Knowledge Representation and the Semantic Web
Este é o documentários sobre as raízes profundas. Chega a Turing e Church nos anos 1930. A joia dessa leitura é o trade-off fundamental da representação do conhecimento:
> Quanto **mais expressiva** a linguagem, **mais lento** (ou impossível) é o racionador automático.

É tipo um carro esportivo cheio de recursos: cada botão extra deixa o carro mais pesado e difícil de dirigir. A Lógica de Primeira Ordem (FOL) é tão poderosa que se torna *indecidível*. O programa pode nunca parar de calcular. Esse dilema é o que motiva, lá na frente, escolher uma lógica mais "comportada". O artigo também reabilita os sistemas de regras: não foram um fracasso total, eles venceram disfarçados, virando a lógica de negócio de sistemas corporativos.

# Aula 04 - Lógica e Raciocínio Automatizado

Agora o curso muda de marcha: sai da história e entra na maquinaria. Essa aula é a **gramática do raciocínio**.

A **lógica proposicional** monta argumentos com tijolinhos chamados de proposições (`p`, `q`) e cola eles com conectivos: $\neg$ (não), $\land$ (e), $\lor$ (ou), $\rarr$ (então).

**Tabela-verdade** é o método "força bruta": testa *todas* as combinações possíveis.

E qual seria o problema? Com $n$ símbolos, ela teria **$2^n$ linhas**. Com só 10 proposições já seria 1024 linhas. Seria como verificar se uma fechadura funciona testando todas as combinações: garante o resultado eventualmente, mas não é viável na prática.

É aí que chega as **regras de inferência**: elas são como "atalhos elegantes" que foram herdados de Aristóteles:

- **Modus Ponens**: de "$\text{se chove} \rarr \text{a rua molha}$" e "$\text{choveu}$", conclui-se "$\text{a rua molhou}$". É o clássico de "destacar" o consequente.
- **Modus Tollens**: de "$\text{se chove} \rarr \text{a rua molha}$" e "$\text{a rua NÃO molhou}$", conclui-se "$\text{NÃO choveu}$".
- **Silogismo Hipotético**: de $A \rarr B$ e $B \rarr C$, conclui-se $A \rarr C$. Isso é o encadeamento de dominós, ou relação transitiva na lógica.

A aula fecha com duas ideias que vão estruturar tudo daqui pra frente: **validade** (verdade em todos os modelos) e **satisfatibilidade** (verdade em *algum* modelo), além das propriedades que todos sistema de prova precisa ter: **corretude** (só prova o que é verdade) e **completude** (prova tudo que é verdade).

# Aula 05 - Solução para exercícios de Lógica.
Essa aula é um "**gabarito comentado**", onde a teoria da Aula 04 ganha força com exercícios resolvidos. 

Os exercícios cobre uma escada de dificuldade:
- **Tradução**: pegar frases em português ("Se Ana é alta e magra, então é elegante") e transforma ela em fórmulas ($p \rarr q$);
- **Tabelas-verdade**: Para testar argumentos do mundo real. (Como "se chove, a rua molha", etc.);
- **Provas por refutação**: em vez de provar $r$ diretamente, você *assume o contrário* ($\neg r$) e mostra que isso gera uma contradição ($\perp$). Ou seja, uma **prova por absurdo**;
- **Prolog e resolução SLD**: entra a lógica de programação, com aquele charmoso exemplo de "quem namora quem" e "quem é infiel", usando o `trace` pra enxergar o motor de inferência trabalhando.
- **Unificação** (lógica de primeira ordem): casar padrões como `cor(sapato(x), branco)` com `cor(sapato(suspeito), y)`, descobrindo que `x = suspeito` e `y = branco`. Como encaixar peças de quebra-cabeças.

# Aula 06 - Lógica de Descrições (DL)
A aula 6 amarra tudo. Pega o trade-off do 03.3 (expressividade vs. velocidade) e resolve com a Lógica de Descrições, já que ela não é nem fraca demais, nem expressiva demais a ponto de travar. Ponto "Cachinhos Dourados". É um **fragmento decidível da FOL**: poderoso o suficiente pra ser útil, mas comportado o suficiente pra sempre terminar o cálculo. Ele é a **base teórica do OWL** (a Web Ontology Language usa a Lógica de Descrições chamada de SROIQ(D)).

A linguagem mínima ensinada é a **ALC**. Ela organiza o conhecimento em "caixas": 

.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.
.