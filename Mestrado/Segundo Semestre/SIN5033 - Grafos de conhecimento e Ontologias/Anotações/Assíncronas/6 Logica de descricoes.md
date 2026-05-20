# 1. Por que não usar LPO direto para ontologias?

A LPO é poderosa demais para esse fim: 
- Semi-decidível (o motor de prova pode não terminar);
- Ela é verbosa para a modelagem, e também não é uma linguagem de marcação web (web markup language).

A solução foi pegar um **fragmento** da LPO que seja decidível e expressivo o suficiente: são as **Lógicas de Descrição**.

# 2. Algoritmo Tableaux

O motor de raciocínio automático central da aula. 

A ideia é sempre a mesma: prova pro refutação. Você nega a conclusç