# Princípio 1 - "Alfabeto"do ALC (Attribute Language with Complements)
São cinco construtores pra montar *classes* (conceitos):
1. $\neg C$ - Negação ("**Não** é $C$");
2. $C \sqcap D$ - Conjunção ("É $C$ **e** $D$");
3. $C \sqcup D$ - Disjunção ("É $C$ **ou** $D$")
4. $\exists R.C$ - Restrição existencial ("tem **algum** $R$ que é $C$")
5. $\forall R.C$ - Restrição de valor ("**todos** os $R$ são $C$")

E dois "conectores" entre as classes, no nível dos Axiomas (a TBox):
- $C \sqsubseteq D$ - Inclusão ("todo $C$ é $D$"). Em LPO vira $\forall x (C(x) \rarr D(x))$
- $C \equiv D$ - Equivalência ("$C$ é exatamente $D$", os dois lados) $\rarr$ dá pra reescrever como "$C \sqsubseteq D$ e $D \sqsubseteq C$"

Pegadinha: $\exists \text{vs.} \forall$:
- Palavras como *"algum, um pelo menus um, tem"* $\rarr \exists$
- Palavras como *"só, apenas, somente, todos"* $\rarr \forall$

Resolve a Q7 da Lista 1 (*"gerenciada por alguém* = $\exists \text{gerente.Pessoa}$) e o item iii da Lista 2 (*"dona **só** de gatos"* = $\forall \text{donoDe.Gato}$).

# Principio 2 - Traduzir do português -> Lógica de Descrição
Receita:
1. **Sujeito** = conceito à esquerda do $\sqsubseteq$;
2. Decida se é uma *definição* ($\equiv$, quando diz "são **exatamente**...") ou só *inclusão* ($\sqsubseteq$, quando diz "são/têm...");
3. Cada verbo relacional ("tem parte", "é movido por") vira um **role** dentro de um $\exists$ ou $\forall$, conforme o gatilho acima.

Exemplo da lista 2: *"Carros são exatamente aqueles veículos que têm rodas e são movidos por um motor*" vira $\text{Carro} \equiv \text{Veículo} \sqcap \exists \text{temParte.Roda} \sqcap \exists \text{movidoPor.Motor}$

# Princípio 3 - Forma Normal Negada (NNF)

Antes de rodas o tableaux, a negação precisa ficar **só na frente de conceitos atômicos**. É como distribuir o sinal de menos na álgebra. As regras são as leis de De Morgan mais os quantificadores:
- $\neg (C \sqcap D) \rarr \neg C \sqcup \neg D$
	- (O único jeito de "C e D" ser falso é se C for falso, ou se D for falso)
- $\neg (C \sqcup D) \rarr \neg C \sqcap \neg D$
	- (O único jeito de "C ou D" for falso é se C e D forem falsos ao mesmo tempo)
- $\neg \exists R.C \rarr \forall R.\neg C$
	- (O único jeito de "existe um R tal que C" ser falso é se "pra todo R, C é falso")
- $\neg \forall R.C \rarr \exists R. \neg C$
	- (O único jeito de "Para todo R tal qual C" for falso, basta "Existir pelo menos um R onde C é falso")
- $\neg \neg C \rarr C$
	- (Cancelamento de negações kk)

(A Q11 é literalmente só aplicar isso kk)

Aliás:
$C \sqsubseteq D$ primeiro vira $\neg C \sqcup D$ e só depois aplica a NNF

# Princípio 4 - Tableaux é o "Abogado del Cartel" kkkkkkkk
Basicamente o coração da coisa e responde as Q1, Q3, Q8, e Q12 da Lista 1 e a Q3 da Lista 2. 

A ideia é a **prova por refutação/absurdo**: assume o contrário e tenta chegar numa contradição/absurdo.

Constrói uma árvore. Cada regra ou **estende o mesmo ramo** (regras $\alpha$, conjuntivas $X \sqcap Y$ te obriga a colocar $X$ **e** $Y$) ou **abre dois ramos** (regras $\beta$, disjuntivas: $X \sqcup Y$ cria um ramo com $X$ e outro com $Y$).

Para os roles:
- $\exists R.C(a)$: crie um *indivíduo novo*, com $R(a, z)$ e $C(z)$.
- $\forall R.C(a)$: pra todo $z$ que já tem $R(a, z)$, adicione $C(z)$.

Um ramo **fecha** quando aparecem $X$ e $\neg X$ juntos (uma contradição). Aí:
- Se **todos** os ramos fecham -> o conceito é **insatisfazível** (a BC original é inconsistente)
- Se sobra **um** ramo aberto e sem regras a aplicar -> é **satisfazível** (achou um modelo)

O truque que unifica tudo: perguntas sobre **equivalência** (Q8) ou **consequência lógica** (Q12) viram uma pergunta de Satisfazibilidade. 

Por ex.: pra provar $C \equiv D$, você testa se $(C \sqcap \neg D)$ e $(\neg C \sqcap D)$ são *ambos* insatisfazíveis.

# Princípio 5 - Mundo Aberto (OWA) vs. Mundo Fechado (CWA)
Isso decide as questões 9 e 10. A diferença é que a máquina responde diante do desconhecido:
- **CWA (Closed World Assumption)**: "o que eu não consigo provar como verdadeiro é **falso**". Como por exemplo: um bando de dados.
- **OWA (Open World Assumption)**: é o padrão das DLs/OWL: "pode haver coisas que eu simplesmente **não sei**". Diante do desconhecido, a resposta é "unknown", não um "falso".

# Exemplo resolvido da Lista - Satisfazibilidade via tableaux

> "$A \sqcap \exists r.B \sqcap \forall r. \neg B$" é satisfazível?

## 0. Checar NNF:

As negações já tão só na frente de átomos ($\neg B$)

---
## 1. Assumir o conceito num indivíduo

Chamo de $a$ e afirmo que ele pertence ao conceito:

$(A \sqcap \exists r.B \sqcap \forall r. \neg B) (a)$

---
## 2. Regra $\sqcap(a)$

A conjunção me obriga a colocar as três partes no mesmo ramo:

$A(a)$
$(\exists r.B)(a)$
$(\forall r. \neg B)(a)$

---
## 3. Regra $\exists$

$(\exists r. B)(a)$ exige que exista *algum* r-sucessor em B. Crio um indivíduo novo $z$:

---
## 4. Regra $\forall$ 

Agora $(\forall r. \neg B)(a)$ diz que *todo* r-sucessor de $a$ tá em $\neg B$.
Como eu já tenho $r(a, z)$, sou obrigado a adicionar:

$\neg B (z)$

---
# 5. Procurar a contradição

Olho o $z$: tenho um $B(z)$ (do passo 3) e $\neg B(z)$ (do passo 4). 

Pronto! O ramo fecha

---

Como esse era o único ramo (não teve nenhuma disjunção pra abrir mais caminhos), **todos** os ramos fecharam, então o conceito é **insatisfazível**.

**A intuição:** cê mandou existir um $r$ que é $B$, mas ao mesmo tempo disse que *todo* $r$ é $\neg B$. Impossível!

$A \sqcap \exists r.B \sqcap \exists r. \neg B$ já é insatisfazível, porque os dois $\exists$ criam *sucessores diferentes* ($z$ em $B$, e $w$ em $\neg B$, e não tem nenhum $\forall$ forçando eles a serem a mesma pessoa. É tipo a diferença entre "tem alguém de branco e tem alguém de preto" (o que é de boas) e o caso anterior.


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
