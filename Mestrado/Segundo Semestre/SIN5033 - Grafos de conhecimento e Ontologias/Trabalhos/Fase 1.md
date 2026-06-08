# 1. Introdução e domínio

A empresa de distribuição de filmes online "Amazing Video" deseja um sistema de recomendação que combine duas abordagens: recomendação por conteúdo, que "casa" as características dos filmes com as preferências dos usuários, e recomendação social ou colaborativa, que usa as notas dadas pelos usuários para sugerir filmes apreciados por pessoas com gostos semelhantes.

O sistema se apoia em um base de conhecimento construída a partir de uma ontologia de filmes e das informações e preferências dos usuários. Este documento corresponde a "Fase 1" do trabalho e cobre o projeto da ontologia, a definição das classes, propriedades e axiomas ,e a representação da base de conhecimento em OWL/RDF. A implementação da aplicação é tratada na "Fase 2".

# 2. Metologia de construção

A ontologia foi desenvolvida seguindo o processo clássico de construção descrito por Noy e McGuinness, organizado nas seguintes etapas:

1. Definir o domínio e o escopo: catálogo de filmes, usuários, preferências e avaliações, com foco em apoiar a recomendação híbrida.
2. Considerar o reuso de vocabulários existentes.
3. Enumerar os termos relevantes do domínio.
4. Definir as classes e a hierarquia de classes.
5. Definir as propriedades (de objeto e de dados) com domínio e contradomínio.
6. Definir as restrições e axiomas que dão semântica e capacidade de inferência.
7. Criar instâncias para popular a base de conhecimento.

**Reuso de vocabulários**: os conceitos centrais foram alinhados, via `rdfs:seeAlso`, a vocabulários consolidados. A classe `Filme` remete a `schema:Movie` e as classes `Pessoa` e `Usuário` remetem a `foaf:Person` e `schema:Person`. Esse alinhamento sinaliza a interoperabilidade sem abrir mão de uma ontologia própria, ajustada a tarefa de recomendação.

**Linguagem e ferramentas**: a ontologia foi escrita em OWL 2, serializada no formato Turtle (RDF). A modelagem e a verificação de consistência são feitas no Protegé, com o reasoner HermiT. A implementação prevista para a Fase 2 utiliza Python com a bilioteca OWLReady2.

# 3. Modelagem da Ontologia
## 3.1 Classes e hierarquia
As classes de topo do domínio são `Filme`, `Pessoa`, `Usuário`, `Gênero`, `Prêmio`, `Evento`, `