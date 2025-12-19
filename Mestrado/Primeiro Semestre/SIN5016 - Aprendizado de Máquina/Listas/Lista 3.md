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
| $10^{-1}$ | $4.441*10^{-15}$ | $7.024*10^{-14}$ |
| $10^{-2}$ | $8.528*10^{-14}$ | $6.288*10^{-12}$ |
| $10^{-3}$ | $4.925*10^{-13}$ | $3.954*10^{-10}$ |
| $10^{-4}$ | $4.006*10^{-12}$ | $1.129*10^{-7}$ |
| $10^{-5}$ | $2.930*10^{-11}$ | $2.340*10^{-7}$ |
| $10^{-6}$ | $3.023*10^{-10}$ | $1.125*10^{-3}$ |

Como a função é polinômio de grau 2, as diferenças centrais quase acertam. O que aparece é o erro numérico, principalmente na Hessiana quando $h$ fica pequeno demais.

# **2)** $f(x,y) = \ln(1 + x² + y²)$ no ponto $(0.5, -0.5)$
## a) Analítico
Se $D = 1 + x² + y²$,
$$
\nabla f=({2x \over D}, {2y \over D})
$$

No ponto, $D = 1 + 0.25 + 0.25 = 1.5$:
$$
	\nabla f(0.5, -0.5) = ({2 \over 3}, -{2 \over 3}) \approx (0.67, -0.67)
$$

Hessiana:
$$
	H = \begin{bmatrix}
		{2 \over D} - {4x² \over D²} & -{4xy \over D²} \\
		-{4xy \over D²} & {2 \over D} - {4x² \over D²}
	\end{bmatrix}
	\to
	H \approx \begin{bmatrix}
		.0.89 & 0.45 \\
		0.45 & 0.89
	\end{bmatrix}
$$

## b) Diferenças finitas
Mesma lógica do exercício 1:
* Gradiente: 4 avaliações $(x \pm h, y)$, $(x , y \pm h)$
* Hessiana: reutiliza essas + 4 avaliações nos cantos $(x \pm h, y \pm h)$

## c) Resultado numérico com $h = 10^{-4}$
$$
	\nabla f_h \approx (0.67, -0.67)
$$
$$
	H_h \approx \begin{bmatrix}
		0.89 & 0.45 \\
		0.45 & 0.89
	\end{bmatrix}
$$

Erros:
 * $|| \nabla f_h - \nabla f||_2 \approx 4.89 * 10^{-9}$
 * $||H_h - H||_F \approx 1.75 * 10^{-8}$

## d) Influêcia de $h$
| h | $mod(\text{erro grad})_2$ | $mod(\text{erro Hess})_F$ |
|:---:|:---:|:---:|
| $10^{-1}$ | $4.871*10^{-3}$ | $1.109*10^{-2}$ |
| $10^{-2}$ | $4.888*10^{-5}$ | $1.119*10^{-4}$ |
| $10^{-3}$ | $4.889*10^{-7}$ | $1.120*10^{-6}$ |
| $10^{-4}$ | $4.889*10^{-9}$ | $1.748*10^{-8}$ |
| $10^{-1}$ | $4.093*10^{-11}$ | $1.163*10^{-7}$ |
| $10^{-1}$ | $5.328*10^{-11}$ | $6.320*10^{-5}$ |

O erro cai até chegar no $10^{-4}$. Depois a Hessiana piora.

# **3)** $f(x,y,z) = x\e^y + $