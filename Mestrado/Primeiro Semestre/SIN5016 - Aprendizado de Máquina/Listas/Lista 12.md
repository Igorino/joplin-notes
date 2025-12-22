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
	L = {1 \over n} \sum_{i=1}^n L_i
$$

# 3) Dedução no gradiente (usando backpropagation)
## Gradiente da loss em relação ao logits da saída
Resultado fundamental (softmax + entropia cruzada):
$$
	{\partial L_i \over \partial z_i^{(2)}}
$$
Elimina as derivadas complicadas do softmax.

Daí definimos:
$$
	\partial_i^{(2)} = p_i - y_i
$$

## Gradiente em relação aos parâmetros da camada de saída
Pesos:
$$
	{\partial L \over partial W_2} = {1 \over n} \sum_{i=1}^n h_i (\delta_i^{(2)})^T
$$

Bias:
$$
	{\partial L \over \partial b_2} = {1 \over n} \sum_{i=1}^n \delta_i^{(2)}
$$

Forma matricial:
$$
	\delta_{W_2} L = {1 \over n} H^T ( P - Y )
$$

## Propagação do erro para a camada escondida
Usando a regra da cadeia:
$$
	\delta
$$
