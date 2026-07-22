# Script de Fala — Slide a Slide (versão despojada)
*~35-40 min com a demo. Os tempos são chute calibrado, ajusta no ensaio.*

---

## Slide 1 — Título (30s)

Bom, gente, boa tarde! Hoje eu vou apresentar esse artigo aqui desse cara: o Lapeyrade, que é de 2022. O título já fala: raciocínio com ontologias pra tomada de decisão de NPCs. Ou seja, é literalmente o conteúdo da nossa disciplina, só que aplicado num lugar que ninguém espera: videogame. E esse `?- decidir(npc, Acao).`  é uma consulta do Prolog. A ideia do artigo é basicamente essa: e se o cérebro do NPC fosse uma consulta?

## Slide 2 — O Problema (2 min)

Antes de qualquer coisa, eu queria que vocês pensassem num NPC burro que já viram. Todo mundo tem um. Aquele guarda que te viu roubando, você se esconde atrás de uma caixa por dez segundos, e ele fala "ah, deve ter sido o vento". Ou o NPC que repete a mesma frase pra sempre. Então, o problema que o artigo ataca é esse: NPC tem decisão pouco crível, comportamento repetitivo, ação inconsistente. E isso não é só em jogo comercial, vale pra jogo educacional, jogo sério, simulação.

E aí vem a pergunta que guia a apresentação inteira, que eu acho genuinamente boa: lógica é uma das áreas mais maduras da IA. Por que nenhum NPC raciocina? A gente passa o semestre inteiro estudando inferência, e a indústria de games simplesmente... não usa. Por quê?

## Slide 3 — Por que a Indústria Simplifica? (2-3 min)

O artigo dá três respostas, e elas são importantes porque qualquer proposta nova precisa responder às três, não adianta só ser "mais inteligente".

Primeira: recurso. Desenvolvimento de jogo é prazo apertado, crunch time, pressão pra reusar código. Inovação em IA é a última prioridade da fila.

Segunda, e essa é mais sutil: controle. O designer QUER limitar o que pode acontecer. Um algoritmo que gera muitos comportamentos complexos também gera comportamentos que ninguém pediu, tipo bug, quebra de fluxo da história. Previsibilidade é feature, não limitação.

Terceira: às vezes simples é melhor mesmo. Tem um conceito do Millington chamado complexity fallacy: um NPC pode parecer super inteligente rodando um algoritmo trivial, e vice-versa. E o objetivo do NPC nunca foi ser ótimo, é ser divertido. Ninguém quer jogar contra uma IA perfeita.

Guardem esses três, porque eles voltam lá no final. Duas vezes, na verdade.

## Slide 4 — Como se Decide Hoje (1-2 min)

Tá, e como a indústria faz hoje? Quatro técnicas dominam. FSM, máquinas de estado. Behaviour trees, que é o padrão atual, Unity e Unreal têm editor visual pra isso. Utility AI, que dá nota pra cada ação possível. E planejamento, tipo GOAP. Eu vou detalhar as duas das pontas nos próximos slides porque elas importam pra comparação. Mas o spoiler é: todas falham em algum eixo, e nenhuma, nenhuma delas, usa raciocínio lógico. Essa é a lacuna do artigo.

## Slide 5 — FSM (2 min)

FSM é a mais antiga e a mais intuitiva. Cada comportamento é um modo: patrulhar, atacar, fugir. E eventos trocam o modo: viu inimigo, sai de patrulhar e vai pra atacar. Vida baixa, foge. Ficou seguro, volta a patrulhar. O NPC tá sempre em exatamente um estado, o que é barato de rodar e, principalmente, previsível, o que o designer ama, lembra do slide anterior.

O problema é matemático: com n estados, você pode precisar de até n ao quadrado transições, todas escritas à mão. Quer adicionar um estado "pedir reforço"? Agora vai lá e pensa na transição dele com cada um dos outros. Escala muito mal.

## Slide 6 — GOAP (2 min)

GOAP é bem mais esperto. Em vez de estados, você declara um objetivo, um estado-alvo do mundo, tipo "baú aberto". E declara ações com pré-condições e efeitos: "abrir o baú" exige ter a chave, "pegar a chave" exige estar na torre. Aí um planejador, geralmente um A*, encadeia essas ações ligando o mundo atual ao objetivo. Olha a cadeia aqui do lado: torre, chave, baú. Ninguém escreveu essa sequência, o planejador montou.

