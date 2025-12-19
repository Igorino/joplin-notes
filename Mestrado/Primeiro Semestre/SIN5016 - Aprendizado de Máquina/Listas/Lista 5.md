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
	\nabla_w ({1 \over 2N}||Xw-y||²) = {1 \over N}
$$