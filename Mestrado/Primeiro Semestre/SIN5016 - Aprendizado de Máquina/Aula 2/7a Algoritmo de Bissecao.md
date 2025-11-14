# Algoritmo de Bisseção
O primeiro algortimo que vamos ver é o algoritmo de bisseção. 

Basicamente, algoritmo de bisseção é um algoritmo de Busca Linear que tenta simplifcar o processo reduzindo o problema em uma função unidimencional, que é derivada do problema multivariável.

# Transformando o problema multivariável em unidimensional

O que a gente pode fazer é reduzir o problema de otimização de **várias dimensões** ($x$ tendo vários componentes) pra um **problema de uma única dimensão** (e uma única variável, o $\alpha$).

Ele define:
$$
h(\alpha) := f(\bar x + \alpha \bar d)
$$

Onde:
 - $\bar x$ é o ponto atual;
 - $\bar d$ é a direção escolhida (ex.: $-\nabla f(\bar x)$); e
 - $\alpha$ é o escalar que diz **o quanto** você anda nessa direção.

Então, $h(\alpha)$ representa o **valor da função** $f$ se você andar $\alpha$ unidades na direção $d$.
Agora, em vez de minizar $f(x_1, x_2, x_3...)$, a gente só precisa **minimizar uma função simples** de $\alpha$.

# Um novo problema

O novo problema que vamos encontrar no caminho é:
$$
\bar \alpha = \arg \min\limits_{\alpha} h(\alpha)
$$

Ou seja:
> "Encontre o valor de $\alpha$ que faz $h(\alpha)$ mínimo"

Que é a mesma ideia da busca linear que falamos anteriormente.

# Propriedades de $h(\alpha)$
O Slide diz:

> $h(\alpha)$ é uma função convexa na variável escalar $a$.

Isso significa que o gráfico de $h(\alpha)$ é em uma **forma de tigela (convexo)**, então tem um **único ponto mínimo**.

Esse é o ideal, o nosso $\bar \alpha$.

# Derivando $h(\alpha)$
No Slide, é dito que devemos demonstrar:
$$
h'(\alpha) = \delta f(\bar x + \alpha \bar d)^T * \bar d
$$

Vamos destrinchar essa equação: 

Pela regra de cadeia: 
 - $f(\alpha) = f(\bar x + \alpha \bar d)$
 - Logo, derivando em relação à $\alpha$:
$$
{\delta h \over \delta \alpha} = {\delta f \over \delta x} * {\delta x \over \delta \alpha} = \nabla f(\bar x + \alpha \bar \delta)^T \bar d
$$