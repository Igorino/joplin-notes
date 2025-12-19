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
 * $||f_h - \nabla f||_2 \approx 4.01 * 10^{-12}$
 * $||H_h - H||_F \approx 1.13 *10^{-7}$

## d) Influência de $h$ (erro vs $h$)
| h | $mod(\text{erro grad})_2$ | $mod(\text{erro Hess})_F$ |
|:---:|:---:|:---:|
| $10^{-1}$ | $4.441*10^{-15}$ | 7.024e-14 |
| $10^{-2}$ | 8.528e-14 | 6.288e-12 |
| $10^{-3}$ | 4.925e-13 | 3.954e-10 |
| $10^{-4}$ | 4.006e-12 | 1.129e-07 |
| $10^{-5}$ | 2.930e-11 | 2.340e-07 |
| $10^{-6}$ | 3.023e-10 | 1.125e-03 |