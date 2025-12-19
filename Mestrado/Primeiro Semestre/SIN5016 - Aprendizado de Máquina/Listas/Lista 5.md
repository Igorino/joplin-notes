# Definição da Elastic Net
A Elastic Net é "MSE + L1 + L2". Uma forma bem comum dela é:
$$
	J(w) = {1 \over 2N} || Xw - y ||² + \lambda_1 || w||_1 + {\lambda_2 \over 2} || w ||²
$$
* $||w||_1 = \sum_j |w_j|$ (L1 / Lasso);
* 