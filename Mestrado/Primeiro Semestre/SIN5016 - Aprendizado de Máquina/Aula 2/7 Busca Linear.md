# Busca Linear

Bem, basicamente, a **busca linear** (ou *linear search*) serve pra escolher o **melhor tamanho de passo $\alpha$** em cada iteração do gradiente descendente que acabamos de ver.

# Por que isso importa?

No gradiente descendente, se você escolher o $\alpha$:

- **Muito pequeno**: passos lentos, converge devagar;
- **Muito grande**: pode ultrapassar o mínimo e oscilar;
- **Ótimo**: passo exato que minimiza a função ao longo da direção escolhida.

# Problema exemplo

Vamos supor que $f(x)$ é uma função convexa continuamente diferenciável e desejamos solucionar:

$$
\bar \alpha := \arg \min\limits_{\alpha} f(\bar x + \alpha \bar d)
$$

> Tradução: "Dado um ponto atual $\bar x$ e uma direção de descida $\bar d$, encontre o valor de $\alpha$ que faz a função $f(\bar x + a \bar d)$ ser mínima"

| Símbolo | Significado | Explicação |
| :---: | :---: | :---: |
| $f(x)$ | Função objetivo | É a função que queremos minimizar |
| $\bar x$ | Ponto atual | É o ponto onde a gente tá agora (na iteração atual) |
| $\bar d$ | Direção de descida | É o vetor que aponta pra onde a função diminui mais rápido (normalmente é $-\nabla f(\bar x)$) |
| $\alpha$ | Tamanho do passo | É o quanto a gente vai andar na direção $\bar d$ |
| ${f(\bar x + \alpha \bar d)}$ | Função ao longo da reta | Representa o valor de $f$ ao andar um pouco ($\alpha$) na direção $\bar d$ |
| $\arg \min\limits_{\alpha}$ | "O valor de $\alpha$ que minimiza" | É o $\alpha$ ótimo que faz $f(\bar + \alpha \bar d)$ ser o menor possível |
| $\bar \alpha$ | O passo ótimo | É o tamanho ideal para do passo nessa direção |

## Agora, queremos resolver:

$$
\min\limits_{\alpha} f(x), x \in X
$$

> "Queremos encontrar o $x$ que minimiza a função $f(x)$ dentro do conjunto de soluções possíveis $X$

No caso do **gradiente descendente**, $X = \reals^n$ (Sem restrições), então estamos só tentando achar o ponto onde $f(x)$ é o menor possível.

## O que significa "direção descendente"

Ele é:

$$
f(\bar x + \epsilon \bar d) < f(\bar x), \forall \epsilon > 0 \text{ (e suficientemente pequeno)}
$$

Ou seja, $d$ é realmente uma **direção de descida** (downhill direction).

Agora vamos ver os algoritmos de busca linear:


