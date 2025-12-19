# Problemas irrestritos (Continuação)

Como identificar se um ponto é mínimo, máximo ou indefinido em funções sem restrições?

## Teorema:
Se $f(x)$ é duas vezes diferenciável em $\bar x$:
 - Se o *Gradiente* $\nabla f(\bar x) = 0$ (Ou seja, é ponto crítico)
 - E a *Hessiana* $H(\bar x)$ é **definida positiva**

Então o $\bar x$ é um **mínimo local estrito**.

Basicamente, o Gradiente nulo indica que não há direção de descida (parada).
A Hessiana positiva indica que a curvatura é pra cima em todas as direções, como o fundo de uma bacia.

Outras observações:
- Se $\nabla f(\bar x) = 0$ e $H(\bar x)$ é **definida negativa**
	- Temos um **máximo local** (cuvatura para baixo, como se o ponto fosse o topo de uma montanha)
- Se $H(\bar x)$ é **semidefinida positiva**
	- Não dá pra afirmar que é mínimo (Por que pode ser um "ponto de sela", ou plano em alguma direção)

## Prova:
### Relembrando o teorema (condição suficiente de 2ª ordem):
<center>

Se $f: \reals^n \to \reals$ é uma constante $C²$ num bairro de $\bar x$, $\nabla f(\bar x) = 0$ e a Hessiana $H(\bar x)$ é **definida positiva**, então $\bar x$ é um **mínimo local estrito**.
</center>

**O que precisa aparecer nessa prova:**
- Mostrar que existe $r>0$ tal que ${0 < ||x - \bar x|| < r} \implies f(x) > f(\bar x)$

> ##### Adendo :
> Quando um teorema diz que:
> - "$f(x)$ é duas vezes diferenciável **num bairro** de $\bar x$"

>Ele quer dizer basicamente que:
> - "A função $f$ tem derivadas até a segunda ordem **não só exatamente em $\bar x$**, mas também em **ponto próximos**".

> Ou seja, precisamos que $f$ seja "suave" (sem quebras, pontas ou descontinuidades) **numa região em volta do ponto $\bar x$**.

### Passo 0: Ferramentas a serem usadas
**1. Taylor de 2ª ordem com resto (multivariável)**:

Para $d = x - \bar x$ pequeno o suficiente,
$$
f(\bar x + d) = f(\bar x) + \nabla f(\bar x)^T d + {1 \over 2} d^T H(\bar x) d + r(d)
$$

Onde $r(d) = o(||d||²)$, isto é:
$$
{\lim \limits_{||d|| \to 0}} {|r(d)| \over ||d||²} = 0
$$
> Tradução: o resto $r(d)$ é Little o (Ao oposto de Big O) de $||d||²$ . Ou seja, cresce muito mais devagar que $||d||²$ quando nos aproximamos do ponto $\bar x$
>
> Também podemos falar: "Para $d$ pequeno o suficiente, o reasto $r(d)$ é menor que qualquer fração do termo $||d||²$"

**2. Fato de Álgebra Linear para matrizes simétricas Definida Positiva**:

Se $H(x)$ é Definida Positiva, então existe uma curvatura mínima $\lambda_{\min} > 0$ tal que:
$$
d^T H(\bar x) d \ge \lambda_{\min} ||d||², \forall d
$$

> Traduzindo: É o menor autovalor. Como é um "fundo de uma tigela", onde a função curva pra cima em todas as direções, a curvatura da função sempre  vai ser maior que (ou pelo menos igual à) $\lambda_{\min}$.

## Passo 1: Aplicar Taylor e zerar o termo linear

Como o "fundo da bacia" é reto, $\nabla f(\bar x) = 0$.

Então, o termo linear some, e passamos o $f(\bar x)$ para o outro lado:

$$
f(\bar x + d) = f(\bar x) + \cancel{\nabla f(\bar x)^T d} + {1 \over 2} d^T H(\bar x) d + r(d)
$$
$$
\tag{1} f(\bar x + d) - f(\bar x) =  {1 \over 2} d^T H(\bar x) d + r(d)
$$
## Passo 2: Usar a propriedade da curvatura positiva

Como sabemos pelo fato da Hessiana $H(\bar x)$ ser **Definida Positiva**, ela curva pra cima, então ela pode ser maior que uma hipotética curvatura $\lambda_{\min}$: 
$$
\tag{2} d^T H(\bar x) d \ge \lambda_{\min} ||d||²
$$
Substituindo isso na função anterior:
$$
\tag{3} f(\bar x + d) - f(\bar x) \ge {1 \over 2} \lambda_{\min} ||d||² + r(d)
$$

## Passo 3: Controlar o resto $r(d)$
Sabemos que o termo quadrático vale no mínimo
$$
{1 \over 2} H(\bar x) d \ge {1 \over 2} \lambda_{\min}||d||²
$$
Se o erro for **menor que metade disso**, o resultado continua positivo.

Escolhendo:
$$
|r(d)| \le {1 \over 4}\lambda_{\min}||d||^2
$$
Garante que:
$$
{1 \over 2} \lambda_{\min} ||d||^2 - |r(d)| \ge {1 \over 4} \lambda_{\min}||d||² > 0
$$
Daí o resultado fica limpo e **estritamente positivo**

Logo, como o $r(d) = \text{o}(||d||²)$, existe $\partial > 0$ tal que, se $||d|| < \partial$:
$$
\tag{4} |r(d)| \le {1 \over 4} \lambda_{\min} ||d||²
$$
> Tradução: Quando chega suficientemente perto, o resto $r(d)$ fica bem pequeno e **não consegue vencer** o termo quadrático, ele cresce mais devagar ($\text{Little o} (||d||²)$)

## Passo 4: Concluir

Das equações $(3)$ e $(4)$, como sabemos que $0 < ||d|| < \partial$, substituimos:
$$
f(\bar x + d) -f(\bar x) \ge {1 \over 2} \lambda_{\min} ||d||² - {1 \over 4} \lambda_{\min} ||d||²
$$
$$
f(\bar x + d) -f(\bar x) = {1 \over 4} \lambda_{\min} ||d||² > 0
$$

Logo, todo ponto suficentemente próximo, mas diferente, tem o valor **maior** que $f(\bar x)$. 

Portanto, $\bar x$ é **mínimo local estrito**. 