# Otimização irrestrita da função de Rosebrock $(N=3)$
Função de Rosebrock:
$$
	f(x) = \displaystyle\sum_{i=1}^{N-1} [100(x_{i+1} - x_i²)^2+ (1 - x_i)²], x \in \reals^N
$$
$$
	f(x) = \displaystyle\sum_{i=1}^{2} [100(x_{i+1} - x_i²)^2+ (1 - x_i)²], x \in \reals^3
$$

O mínimo global ocorre em $(1, 1, 1)$, com $f = 0$

# Aproximação do Gradiente e da Hessiana
O Gradiente e a Hessiana foram aproximados por diferenças finitas centrais, usando um passo pequeno de $h$.
* Gradiente:
$$
	{\partial f \over \partial x_i} (x) \approx {{f(x + he_i) - f(x- he_i)} \over 2h}
$$
* Hessiana:
$$
	{\partial² f \over \partial x_i²} (x) \approx {{f(x + he_i) - 2f(x) + f(x - he_i)} \over h²}
$$
$$
	{\partial² f \over {\partial x_i \partial x_j}} (x) \approx {{f(x + he_i + he_j) - f(x + he_i - he_j) - f(x - he_i + he_j) + f(x - he_i - he_j)} \over 4h²}
$$

Foram utilizados valores típicos $h = 10^{-6}$ para o gradeinte e $h = 10^{-4}$ para a Hessiana

# Métodos utilizados
Foram implementados os seguintes métodos de otimização irrestrita:
 * **Gradiente descendente**, com escolha do passo via busca linera (razão áurea);
 * **Método de Newton**, com Hessiana A