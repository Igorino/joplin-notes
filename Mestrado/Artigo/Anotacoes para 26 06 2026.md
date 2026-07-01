Anotações para a apresentação que explica a SLR do SBGames e que mostra as possíveis lacunas nele.

**Questões apresentadas:**
1. Quais são os critérios necessários para o desenvolvimento de um comportamento crível de NPCs em jogos digitais?
2. Quais são os papéis da IA para elaborar um comportamento crível em jogos digitais?
3. Quais são os critérios que compõem o processo de decisão em jogos digitais para deixar comportamentos mais realistas?
4. Quais são os comportamentos esperados de NPCs em um ambiente virtual de jogos para os deixarem mais realistas?
5. Qual é a relação de comportamento emocional com a tomada de decisão de NPCs em jogos digitais para os deixarem mais convincentes?

Ótimas perguntas, porém: essa revisão foi escrita e publicada em 2021, *antes* do boom das IAs que aconteceu por volta de 2023. Como que eu posso saber se o estado da arte não mudou desde esse tempo?

Aliás, os outros artigos que eu cheguei a ver que foram publicados depois parecem ter coisas mais modernas, como o Echoes of Others, que parece ter trabalhado bem legal o uso de LLMs em jogos.

Mas o Echoes of Others só trabalhou no quesito de diálogo, e só consegue fazer **um por vez**. Não é exatamente o que eu tava pensando quando pensei em trabalhar NPCs no paradigma de multi-agente.

Park et al 2023 conseguiu fazer vários NPCs pequenos fazerem uma simulação de uma vila. Queria saber o quão viável seria isso em um jogo comercial. Mas não sei se isso vai acabar tirando o meu foco inicial de tentar fazer uma análise dos algoritmos mais básicos como FSM, GOAP, etc.

Perguntas feitas pelo Professor Lauretto:
- *a) Quais subáreas estão saturadas e quais estão menos exploradas?*
R: Essas mesmas áreas de algoritmos deterministicos de FSM, GOAP, etc.

- *b) Você vislumbra algum tópico que poderia ser explorado em seu mestrado para uma eventual contribuição incremental? P.ex. extensão de algum método já existente?*
R: Essa comparação de performance entre algoritmos determinísticos e SLMs parece ser legal, e não foi explorada muito ainda (pelo menos não do que eu vi)

- *c) você vislumbra a possibilidade de realizar  comparações de diferentes métodos para um problema específico?*
R: Sim, como como mencionei, a comparação entre determinísticos e de SLMs. Mas eu teria que levar em comparação os quatro aspectos que mencionei antes de: custo, autoria, explicabilidade e emergência.

Não sei se também não seria interessante juntar explicabilidade com autoria, já que o que eu realmente quero saber é se o NPC tá se comportando do jeito que eu espero que ele se comporte quando procuro explicabilidade nesse contexto, então talvez autoria seria mais apropriado.

Daí ficaria custo, autoria e emergência.

Mas como eu definiria emergência? Só como a capacidade de um algoritmo de conseguir exibir comportamentos emergentes? Meio estranho isso. O que eu procuraria com isso nesse contexto seria a capacidade de um alg. conseguir "fakear" complexidade e passar uma **percepção** de inteligência/adaptabilidade para o jogador (inclusive o artigo do SBGames fala exatamente sobre isso, e cita até artigos da área de psicologia, o que eu achei fantástico).

Mas será que eu não tô saindo muito do escopo? Eu acho melhor por enquanto eu só apresentar pros meus orientadores o artigo de SLR do SBGames, daí eu posso no final falar sobre essa minha ideia de multi-agentes. O foda é que eu realmente preciso de um artigo pra avaliação o mais rápido possível. O que eu faço agora? Se eu tentar mudar o escopo mais uma vez, mesmo que pouco, os professores podem se irritar. Acho melhor eu ficar só nesse meu escopo de IAs determinísticas de NPCs, talvez deixando só como um possível trabalho futuro um trabalho usando SLMs para tentar recriar alguma coisa parecida com aquela vila do Park et al.