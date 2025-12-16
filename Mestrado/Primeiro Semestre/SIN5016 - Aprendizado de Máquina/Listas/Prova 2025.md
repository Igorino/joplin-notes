# Prova 2025
## Exercício 1:
**a)** A dimensionalidade é a quantidade de atributos (features) usados pra representar os dados. Ela influencia muito modelos linears, pois quando aumentamos o números de atributos, o modelo consegue capturar mais relações nesses dados, e logo tende a reduzir o viés (que é a tendência do modelo de cometer erros baseados em presunções erradas vindas de um dataset com esse tipo de fenomeno) um tipo de . Por exemplo, um modelo regressivo que tem acesso à idade, renda e escolaridade pode conseguir extrair mais relações do que um que só tem acesso à idade.

O problema é que conforme o númeor de atributos aumenta, também corremos os risco de termos atributos redundantes (que descrevem coisas muito parecidas), como por exemplo, idade em mêses e idade em anos, ou peso e altura, o que  pode deixar o modelo mais instável. Esse é o problema da multicolinearidade.

Por outro lado, quanto mais features temos, maior tende a ser a variância, já que o ruído dos dados começam a afetar significativamente o modelo na hora do treino. Por exemplo, se treinarmos um modelo com poucas amostrar mas com muitas medições médicas, o ruído começa a aumentar em proporção aos dados úteis, o que faz o modelo generalize mal fora dos testes.

.

**c)** O modelos lineares continuam sendo competitivos exatamente quando a relação entre atributo e saída é aproximadamente linear. Nesses casos, modelos mais complexos podem aprender padrões que não são relevantes ao que queremos. Além do fato de que modelos linears, pelo fato de serem mais simples, são mais fáceis de interpretar e treinar do que modelos, bem, mais complexos.

.

**d)** Como dito anteriormente, modelos lineares são mais simples de interpretar do que modelos mais complexos: é mais fácil ver aumentos e diminuições na progressão dos dados, e prever esses mesmos para dados que ainda não temos. 

Além disso, costumam serem treinados mais rapidamente, usam menos memória e precisam de menos dados do que modelos mais complexos.Logo, esses tipos de modelos são populares para análises econômicas, investimentos, e estudos médicos que tentam relacionar fatores de risco a diagnósticos. 

---
## Exercício 2:

**a)** Começa avaliando, em cada nó da árvore, qual é o atributo que separa melhor os dados em grupos menos "misturados". O algoritmo testa possíveis divisões e escolhe a que organiza melhor os exemplos, e vai repetindo esse processo até chegar no critério de parada definido, usando como base métricas como entropia e ganho de informação para ver o quão "misturados" estão os dados, e fazendo as divisões com base neles.

.

**d)** Modelos lineares mostram o peso de cada atributo, enquanto árvores explicam decisões por meio de regras simples do tipo "se, então", logo, os dois conseguem ser interpretáveis para seu tipo de análise.
Modelos lineares obviamente não conseguem modelar não-linearidades, enquanto árvores conseguem.
Modelos lineares, como discutido anteriormente, são mais robustos à ruídos dado sua simplicidade, o que não é o caso de árvores.
Árvores de decisão são preferíveis quando o prroblema envolve relações não-lineares, combinações específicas de atributos, ou quando explicações baseadas em regras claras são mais úteis.

.

**e)** Os critérios de impureza influenciam diretamente como a árvore escolhe a divisões e a sua estrutura final.
Entropia tende a busca divisões mais "puras", mesmo que desbalanceadas, sendo útil quando separar bem classes é importante. 
O Índice Gini é o mais simples e rápido, gerando árvores semelhantes, mas com menor custo computacional.
O erro de classificação é o menos sensível a pequenas melhorias, e costuma ser mais adequado pra decisçoes mais grossas (ou para poda)

---

## Exercício 3:

