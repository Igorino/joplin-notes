https://github.com/Igorino/lista9_ML

# Modelo:
$$
	P = \text{softmax}(XW), L(W) = - {1 \over n} \sum_{i=1}^n \sum_{k=1}^K Y_{ik} \log P_{ik}
$$

# Gradiente: 
$$
	\nabla_w L = {1 \over n} X^T (P - Y)
$$

# Hessiana:
Para cada amostra $i$:
$$
	R_i \text{diag}(p_i) - p_i p_i^T
$$
Onde $p_i$ é a linha $P_{i:}$.

Então, o bloco $(k, l)$ da Hessiana é:
$$
	H_kl = {1 \over n} \sum_{i=1}^n R_i [k,l] x_i x_i^T
$$

Equivalente em termos de $p