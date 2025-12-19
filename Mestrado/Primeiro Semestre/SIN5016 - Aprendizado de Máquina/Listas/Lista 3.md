# **1)** $f(x,y) = x² + y²$ no ponto $(1,2)$
## a) Analítico
$$
\nabla f(x,y) = (2x, 2y) \to \nabla f(1,2) = (2,4) \\
$$
$$
H(x,y) = \begin{bmatrix}
	2 & 0 \\
	0 & 2
\end{bmatrix}
$$

## b) Diferenças finitas
 - Para $\delta f / \delta x$: Avaliei $f(1+h, 2)$ e $f(1-h,2)$.
 - Para $\delta f / \delta y$: Avaliei $f(1, 2+h)$ e $f(1, 2-h)$
 - Para Hessiana:
	 - Diagonais com $f(1 \pm h, 2)$, $f(1,2)$, $f(1,2 \pm h)$
	 - Termo misto com os 4 cantos $(1 \pm h, 2 \pm h)$

## c) Resultado numérico com $h = 10^{-4}$
$$
\nabla f_h(1,2) \approx (2.00000000, 4.00000000)
$$

$$
H_h(1,2) \approx \begin{bmatrix}
	2 + 8*10^{-8} & -2.22 * 10^{-8}
	-2.22 * 10^{-8} & 2 + 8*10^{-8}
\end{bmatrix}
$$

Erros: 
- 