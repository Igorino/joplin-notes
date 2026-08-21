# Roteiro – Explicação dos Scripts do Projeto

## make_subset.py

Esse script é responsável por criar um subconjunto menor e balanceado da base CelebA, que originalmente é grande demais pra rodar os experimentos com facilidade. Ele escolhe um número fixo de identidades (classes) e, pra cada uma, seleciona a mesma quantidade de imagens, garantindo que todas as classes tenham o mesmo número de amostras. Isso foi essencial pra evitar viés e também pra permitir divisão estratificada depois. Essa parte deu um certo trabalho porque algumas identidades tinham poucas imagens, e quando isso passava despercebido, o pipeline quebrava mais pra frente.

```python
# exemplo do make_subset.py
selected_ids = random.sample(valid_ids, NUM_CLASSES)
for identity in selected_ids:
    imgs = random.sample(images_by_id[identity], IMAGES_PER_CLASS)
```

Aqui eu garanto explicitamente que cada classe vai ter exatamente o mesmo número de imagens.

---

## run_id.py

Esse script funciona como um teste de sanidade do projeto. Ele implementa uma versão bem simples do pipeline de identificação facial só pra verificar se o carregamento das imagens, a criação dos rótulos e a divisão treino/teste estavam corretos. Antes de partir pros modelos mais pesados, eu usei esse script pra confirmar que o problema multiclasse estava bem definido e que não tinha erro básico nos labels.

```python
paths, y, class_names = list_images_by_class(DATA_DIR)
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.3, stratify=y
)
```

---

## mlp_model.py

Nesse arquivo fica definida a implementação da rede neural Multilayer Perceptron usada no trabalho. Em vez de usar o MLPClassifier pronto do scikit-learn, eu implementei a MLP do zero pra entender melhor o treinamento, o forward, o backward e onde exatamente surgia o overfitting.

```python
class SimpleMLP:
    def __init__(self, input_dim, hidden_dim, output_dim, lr, epochs):
        self.W1 = ...
        self.W2 = ...
```

---

## run_mlp.py

Esse é o script principal do experimento HOG + MLP, que acabou sendo o melhor cenário do trabalho. Ele carrega as imagens, aplica pré-processamento, extrai os descritores HOG e usa esses vetores como entrada da MLP.

```python
feat = hog(img, orientations=9,
           pixels_per_cell=(8, 8),
           cells_per_block=(2, 2))

mlp.fit(X_train, y_train, X_val, y_val)
```

---

## run_lbp_svm.py

Esse script implementa o pipeline usando LBP junto com um classificador SVM. Ele foi fortemente baseado em exemplos da documentação do scikit-image e do PyImageSearch.

```python
lbp = local_binary_pattern(img, N_POINTS, RADIUS, method="uniform")
hist, _ = np.histogram(lbp.ravel(), bins=n_bins)
clf = LinearSVC(C=10.0)
```

---

## run_lbp_svm_worse.py

Esse script é uma versão propositalmente pior do run_lbp_svm.py, criada só pra cumprir o requisito do enunciado.

```python
MODEL_PARAMS = dict(C=0.01)
```

