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