Curiosidade: GOAP ficou famoso com F.E.A.R., em 2005, e os inimigos daquele jogo são elogiados até hoje. Então planejamento funciona em jogo, tá provado. O custo é que toda vez que o mundo muda, replaneja, e isso pesa em tempo real.

Ah, e guardem essa imagem da cadeia, porque ela vai voltar. É proposital.

## Slide 7 — FSM × GOAP × Reasoner (2 min)

Botando os três lado a lado, dá pra ver uma escada. FSM: tudo à mão, autoria total, emergência zero. GOAP: já monta planos sozinho, mas o mundo dele é uma lista plana de fatos, não tem estrutura de conhecimento. E o reasoner, que é a proposta do artigo, planeja E infere sobre uma ontologia. Uma regra escrita sobre "arma" vale automaticamente pra toda arma que existir, pra toda arma que você criar semestre que vem.

E aqui embaixo tá o resumo do artigo em uma linha: a sacada é reciclar o motor de prova como planejador. Planejamento de graça. Como assim de graça? Próximo slide.

## Slide 8 — A Sacada: a Prova é o Plano (2-3 min)

Deixa eu ser honesto: quando eu li isso pela primeira vez, minha reação foi "isso é meio gambiarra, né?". Pegar um provador de teoremas dos anos 70 e enfiar de cérebro de NPC. Mas olha como funciona, que a gambiarra é elegante.

A consulta do NPC é uma meta: "como abro o baú?". O backward chaining, que a gente conhece, decompõe essa meta em submetas até chegar em ações concretas. E aí vem o pulo do gato: a sequência de passos que fecha a prova É a sequência de ações do NPC. A prova é o plano. Ninguém escreveu um planejador, ele veio de brinde do mecanismo de inferência.

E tem um bônus enorme: explicabilidade. Cada decisão carrega a própria justificativa, que é a prova. Isso conecta direto com XAI, que tá na ementa. Uma rede neural não te explica por que atacou; uma prova, sim.

E o artigo ainda dá o contraponto pra quem achou gambiarra, citando o Jackson: sistema especialista emula a decisão de um especialista humano. E emular um "especialista", um personagem que sabe o papel dele no mundo... é literalmente o trabalho de um NPC. Então talvez não seja gambiarra, talvez seja a tecnologia voltando pra casa.

## Slide 9 — A Proposta do Artigo (2 min)

Formalizando, a proposta tem três pilares. Um: reasoner lógico, Prolog no caso, como cérebro do NPC. O argumento é que designer já pensa o jogo em regras quase lógicas, "se o jogador tem a chave, o baú abre", então por que não escrever isso COMO lógica? Dois: ontologias hierárquicas e modulares, que dão conhecimento genérico e reutilizável, e isso responde a restrição de recursos lá do slide 3, dá pra reaproveitar entre jogos. Três: planejamento por backward chaining, que a gente acabou de ver, e que gera comportamento emergente mas sempre dentro das regras declaradas, o que responde a restrição de controle do designer. Viu? Os três problemas do slide 3, cada um com uma resposta.

## Slide 10 — Relembrando: Prolog (1-2 min)

Isso aqui é só pra reativar o vocabulário, porque o professor já cobriu Prolog com a gente. Fatos são o mundo do jogo: `em(chave, torre)`. Regras são o design do jogo. E a consulta é a decisão do NPC. A busca da prova, que a gente viu como resolução SLD lá na aula de lógica e inferência, é o que daqui a pouco vira planejamento. Só isso, sigo em frente.

## Slide 11 — Ontologias Hierárquicas (2-3 min)

Agora, atenção nesse slide, porque tem uma pegadinha terminológica que eu preciso destacar, senão o professor destaca por mim, haha.

A "ontologia" do artigo é isso aqui: espada é arma, arma é objeto. Hierarquia de conceitos com herança, e regra escrita sobre "arma" vale pra toda arma, presente e futura. Organizada em módulos com partes públicas e privadas, tipo encapsulamento de OOP.

Só que... isso NÃO é uma ontologia OWL/DL como as que a gente estuda. Não tem semântica formal de lógica de descrições, não tem interoperabilidade RDF, não roda num reasoner de DL, não abre no Protégé. É uma hierarquia de predicados Prolog usando a palavra "ontologia" no sentido fraco, de vocabulário estruturado. Isso não invalida a proposta, mas é uma diferença conceitual importante pra nossa disciplina, e eu volto nela na crítica.

