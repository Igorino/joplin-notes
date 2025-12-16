# Prova 2025
## Exercício 1:
a) Discuta o impacto da **dimensionalidade** do espaço de atributos no desempenho de modelos lineares para regressão e classificação, incluindo o problema de **multicolinearidade**. Como a alta dimensionalidade pode afetar o **viés** e a **variância** do modelo?

R: A dimensionalidade é a quantidade de atributos (features) usados pra representar os dados. Ela influencia muito modelos linears, pois quando aumentamos o números de atributos, o modelo consegue capturar mais relações nesses dados, e logo tende a reduzir o viés (que é a tendência do modelo de cometer erros baseados em presunções erradas vindas de um dataset com esse tipo de fenomeno) um tipo de . Por exemplo, um modelo regressivo que tem acesso à idade, renda e escolaridade pode conseguir extrair mais relações do que um que só tem acesso à idade.

O problema é que conforme o númeor de atributos aumenta, também corremos os risco de termos atributos redundantes (que descrevem coisas muito parecidas), como por exemplo, idade em mêses e idade em anos, ou peso e altura, o que  pode deixar o modelo mais instável. Esse é o problema da multicolinearidade.

Por outro lado, quanto mais features temos, maior tende a ser a variância, já que o ruído dos dados começam a afetar significativamente o modelo na hora do treino. Por exemplo, se treinarmos um modelo com poucas amostrar mas com muitas medições médicas, o ruído começa a aumentar em proporção aos dados úteis, o que faz o modelo generalize mal fora dos testes.

- c) Discuta em quais cenários **modelos lineares** continuam sendo competitivos, mesmo usando comparados a **modelos não lineares** mais complexos. Em quais situações os modelos lineares podem ser mais vantajosos, apesar das limitações de não modelar não-
linearidades?

O modelos lineares continuam sendo competitivos exatamente quando a relação entre atributo e saída é aproximadamente linear. Nesses casos, modelos mais complexos podem aprender padrões que não são relevantes ao que queremos. Além do fato de que modelos linears, pelo fato de serem mais simples, são mais fáceis de interpretar e treinar do que modelos, bem, mais complexos.