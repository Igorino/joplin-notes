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
As classes de topo do domínio são `Filme`, `Pessoa`, `Usuário`, `Gênero`, `Prêmio`, `Evento`, `País`, `Idioma` e `Avaliação`, declaradas mutualmente disjuntas. A hierarquia principal é:

- `Filme`, com a subclasse estrutural `Documentário` e a classe definida `FilmeFiccional`
- `Pessoa`, com as subclasses `Diretor`, `Ator`, `Produtor` e `Roteirista`. Essas subclasses **não** são disjuntas, pois a mesma pessoa pode acumular papéis. Por exemplo: dirigir e atuar ao mesmo tempo.
- `FilmePremiado`, classe definida (não estrutural) usada para inferência automática.

`Documentário` e `FilmeFiccional` recebem tratamentos diferentes de propósito. `Documentário` é uma classe asserida, pois carrega uma regra especial de cardinalidade. `FilmeFiccional` é uma classe definida como todo filme que não é documentário, o que permite ao Reasoner classificar os indivíduos sozinho.

## 3.2 Propriedades de objeto
As propriedades de objeto ligam indivíduos entre si. A tabela abaixo resumo cada uma com seu domínio, contradomínio e características.
| Propriedade | Domínio | Contradomínio | Características |
| --- | --- | --- | --- |
| temDiretor | Filme | Diretor | |
| temAtor | Filme | Ator | |
| temProdutor | Filme | Produtor |
| temRoteirista | Filme | Roteirista |
| temGênero | Filme | Gênero |
| temNacionalidade | Filme | País |
| temIdiomaOriginal | Filme | Idioma | Funcional |
| ganhouPremio | Filme | Premio |
| premioConcedidoEm | Premio | Evento |
| prefereGênero | Usuário | Gênero |
| prefereAtor | Usuário | Ator |
| feitaPor | Avaliação | Usuário | Funcional |
| sobreFilme | Avaliação | Usuário | Funcional |
| fezAvaliação | Usuário | Avaliação | Inversa de feitaPor |

## 3.3 Propriedades de dados.
As propriedades de dados associam indivíduos a valores literais.

| Propriedade | Domínio | Tipo | Observação |
| --- | --- | --- | --- |
| tituloOriginal | Filme | String | Funcional |
| tituloPortuguês | Filme | String | 
| anoProdução | Filme | Integer | 
| anoLançaamento | Filme | Integer |
| nome | Pessoa ou Usuário | String | Domínio em união |
| idade | Usuário | Integer |
| email | Usuário | String |
| whatsapp | Usuário | String |
| notaEstrelas | Avaliação | Integer | 

## 3.4 Reificação da avaliação

A afirmação "um usuário deu N estrelas a um filme" é uma relação ternária, pois envolve três elementos: o **usuário**, o **filme** e o **valor da nota**. A OWL não oferece propriedades com valor qualificado, então a relação foi reificada na classe `Avaliação`.  Cada instância de `Avaliação` se liga ao usuário por `feitaPor`, ao filme por `sobreFilme`, e carrega a nota em `notaEstrelas`. As três propriedades de ligação são funcionais, garantindo que uma avaliação pertença a exatamente um usuário, a um filme e a uma nota.

## 3.5 Axiomas e restrições

Os axiomas a seguir dão semântica formal a ontologia e habilitam o raciocínio automático:
1. Todo `Filme` tem ao menos um `Diretor`, expresso por cardinalidade mínima qualificada sobre `temDiretor`
2. Todo `FilmeFiccional` tem ao menos um `Ator`. Como `Documentário` não é ficcional, a exceção do enunciado, segundo a qual documentários incluem apenas o diretor, fica satisfeita sem uma contra