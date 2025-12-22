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
	p_{ik} = { 
		e^{
			z_{ik}^{(2)} 
		} \over 
		\sum_{j=1}^K e^{
			z_{ij}^{(2)} 
		} 
	}
$$

# 2) Função de perda: Entropia cruzada
Para classificação multiclasse com rótulo one-hot $y_i$:
$$
	L_i = - \sum_{k=1}^K y_{ik} \log(p_{ik})
$$

Loss média no dataset:
$$
	L = {1 \over n} \sum_{i=}
$$