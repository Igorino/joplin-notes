

# Informações iniciais:
- *Development of Non-Player Character with Believable Behavior: a systematic literature review*
- Autores: Guilherme Alves da Silva e Marcos Wagner de Souza Ribeiro (Da UFJ)
- Publicado em 2021
- É uma revisão sistemática da literatura, não um experimento
- Mapeia o estado da arte, nomeando 18 estudos que foram selecionados a partir de determinados critério, propostos por Kitchenham

# Problema central: NPCs
- NPC significa "Non-Player Character", ou Personagens Não-jogáveis, e o termo veio de RPGs de mesa como Dungeons & Dragons.
- NPCs básicamente tentam simular o comportamento de outros agentes (que não são controlados por seres humanos) dentro do ambiente virtual
- Também são meio burros kk
- Nem sempre tem o comportamento apropriado ou responsivo
- Quando uma decisão é "Mais artifical do que inteligente", a qualidade da experiência cai
- A indústria não dá muito tempo/recurso pra elaborar conjuntos de regras complexos
- E também acaba insistindo em uma abordagem de reutilizar modelos anteriores
- Daí a tese: deveria ser valorizada as técnicas **fáceis de implementar**, de **baixo custo computacional**, e que garantam um "**controle firme**" sobre as saídas (pra evitar outputs inesperado pelos designers)

# Metodologia que foi usada
- Seguem Kitchenham, esturturando as perguntas pela lógica PICOC: **P**opulação, **I**ntervenção, **C**omparação, **O**utcome (Resultado) e **C**ontexto
- Pegaram artigos de: ACM Digital Library, CAPES, IEEE Xplore, Elsevier. E também conferências como: COF, ICAART, GAME-ON e SBGames.
- Pegaram artigos de 2015 à 2021, do português e inglês
- String de busca (essência): NPC **E** Inteligência Artificial **E** jogo **E** tomada de decisão **E** comportamento
- Excluíram pathfinding (não é tão relevante), geração procedural de conteúdo e "Serious Games"
- Resultado: Acharam 18 trabalhos que passaram nessa triagem

# As 5 perguntas:
### 1. Quais são os critérios necessários para o **desenvolvimento de um comportamento crível** de NPCs em jogos digitais? (9 respostas):
R: Credibilidade vem de requisitos que fazem o jogador "acreditar" no personagem.


### 2. Quais são os **papéis da IA** para elaborar um comportamento crível em jogos digitais? (6 respostas, tema geralmente implícito):
R: Comportamento modelado por regras predeterminadas em algoritmos de busca. Modelagem deveria ser acessível a programadores e designers, fácil de testar, controlar e alterar.

### 3. Quais são os critérios que compõem o **processo de decisão** em jogos digitais para deixar comportamentos mais realistas? (13 respostas)
R: Decisão como estrutura hierárquica que mapeia comportamento em nós. Escolhas influenciadas por fatores externos (ambiente, preferência de ação, recompensa/punição, influência emocional).
O gênero do jogo importa: RPGs teriam comportamentos diferentes de um Shooter.

### 4. Quais são os **comportamentos esperados** de NPCs em um ambiente virtual de jogos para os deixarem mais realistas? (8 respostas)
R: NPCs invencíveis ou previsíveis demais frusta o jogador. Previsibilidade só é tolerada em ambientes com regras bem fixas e rígidas. Gera o grupo de **comportamento esperado**: perspectiva do jogador, nível de desafio e nível de previsibilidade.

### 5. Qual é a relação de **comportamento emocional** com a **tomada de decisão** de NPCs em jogos digitais para os deixarem **mais convincentes**? (7 respostas)
R: Antes se achava que a emoção podia atrapalhar a lógica, mas inteligência emocional torna o NPC mais convincente. Medo leva a decisões simples e deseperadoras. 

# Conclusão:
- Adoção de técnicas tradicionais pela indústria pode ser o maior obstáculo pra um comportamento mais crível.
- Motivo: conforme os critérios de engajamento ficam mais complexos, o designer perde o controle das respostas possíveis. Ainda mais quando a modelagem foge do papel do designer e exige que o desenvolvedor mexa direto nos algoritmos.
- Trabalho futuro deles: aplicar a taxonomia pra achar frameworks ou engines que são mais adequados e avaliar com métricas e **questionários com jogadores**.

# Pontos de contato
- "Controle Firme" e "Autoria acessível" são meu eixo de contrabilidade e autoria
- A psicologia suporta o uso da percepção nessa análise (Affective computing, efeito da emoção no julgamento)
- Janela de artigos somente até 2021: nada de LLMs, SLMs, Redes Neurais, agentes generativos, etc. Pode ser que hoje essas abordagens sejam mais efetivas ou viáveis.

# Perguntas feitas pelo Professor Lauretto:
- *a) Quais subáreas estão saturadas e quais estão menos exploradas?*
R: Essas mesmas áreas de algoritmos deterministicos de FSM, BT, GOAP, etc.

- *b) Você vislumbra algum tópico que poderia ser explorado em seu mestrado para uma eventual contribuição incremental? P.ex. extensão de algum método já existente?*
R: Essa comparação de performance entre algoritmos determinísticos e SLMs parece ser legal, e não foi explorada muito ainda (pelo menos não do que eu vi)

- *c) você vislumbra a possibilidade de realizar  comparações de diferentes métodos para um problema específico?*
R: Sim, como como mencionei, a comparação entre determinísticos e de SLMs. Mas eu teria que levar em comparação os quatro aspectos que mencionei antes de: custo, autoria, explicabilidade e emergência.





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
.
.
.
.
