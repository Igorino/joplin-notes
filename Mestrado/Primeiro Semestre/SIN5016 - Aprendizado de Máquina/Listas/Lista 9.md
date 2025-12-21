https://github.com/Igorino/lista9_ML

# Modelo:
$$
	P = \text{softmax}(XW), L(W) = - {1 \over n} \sum_{i=1}^n \sum_{k=1}^K Y_{ik} \log P_{ik}
$$

# Gradiente: 
$$
	\nabla_w L = {1 \over n} X^T
 (P - Y)$$
