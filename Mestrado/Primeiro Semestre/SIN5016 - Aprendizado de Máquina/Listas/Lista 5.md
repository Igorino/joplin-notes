# 1) Definição da Elastic Net
A Elastic Net é "MSE + L1 + L2". Uma forma bem comum dela é:
$$
	J(w) = {1 \over 2N} || Xw - y ||² + \lambda_1 || w||_1 + {\lambda_2 \over 2} || w ||²
$$
* $||w||_1 = \sum_j |w_j|$ (L1 / Lasso);
* $||w||_2 = \sum_j w_j²$ (L2 \ Ridge).

> Obs: As vezes o viés/intercepto não é regularizado, daí é só tirar o termo do intercepto dessas normas.

# 2) Derivada do termo de erro quadrático
Defina o resíduo: $r(w) = Xw-y$.

O termo de erro é:
$$
	{1 \over 2N} ||r||² = {1 \over 2N}r^Tr
$$

Derivando:
* $\nabla w (r^Tr) = 2X^Tr$ (pq $e = Xw-y$)
* Multiplicando pelo $1/(2N)$, fica:
$$
	\nabla_w ({1 \over 2N}||Xw-y||²) = {1 \over N} X^T(Xw-y)
$$

# 3) Derivada do termo L2
$$
	{\lambda_2 \over 2}||w||² = {\lambda_2 \over 2} \displaystyle\sum_{j}w_j²
$$
Derivando componente a componente:
$$
	{\partial \over \partial w_j} ( {\lambda_2 \over 2} w_j²) \lambda_2 w_j
$$
Em vetor:
$$
	\nabla_w ( {\lambda_2 \over 2} ||w||²) = \lambda_2 w
$$

# 4) "Derivada" do termo L1
$$
	\lambda_1||w||_1 = \lambda_1 \sum_j |w_j|
$$
Para cada componente:
* Se $w_j > 0$, ${d \over dw_j} |w_j| = +1$
* Se $w_j < 0$, ${d \over dw_j} |w_j| = -1$
* Se $w_j = 0$, não é diferenciável, então a gente usa subgradiente:
$$
	\partial |w_j| = [-1, 1]
$$
O subgradiente de L1 é:
$$
	\partial (\lambda_1 ||w||_1 ) = \lambda_1 s
$$
onde:
