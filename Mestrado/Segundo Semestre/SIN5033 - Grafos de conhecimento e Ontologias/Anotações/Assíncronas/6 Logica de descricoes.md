# 1. Por que não usar LPO direto para ontologias?

A LPO é poderosa demais para esse fim: 
- Semi-decidível (o motor de prova pode não terminar);
- Ela é verbosa para a modelagem, e também não é uma linguagem de marcação web (web markup language).

A solução foi pegar um **fragmento** da LPO que seja decidível e expressivo o suficiente: são as **Lógicas de Descrição**.

# 2. Algoritmo Tableaux

O motor de raciocínio automático central da aula. 

A ideia é sempre a mesma: prova por refutação. Ou seja, você nega a conclusão que você quer provar e tenta derivar uma contradição ($\perp$) disso. 

## Regras básicas:
| Tipo | Fórmula | Resultado |
| --- | --- | --- |
| $\alpha$ (conjuntiva) | $x \land y$ | Adiciona $x$ e $y$ no mesmo caminho. |
| $\beta$ (disjuntiva) | $x \lor y$ | Bifurca o caminho em $x$ ou em $y$ |

Um caminho é **fechado** quando contém $x$ e $\neg x$. Se **todos os caminhos fecham**, a fórmula original é provada (a negação dela é contraditória).

**Exemplo 1**:
1. Nega a fórmula $\to$ aplica regras $\alpha$ sucessivamente.
2. Obtém $q$, $r$, $q$ e $\neg r$ no mesmo caminho.
3. $r$ e $\neg r$ $\to$ contradição $\to$ tableaux fechado $\to$ fórmula válida $\checkmark$

**Extensão** para LPO acrescenta duas regras:
1. $\gamma$ (universal $\forall$): substitui a variável por qualquer termo $t$;
2. $\delta$ (existencial $\exists$): introduz uma nova constante $c$

# 3. Por que não usar LPO pura para a Web Semântica

É por que ela é semi-decidível, ou seja, um algoritmo pode ficar rodando pra sempre sem nunca chegar no final e chegar a nenhuma conclusão. Nós precisamos de um **fim da execução garantido**, o que leva a gente para às **Lógicas de Descrição** (LDs).

# Lógicas de Descrição (LD)

Lógicas de descrição são fragmentos decidíveis da LPO. Cada LD é uma "família" com diferentes poderes de se expressar.

A Lógica de Descrição mais básica é a ALC (Attribute Language with Complements)

| Componente | O que guarda | Exemplo |
| --- | --- | --- |
| TBox | Conhecimento terminológico (classes/conceitos) | $\text{escritor} \equiv \text{pessoa} \hat \text{autor} \text{Livro}$


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
.
