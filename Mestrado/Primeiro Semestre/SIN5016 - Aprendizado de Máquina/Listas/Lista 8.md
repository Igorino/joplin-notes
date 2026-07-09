# 0) Conjunto total D:
 * **yes** = 9
 * **no** = 5
$$
	\text{Info}(D) = -{9 \over 14} \log_2 {9 \over 14} - {5 \over 14} \log_2 {5 \over 14} = 0.940
$$
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
	\text{info}_\text{income}(D) = {4 \over 14}(1.0) + {6 \over 14}(0.918) + {4 \over 14}(0.811) \approx 0.911
$$

## Ganho de informação:
$$
	\text{Gain}_\text{(income)} = 0.940 - 0.911 = 0.029
$$

# 2) Atributo "student"
## Valores:
 * **yes**
 * **no**

## Distribuição
| student | yes | no | total |
| :---: | :---: | :---: | :---: |
| yes | 6 | 1 | 7 |
| no | 3 | 4 | 7 |

## Entropias parciais:
### student = **yes**
$$
	\text{info} = -{6 \over 7} \log_2 {6 \over 7} - {1 \over 7} \log_2 {1 \over 7} \approx 0.592
$$

### student = **no**
$$
	\text{info} = -{3 \over 7} \log_2 {3 \over 7} - {4 \over 7} \log_2 {4 \over 7} \approx 0.985 
$$

## Entropia ponderada:
$$
	\text{info}_\text{student}(D) = {7 \over 14}(1.0) + {7 \over 14}(0.918) \approx 0.789
$$

## Ganho de informação:
$$
	\text{Gain}_\text{(student)} = 0.940 - 0.789 = 0.151
$$

# 3) Atributo "credit_rating"
## Valores:
 * **fair**
 * **excellent**

## Distribuição
| credit_rating | yes | no | total |
| :---: | :---: | :---: | :---: |
| fair | 6 | 2 | 8 |
| excellent | 3 | 3 | 6 |

## Entropias parciais:
### credit_rating = **fair**
$$
	\text{info} = -{6 \over 8} \log_2 {6 \over 8} - {2 \over 8} \log_2 {2 \over 8} \approx 0.811
$$

### student = **no**
$$
	\text{info} = -{3 \over 6} \log_2 {3 \over 6} - {3 \over 6} \log_2 {3 \over 6} = 1.0
$$

## Entropia ponderada:
$$
	\text{info}_\text{credit}(D) = {8 \over 14}(0.811) + {6 \over 14}(1.0) \approx 0.892
$$

## Ganho de informação:
$$
	\text{Gain}_\text{(student)} = 0.940 - 0.892 = 0.048
$$

# Ganho de informação total:
| Atributo | Ganho de informação |
| :---: | :---: |
| age | 0.246 |
| student | 0.151 |
| credit_rating | 0.048 |
| income | 0.029 |

# Regras finais:
* Se **age = middle_aged**, yes;
* Se **age = youth** e **student = yes**, yes;
* Se **age = youth** e **student = no**, no;
* Se **age = senior** e **credit_rating = fair**, yes;
* Se **age = senior** e **credit_rating = excellent**, no.

# Árvore:
```
                           age?
            ┌───────────────┼────────────────┐
         [youth]      [middle_aged]       [senior]
            |               |                |
         student?          yes         credit_rating?
        ┌────────┐                     ┌───────────┐
      [yes]     [no]                 [fair]   [excellent]
       yes       no                   yes         no
```