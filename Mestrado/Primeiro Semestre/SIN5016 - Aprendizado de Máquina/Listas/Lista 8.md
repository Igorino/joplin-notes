# 1) Atributo "Income"
## Valores: 
* **high**
* **medium**
* **low**

## Distribuição:
| Income | yes | no | total |
| :---: | :---: | :---: | :---: |
| high | 2 | 2 | 4 |
| medium | 4 | 2 | 6 |
| low | 3 | 1 | 4 |

## Entropias parciais:
### Income = **high**
$$
	\text{info} = -{2 \over 4} \log_2 {2 \over 4} - {2 \over 4} \log_2 {2 \over 4} = 1.0 
$$

### Income = **medium**
$$
	\text{info} = -{4 \over 6} \log_2 {4 \over 6} - {2 \over 6} \log_2 {2 \over 6} \approx 0.918 
$$

### Income = **low**
$$
	\text{info} = -{3 \over 4} \log_2 {3 \over 4} - {1 \over 4} \log_2 {1 \over 4} \approx 0.811
$$

## Entropia ponderada:
$$
	\text{info}_\text{income}(D) = {4 \over 14}(1.0) + {3 \over 4} - {1 \over 4} \log_2 {1 \over 4} \approx 0.811
$$