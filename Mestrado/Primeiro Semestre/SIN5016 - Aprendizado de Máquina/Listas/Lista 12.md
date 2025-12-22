# 1) Modelo MLP (Uma camada escondida)
Consideremos um MLP com uma camada escondida:
## Forward pass
Para uma amostra $x_i$:
* Camada escondida:
$$
	z_i^{(1)} = W_i^T x_i + b_1
$$
$$
	h_i = \phi (z_i^{(1)}) \qquad \text{(exemplo: tanh ou ReLU)}
$$

* Camada de saída:
$$
	z_i^{(2)} = W_2^T h_i + b_2
$$

* Softmax:
$$
	p_{ik} = { e^{z_{ik}^{(2)} } \over \sum_{j=1}^K e^{z_{ij}^{(2)}
$$