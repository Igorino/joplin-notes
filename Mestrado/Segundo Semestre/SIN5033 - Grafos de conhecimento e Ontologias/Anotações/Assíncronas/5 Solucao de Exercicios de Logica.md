# 1. Fomalização de Linguagem Natural
O primeiro passo é traduzeir frases me fómulas lógicas, atribuindo variáveis proposicionais.

Por exemplo:
> "Se Ana é alta e magra, então ela é elegante"

$p = \text{Ana é alta e magra}$, $q = \text{Ana é elegeante}$ 
$p \to q$

> "Se caio ama a natureza, então ele ama plantas e animais"

$p \to (q \land r)$

# 2. Formas de Argumento válido
Dois padrões clássicos usados o tempo todo:

| Regra | Forma | Exemplo |
| --- | --- | --- |
| **Modus Ponens (MP)**| $p \to q$, $p \vdash q$| *"Chove $\to$ rua molhada. Choveu, logo, rua molhada"* |
|**Modus Tollens (MT)**| $p \to q$, $\neg q \vdash \neg p$|*"Chove $\to$ rua molhada. Rua seca, logo, não choveu"*|

ATENÇÃO: Falácia classica no Exercício 3:
*"Rua amolhada $\therefore$ choveu"* é **inválido**.

A rua pode estar molhada por outra razão. A tabela-verdade confirma que a fórmula não é uma tautologia.

# 3. Dedução Natural
Provas formais passo a passo, citando a regra usada em cada linha.

Exemplo: $\{p \to q, ~ \neg q, ~ \neg p \to r\} \vdash r$:
$$
\begin{array}{lll}

(1) & p \to q & \text{(premissa)} \\
(2) & \neg q & \text{(premissa)} \\
(3) & \neg p \to r & \text{(premissa)} \\
(4) & \neg p & \text{(MT em 1,2)} \\
(5) & r & \text{(MP em 3,4)} \checkmark \\

\end{array}
$$

# 4. Prova por refutação
Em vez de procurar provar $C$ diretamnete, podemos assumir que $\neg C$ seja verdadeiro, e derivamos uma contradissão $(\perp)$ disso.

Exemplo (Exercício 5 - Ana e o remédio):

- **Premissas**: dor no estômago $\to$ irritada; remédio $\to$ dor; Ana não está iritada;
- **Objetivo**: provar que ana não tomou o remédio;
- Assumimos $r$ (tomou o remédio), e chegamos a conclusão que $p$ (dor) e $\neg p$ (MT) $\to$ **contradição** $\to$ logo $\neg r ~\checkmark$

# 5. Resolução (Forma Clausal)
Método algorítmico - base dos provadores automáricos. Todas as fórmulas são convertidas para cláusulas (disjunções) e aplicamos a regra:

> Se temos $A \lor p$ e $B \lor \neg p$, podemos concluir $A \lor B$

Exercício 8 (BBB na lógica):
- Premissas sobre o paredão, choro, conquista de público, eliminação, etc.
- Após conversão clausal, a resolução deriva $\vdash$ a partir da hipótese $s$ (chorou).
- Conclusão: o participante **não chorou**

# 6. Lógica de Primeira Ordem (LPO)
Vai além do proposicional, permite quantificar sobre objetos.

| Quantificador | Símbolo | Exemplo |
| --- | --- | --- |
| Universal | $\forall$ | *"Tudo que sobe, desce"* $\forall x ~ \text{sobe}(x) \to \text{desce}(x)$ |
| Existencial | $\exists$ | *"Alguns escritores são cultos"* $\exists x ~ \text{escritor}(x) \land \text{culto}(x)$ |

Ponto importante, escopo da negação:
> Nem toda estrada é perigosa

$\neg \forall x$ se transofmra em $\exists x (\text{estrada}(x) \land \neg \text{perigosa}(x))$

Isso equivale à *"algumas estradas não são perigosas"*. As duas frases dizem a mesma coisa.

# 7. Unificação 
Mecanismo que verifica se dois termos podem ser "casados" via substituição de variáveis, o que é fundamental em Prolog e motores de inferência.

Exemplos: 
- $\text{cor}( \text{sapato}(x), \text{branco})$ e $\text{cor}(\text{sapato}(\text{suspeito}), y)$ são unificados em $x/\text{suspeito}, y/\text{branco}$
- $\text{primo}(x, y)$ e $\text{prima}(a, b)$ $\to$ falha (predicados diferentes)
- $\text{ponto}(x, 2, z)$ e $\text{ponto}(1, w)$ $\to$ falha (aridades diferentes)



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