**a)** Ela pode ser mais eficiente do que a largura já permite representar funções complexas de forma hierárquica (combinando transformações simples em vários níveis) em vez de tentar aprender tudo de uma vez. Algumas funções que exigiriam um número gigantesco de neurônios em uma camada rasa, podem ser representadas com muito menos parâmetros usando várias camadas menores (já que cada camada reaproveita e refina os padrões aprendidos anteriormente). 

Isso leva a arquiteturas mais compactas, com melhor generalização e menor custo. Também motiva o uso de redes profundas, que exploram estrutura, composição e reutilização de características ao longo das camadas.

.

**b)** O dropout remove aleatoriamente neurônios da rede a cada passo, criando várias versões diferentes do mesmo modelo. Então, o aprendizado acontece como se múltiplos modelos estivessem sendo treinados ao mesmo tempo, usando os mesmos parâmetros. Isso reduz a dependência excessiva entre os neurônios e ajuda a ter representações mais gerais, o que reduz overfitting. 

.

**e)** A inicialização dos pesos deve ser compatível com a função de ativação para evitar um aprendizado lento ou instável. Uma inicialização correta mantém o fluxo de informação estável entre as camadas. Por exemplo: com sigmoide, pesos grandes causam saturação; com ReLU, uma má inicialização pode fazer neurônios pararem de aprender

---

## Exercício 4:

**a)** Mistura de especialistas é mais adequada para dados heterogêneos ou multimodais porque permite que diferentes modelos se especializem em partes específicas dos dados (em vez de tentar aprender tudo ao mesmo tempo). Escolhe-se um epecialista para cada entrada, o que é útil quando os dados vem de fontes ou padrões diferentes.
Ensembles tradicionais combinan modelos de forma fixa, sem essa adaptação ao tipo de entrada.

.

**b)** Uma combinação de múltiplos modelos tende a ter melhor desempenho porque diferentes modelos cometem erros diferentes. Juntar esses modelos ajuda a reduzir esses erros individuais, um compensando pela falha do outro, o que gera resultado melhor, mais estável no final.

.

**c)** Mistura de especialistas podem ter dificuldades em convergir para uma resposta porque o mecanismo de roteamento pode acabar favorecendo os mesmos especialistas, enquanto os oturos quase não aprendem.Para lidar com isso e evitar o risco de sobreajuste, podemos usar técnicas que incentivam o uso equilibrado de especialistas, aplicar regularização e/ou limitar a complexidade de cada modelo, o que garante que todos aprendam e generalizem melhor.

---

## Exercício 5: 

**b)** O parâmetro C controla o quanto o modelo penaliza os erros de classificação em relação ao tamanho da margem. 
Valores altos fazem o modelo tentar classificar corretamente quase todos os exemplos de treino, o que resulta em uma margem menor e maior risco de sobreajuste. 
Valores baixos permitem mais erros no treino, mas produzem uma margem maior, o que tende a melhorar a generalização.

.

**d)** Esparcidade se refere a quanto o modelo depende de poucos elementos para fazer uma previsão. A LSVM tende a ser mais esparsa, pois a predição usa apenas um vetor de pesos. Já a SVM kernelizada depende de vários vetores, o que reduz a esparsidade, e faz com que a LSVM seja a mais rápida e eficiente.

.

**e)** A margem é a distância entre a fronteira de decisão e os pontos mais próximos das classes. Maximizar ela significa separar os dados com mais espaço entre eles, o que torna o modelo mais robusto a ruídos. Isso ajuda a melhorar a generalização.

---

## Exercício 6:

**c)** Isso acontece porque o domínio das imagens naturais é muito diferente do que as de sensoriamento remoto. Imagens de satélite tem outra escala, outro ponto de vista, resuoluções distintas, etc. As características aprendidas no pré-treinamento não se adaptam tão bem à esse caso de uso.

**d)** O pooling causa perda de informação porque reduz uma região da imagem a um único valor, e joga fora detalhes. Quando aplicado várias vezes, ele diminui a resolução espacial e elimina 