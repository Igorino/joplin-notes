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
Isso aí é como uma "Foto aérea do campo". 