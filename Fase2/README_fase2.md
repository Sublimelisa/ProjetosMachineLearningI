# Classificação com Machine Learning

> Projeto desenvolvido para a disciplina de **Machine Learning I**.  
> Esta fase aplica e compara algoritmos de classificação binária para prever a sobrevivência de passageiros do Titanic.


## Objetivo

Construir e avaliar classificadores binários usando o dataset preparado na Fase 1, comparando o desempenho de **4 algoritmos** com exploração de hiperparâmetros, validação cruzada e análise das métricas de classificação.

**Variável alvo:** `Survived` (0 = não sobreviveu, 1 = sobreviveu)


## Estrutura dos arquivos

```
Fase2/
├── Template - Fase 2 - Machine Learning I.ipynb   # Notebook com código, experimentos e análise
└── TitanicNovoDataset.csv                         # Dataset preparado na Fase 1
```

---

## Algoritmos utilizados

| Algoritmo | Hiperparâmetros explorados |
|---|---|
| **Árvore de Decisão** | `max_depth`, `min_samples_split`, `criterion` |
| **MLP (MultiLayer Perceptron)** | `hidden_layer_sizes`, `alpha` |
| **KNN (K-Nearest Neighbors)** | `n_neighbors`, `weights` |
| **Naive Bayes (Gaussian)** | `var_smoothing` |

A seleção dos melhores hiperparâmetros foi feita com **GridSearchCV**.

---

## Etapas realizadas

### 1) Escolha dos algoritmos e hiperparâmetros
- Definição de grade de hiperparâmetros para cada algoritmo
- Busca pelo melhor conjunto com `GridSearchCV` + validação cruzada estratificada

### 2) Divisão treino/teste com estratificação
- **80% treino / 20% teste**, com `stratify=y` para manter a proporção da classe alvo
- Validação durante treino com **5-fold StratifiedKFold**

### 3) Avaliação dos resultados

#### Métricas — Validação Cruzada (treino)

| Algoritmo | Acurácia | Precisão | Recall | F1-Score |
|---|---|---|---|---|
| Árvore de Decisão | 82,3% | 82,3% | 82,5% | 82,4% |
| MLP | 82,3% | 83,8% | 80,3% | 82,0% |
| KNN | **84,9%** | **82,6%** | **88,8%** | **85,5%** |
| Naive Bayes | 76,5% | 77,9% | 74,3% | 75,9% |

#### Métricas — Conjunto de Teste

| Algoritmo | Acurácia | Precisão | Recall | F1-Score |
|---|---|---|---|---|
| Árvore de Decisão | 85,2% | 85,6% | 84,6% | 85,1% |
| MLP | 84,1% | 90,8% | 75,8% | 82,6% |
| KNN | **90,7%** | **90,2%** | **91,2%** | **90,7%** |
| Naive Bayes | 76,0% | 85,1% | 62,6% | 72,2% |

### 4) Conclusão

O **KNN com K=11 e pesos por distância** foi o melhor algoritmo, atingindo **90,7% de acurácia** no conjunto de teste com excelente Recall (91,2%) — o que significa que o modelo identifica corretamente a grande maioria dos sobreviventes.

A Árvore de Decisão e o MLP apresentaram desempenho sólido (~84-85%), enquanto o Naive Bayes obteve o menor resultado, esperado pela violação do pressuposto de independência condicional entre os atributos.

---

## Visualizações geradas

- Gráficos de barras comparando Acurácia, Precisão, Recall e F1 (CV e teste)
- Matrizes de confusão para todos os modelos
- Visualização da Árvore de Decisão (primeiros 3 níveis)

---

## Tecnologias utilizadas

- Python 3.10
- pandas / numpy
- scikit-learn (`DecisionTreeClassifier`, `MLPClassifier`, `KNeighborsClassifier`, `GaussianNB`, `GridSearchCV`, `StratifiedKFold`, `cross_validate`)
- matplotlib / seaborn

---

## Uso de IA generativa

Este projeto utilizou ferramentas de IA generativa (Claude) como suporte para ideias, estruturação do código e explicação de conceitos. Todo o desenvolvimento, análise, interpretação dos resultados e tomada de decisões foi realizado pela autora, garantindo autoria intelectual do trabalho.