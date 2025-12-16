# Prova 2025
## Exercício 1:
a) Discuta o impacto da **dimensionalidade** do espaço de atributos no desempenho de modelos lineares para regressão e classificação, incluindo o problema de **multicolinearidade**. Como a alta dimensionalidade pode afetar o **viés** e a **variância** do modelo?

R: A dimensionalidade é a quantidade de atributos (features) usados pra representar os dados. Ela influencia muito modelos linears, pois quando aumentamos o números de atributos, o modelo consegue capturar mais relações nesses dados, e logo tende a reduzir o viés. Por exeplo, um modelo regressivo que tem acesso à idade, renda e escolaridade pode conseguir extrair mais relações do que um que só tem acesso à idade.

O problema é que conforme o númeor de atributos aumenta, também corremos os risco de termos atributos redundantes (que descrevem a mesma coisa, mas de formas diferentes), como por exemplo, idade em mêses e idade em anos. Isso pode deixar o modelo mais instável. Isso é o problema da multicolinearidade.