## Slide 12 — Planejamento, Backward Chaining (2 min)

E aqui o planejamento rodando no exemplo do artigo... e olha a imagem: é a MESMA cadeia do slide do GOAP. Torre, chave, baú. De propósito. A diferença é quem monta: no GOAP, você precisou implementar um planejador A* pra isso. Aqui, você declarou `aberto(bau)` como meta, e o motor busca as subações sozinho, de trás pra frente. Mesma saída, só que o planejador veio de graça.

E o detalhe que reconecta com o slide 3: ninguém programou essa sequência, ela emergiu. Mas ela só pode emergir dentro do que as regras permitem. Emergência contida. O designer continua no controle.

## Slide 13 — O Problema da Negação, CWA (2 min)

Beleza, até aqui tudo lindo. Agora o problema, que é onde o artigo fica realmente interessante.

Prolog é CWA, mundo fechado, com negação por falha: o que não é provável é falso. A gente viu isso no curso. Pra banco de dados, ótimo. Pra NPC, é um desastre sutil: o NPC não distingue "eu sei que é falso" de "eu não sei". O guarda que nunca ouviu falar do dragão conclui que o dragão não existe. E pior, em Prolog puro você nem consegue afirmar fatos falsos explicitamente.

Pra um agente que deveria parecer crível, ignorância e falsidade serem a mesma coisa é um problema de credibilidade. Como resolver?

## Slide 14 — WFS: o 3º Valor de Verdade (3 min)

Essa é a contribuição central do artigo, então capricho aqui.

Existem duas grandes semânticas pra negação em programação em lógica. A Stable Model Semantics, que é a base do ASP, permite negação explícita, mas pode gerar múltiplos modelos pra mesma consulta. E jogo precisa de UMA resposta, o guarda não pode agir em dois universos paralelos. A outra é a Well-Founded Semantics, que gera um modelo único e introduz um terceiro valor de verdade: indefinido.

E a sacada do artigo é usar esse indefinido pra representar ausência de conhecimento do NPC. Caso de uso perfeito: fontes conflitantes. O taverneiro fala bem do forasteiro, o ferreiro fala mal. Verdadeiro? Falso? Nenhum dos dois: indefinido. E o designer mapeia indefinido pra um comportamento de incerteza: vigiar, investigar, ficar em alerta.

Conectando com o curso: a gente viu regras revogáveis resolvendo conflito com prioridades. A WFS oferece a outra saída, manter o não-sei como estado legítimo. E se lembram da LCWA como meio-termo entre mundo aberto e fechado? A WFS é outro meio-termo, só que no eixo da negação: mundo fechado, mas com espaço pra ignorância.

## Slide 15 — Arquitetura de Integração (1-2 min)

Na prática, como isso entra num jogo: Unity de um lado, SWI-Prolog do outro, uma DLL de interface no meio. O código que fala com Prolog fica isolado num módulo, então o designer usa a interface sabendo o mínimo de Prolog. E o SWI foi escolhido porque tem interface pra C#, da Unity, e C++, da Unreal.

Curiosidade que eu gosto: o Jan Wielemaker, mantenedor do SWI-Prolog, ajudou o autor pessoalmente com a implementação da WFS. O `tnot` que vocês vão ver agora existe por causa disso.

## >>> DEMO AO VIVO (6-7 min) <<<

*[Abre o terminal: `swipl demo_npc.pl`]*

Chega de slide, deixa eu mostrar isso rodando.

**Parte 1, ontologia:** olha a hierarquia: espada, arma, objeto. Pergunto: `e_um(excalibur, objeto).` True. Esse fato não existe em lugar nenhum do arquivo, foi inferido pela cadeia. Regra genérica, serve pra qualquer jogo.

**Parte 2, planejamento:** `plano(aberto(bau_tesouro), P).` E olha o plano: ir na torre, pegar a chave, ir no salão, abrir o baú. Eu não escrevi essa sequência em lugar nenhum. É a prova virando plano, ao vivo.

