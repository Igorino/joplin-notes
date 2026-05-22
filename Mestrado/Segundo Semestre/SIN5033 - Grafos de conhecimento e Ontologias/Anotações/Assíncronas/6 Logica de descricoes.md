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
| TBox | Conhecimento terminológico (classes/conceitos) | $\text{escritor} \equiv \text{pessoa} \sqcap \text{autor} \text{Livro}$ |
| ABox | Conhecimento assertivo (indivíduos) | $\text{Escritor} (\text{GeorgeOrwell})$ , $\text{autor} (1984, \text{GeorgeOrwell})$
| RBox | Hierarquia de papeis (roles) | $\text{coAutor} \sqsubseteq \text{autor}$ |

# 5. Construtores ALC

Os blocos de montagem da linguagem são:

| Construtor | Símbolo | Exemplo legível |
| --- | --- | --- |
| Conjunção | $C \cap D$ | *"É livro **e** Ficção* |
| Disjunção | $C \cup D$ | *"É livro **ou** revista* |
| Negação | $\neg C$ | *"**Não** é poesia"* | 
| Universal | $\forall R.C$ | *"**Todos** os autores são Escritores"* |
| Existencial | $\exists R.C$ | *"**Tem ao menos** um autor que é Pessoa"* | 
| Top/Bottom | $\top \bot$ | *"Tudo / nada"* |

## Inclusão vs. Equivalência:
- $\text{Novela} \sqsubseteq \text{Livro} \to$ toda novela é livro (subclasse)
- $\text{Novela} \equiv \text{Prosa} \to$ novela e prosa são exatamente o mesmo conjunto

## Diferença crucial entre $\forall$ e $\exists$ sobre roles:
- $\text{Livro} \sqsubseteq \forall \text{Autor}.\text{Escritor} \to$ se um livro tem um autor, esse autor **deve** ser escritor.
- $\text{Livro} \sqsubseteq \forall \text{autor Pessoa} \top$ todo livro tem **ao menos um** autor que é Pessoa (restrição aberta)

# 6. Semântica de Modelos ALC
A LD tem significado formal via interpretações $I = (\Delta¹, .¹)$, onde:
- $\Delta¹$ é o domínio (conjunto de indivíduos)
- $.¹$ mapeia nomes de classes para os subconjuntos do domínio, e roles para de elementos.

Isso serve para dar significado preciso às afirmações: $C(a)$ é verdadeiro somente se $a^I \in C^I$.

# 7. Família de LDs e OWL

Cada letra da sopa-de-letrinhas representa uma extensão sobre a ALC

# 8. Problemas de inferência

O que um reasoner pode responder sobre uma BC (Base de Conhecimento):

| Pergunta | Formal |
| --- | --- |
| A $BC$ é consistente? | $BC \models \bot ?$ |
| Classe $C$ é sempre vazia? | $C \equiv \bot ?$ |
| $C$ é subclasse de $D$? | $C \sqsubseteq D ?$ |
| As classes $C$ e $D$ são disjuntas? | $C \sqcap D \models \bot ?$ |
| O indivíduo $a$ pertence a $C$? | $C(a)?$

Todos esses problemas são **reduzidos à insatisfatoriedade**, o reasoner sempre testa se uma contradição existe.

# 9. OWA vs. CWA: Diferença filosófica mais importante

Essa distinção é fundamental para entender o comportamento de ontologias OWL.

**Hipótese do Mundo Aberto (OWA)**, adotada pela Web Semântica:
> *"O que não está declarado é **desconhecido**, não falso.*

**Hi**
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
