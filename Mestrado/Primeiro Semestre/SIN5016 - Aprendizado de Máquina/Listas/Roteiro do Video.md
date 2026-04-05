# Roteiro do vídeo — Trabalho de Aprendizado de Máquina (SIN5016)

## Abertura
Oi, professor, tudo bem?
Meu nome é Igor, e neste vídeo eu vou apresentar rapidamente o meu trabalho da atividade parcial, onde eu implementei um sistema de identificação biométrica facial usando os descritores HOG e LBP, comparando o desempenho deles com MLP e SVM.

A ideia do trabalho foi comparar cenários de melhor e pior desempenho, conforme solicitado no enunciado, e eu vou mostrar também alguns trechos do código.

---

## 1. Subconjunto da base (make_subset.py)
Primeiro, como a base CelebA é muito grande, eu precisei criar um subconjunto balanceado.

### Trecho: definição do subconjunto
Arquivo: make_subset.py
```python
K_IDS = 50
M_PER_ID = 10
SEED = 42
```

O que falar:
Aqui eu escolho usar 50 identidades e 10 imagens por identidade, o que gera um subconjunto balanceado com 500 imagens no total.

---

### Trecho: seleção aleatória das identidades
```python
random.seed(SEED)
selected_ids = random.sample(list(id_to_imgs.keys()), K_IDS)
```

O que falar:
Aqui eu faço a seleção aleatória das identidades, mas usando uma seed fixa para garantir a reprodutibilidade dos experimentos.

---

### Trecho: escolha das imagens por identidade
```python
for pid in selected_ids:
    imgs = random.sample(id_to_imgs[pid], M_PER_ID)
```

O que falar:
Neste ponto eu garanto que cada identidade tenha exatamente o mesmo número de imagens.

---

## 2. Pipeline geral (run_id.py)

### Trecho: divisão estratificada
Esse script funciona como uma versão inicial e mais simples do pipeline de identificação facial, servindo principalmente pra validar se o carregamento das imagens, a criação dos rótulos e a divisão dos dados estavam funcionando corretamente. Ele ajuda a checar se o problema de classificação multiclasse estava bem definido antes de entrar nos modelos mais pesados. Era só pra garantir que o dataset, os labels e o split treino/teste não estavam errados logo no começo.

Arquivo: run_id.py
```python
X_trainval, X_test, y_trainval, y_test = train_test_split(
    X, y, test_size=TEST_SIZE, random_state=SEED, stratify=y
)
```

O que falar:
Aqui eu faço a divisão estratificada entre treino, validação e teste, garantindo que todas as identidades apareçam proporcionalmente em cada conjunto. Eu tava tendo um erro com o stratify pq não tinha 

---


## 4. Implementação da MLP (mlp_model.py)

### Trecho: inicialização dos pesos
Arquivo: mlp_model.py
Aqui fica é onde fica a modelo de rede neural (MLP) usada no trabalho. Esse script tem a criação do modelo, o número de camadas ocultas, quantidade de neurônios, função de ativação e outros hiperparâmetros importantes. A ideia foi separar a definição do modelo da lógica de execução, pra deixar o código mais organizado e fácil de ajustar. Essa parte é onde ficam concentradas as decisões que mais impactam o overfitting, já que o MLP tende a memorizar o conjunto de treino com facilidade.
```python
self.W1 = np.random.randn(input_dim, hidden_dim) * 0.01
self.W2 = np.random.randn(hidden_dim, output_dim) * 0.01
```

A rede neural foi implementada do zero, usando apenas NumPy, sem utilizar a implementação pronta do scikit-learn.



## 3. HOG + MLP (melhor caso)

### Trecho: extração do HOG


Arquivo: run_mlp.py

Esse é o script principal do experimento com HOG + MLP. Ele carrega o subset de imagens, aplica o pré-processamento, pega os descritores HOG e usa os vetores de características como entrada pro MLP. Também é nesse script que acontece a divisão entre treino, validação e teste, além do loop de treinamento e da avaliação final do modelo. Aqui ficaram bem claros os problemas de overfitting, já que a acurácia de treino sobe rápido enquanto a validação e o teste ficam bem mais baixos. Apesar disso, esse foi o cenário com melhor desempenho geral do trabalho.