**Parte 3, o clímax:** o guarda recebe relatos conflitantes sobre o forasteiro. Do orc só falam mal: impostor verdadeiro, decisão atacar. Do aldeão só falam bem: confiável, cumprimentar. E o forasteiro? `verdade(impostor(forasteiro), V).` Indefinido! E a decisão: vigiar. O terceiro valor de verdade virou comportamento de incerteza. Isso é o artigo inteiro rodando em vinte linhas.

*[Se algo der errado: `?- demo.` roda tudo de uma vez. Respira.]*

## Slide 16 — Análise Crítica e Conclusão (2-3 min)

Agora tirando o chapéu de vendedor e botando o de cientista.

Limitação principal: é um artigo de proposta, sem validação empírica. O protótipo era trabalho em andamento, o teste com estúdio comercial era futuro. As dúvidas que o próprio autor admite: desempenho em tempo real com vários NPCs, planos longos, consumo de recursos, e a barreira de adoção, porque ferramentas declarativas amigáveis existem e nem por isso pegaram.

E a minha crítica, da perspectiva desta disciplina: as ontologias são hierarquias Prolog, sem a semântica formal e o ferramental do nosso ecossistema. Usar OWL de verdade seria uma extensão natural, ganharia mundo aberto nativo, mas pagaria caro em raciocínio.

Dito isso, a força do artigo pra mim é dupla: o diagnóstico honesto de por que a indústria não usa lógica, e a elegância da WFS pra modelar ignorância. E fechando com a pergunta da abertura: hoje todo mundo só fala de LLM pra NPC. Raciocínio simbólico talvez seja o contrapeso: barato, determinístico, auditável. Talvez o futuro seja os dois juntos, LLM no diálogo, lógica na decisão.

## Slide 17 — Bônus: Meu Mestrado em Três Eixos (2 min)

Antes de encerrar, um bônus rápido conectando isso com a minha pesquisa de mestrado, porque a sobreposição é grande demais pra eu ignorar.

Minha pergunta de qualificação: FSM, BT e GOAP no mesmo cenário, como se comparam? E eu comparo em três eixos. Escalabilidade: quanto custa rodar muitos cérebros em tempo real. Autoria: quão controlável e auditável é o comportamento. E emergência: quão crível e não-estereotipado o NPC parece, believability.

E aí... vocês já viram esses três eixos hoje. São exatamente as três razões pelas quais a indústria simplifica, lá do slide 3. O que a indústria trata como restrição prática, eu tô tentando formalizar como eixo de avaliação.

## Slide 18 — Onde o Artigo Toca Minha Pesquisa (2 min)

E o Lapeyrade encosta na minha pesquisa em cheio. Mesmo diagnóstico: as políticas da indústria são meus eixos. E a aposta dele, planos emergentes dentro das regras, é uma afirmação fortíssima pro meu problema: ele tá prometendo emergência sem perder autoria, ou seja, prometendo dissolver exatamente o trade-off que eu estudo. Olha a balança aqui do lado.

Só que é uma promessa sem evidência. E o que falta lá é o que eu faço: avaliação empírica comparativa com métricas. Então a ponte futura é natural: Prolog com WFS como quarta arquitetura candidata no meu framework, ao lado de FSM, BT e GOAP. A crítica ao artigo vira o meu trabalho futuro.

## Slide 19 — Referências (30s)

E é isso! Referências principais aqui: o artigo do Lapeyrade, o paper original da WFS de 91, o livro do Millington que é meio que a bíblia de IA pra jogos, Yannakakis e Togelius, e o trabalho do Calimeri com ASP na Unity, que é o parente mais próximo dessa proposta. Obrigado, gente! Perguntas?

---

### Colas de emergência

- **Estourou o tempo:** corta a fala dos slides 5 e 6 pra 1 min cada (a imagem carrega) e encurta o 17-18 pra 1 min cada.
- **Sobrou tempo:** estende a demo com consultas extras da Parte 1 (`findall` dos personagens) e conta a história do F.E.A.R. com mais calma.
- **Demo quebrou:** `?- demo.` roda tudo. Se nem isso: "a saída esperada tá comentada no código, olha só" e mostra o arquivo. Segue o jogo sem pânico, o conteúdo já foi dado nos slides.
- **Deu branco:** a estrutura é sempre "problema, por que ninguém resolve, a proposta, a parte técnica, a crítica". Se perder, pergunta pra si mesmo em qual desses cinco você tá.