```python
feat = hog(img, **HOG_PARAMS)
```


O que falar:
Aqui eu extraio as características usando o descritor HOG, que captura informações estruturais do rosto.

---

### Trecho: normalização
```python
scaler = StandardScaler()
X_train = scaler.fit_transform(X_train)
X_val = scaler.transform(X_val)
X_test = scaler.transform(X_test)
```

O que falar:
Depois eu normalizo os dados, porque a MLP é bastante sensível à escala das features.

---


---

### Trecho: loop de treinamento
```python
for epoch in range(epochs):
    loss = self.train_step(X_train, y_train)
```

O que falar:
Aqui acontece o treinamento por épocas, e é nesse ponto que aparece o overfitting em algumas configurações.

---

## 5. Overfitting (resultados)

Trecho mostrado no terminal ou nos arquivos de resultado:
```
train_acc=1.0000, val_acc=0.1143
```

O que falar:
Dá para ver claramente que o modelo aprende muito bem o conjunto de treino, mas generaliza mal para validação e teste.

---

## 6. LBP + SVM

Esse script implementa o pipeline de classificação usando o descritor LBP em conjunto com um classificador SVM. Ele segue uma estrutura parecida com o run_mlp.py, mas troca o HOG pelo LBP e o MLP por um SVM. A extração de LBP é feita a partir de padrões binários locais e transformada em histogramas, que depois são usados como entrada pro SVM. Esse código foi fortemente baseado em exemplos da documentação do scikit-image e em tutoriais do PyImageSearch, com adaptações pro formato do trabalho. O desempenho final ficou baixo, o que mostrou que o LBP não funcionou tão bem nesse cenário multiclasse.

### Trecho: extração do LBP
Arquivo: run_lbp_svm.py
```python
lbp = local_binary_pattern(image, P, R, method="uniform")
hist, _ = np.histogram(lbp, bins=n_bins, density=True)
```

O que falar:
Aqui eu extraio o descritor LBP e construo o histograma normalizado que representa cada imagem.

---

### Trecho: classificação com SVM
```python
clf = LinearSVC(C=1.0)
clf.fit(X_train, y_train)
```

O que falar:
Essas features são classificadas usando uma SVM linear. Mesmo no melhor cenário, o desempenho ficou bem abaixo do HOG.

---

## 7. Pior cenário proposital
Esse script é uma variação propositalmente pior do run_lbp_svm.py, criado pra atender ao requisito do enunciado de gerar um cenário de pior desempenho. Nele, o descritor LBP é degradado de propósito, usando menos vizinhos e configurações menos discriminativas, o que reduz ainda mais a qualidade da representação das imagens. A ideia aqui não foi “errar sem querer”, mas sim mostrar, de forma controlada, como escolhas ruins de parâmetros impactam diretamente o desempenho do modelo, resultando em acurácia próxima ao aleatório.

### Trecho: redução da capacidade do modelo
Arquivo: run_lbp_svm_worse.py
```python
clf = LinearSVC(C=0.01)
```

O que falar:
Aqui eu reduzo propositalmente o parâmetro C da SVM para gerar um cenário de pior desempenho, como exigido no enunciado.

---

## 8. Organização dos resultados

### Trecho: criação das pastas de saída
```python
OUT_DIR = "results_lbp_worse"
os.makedirs(OUT_DIR, exist_ok=True)
```

O que falar:
Cada execução gera arquivos de configuração, erros, acurácia e o modelo salvo, todos organizados em pastas separadas.

---

## Encerramento
No geral, o HOG com MLP foi o que apresentou o melhor desempenho.
O LBP teve resultados próximos ao aleatório, especialmente por causa do problema multiclasse com poucas amostras por identidade.
O código completo e os experimentos estão disponíveis no repositório indicado no relatório.
Obrigado.
