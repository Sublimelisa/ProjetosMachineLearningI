# Titanic - Análise Exploratória e Preparação dos Dados:

> Projeto desenvolvido para a disciplina de **Machine Learning I**.  
> Esta fase cobre o processo completo de EDA (Exploratory Data Analysis) e preparação do dataset para classificação.


## Objetivo

Explorar, limpar e preparar o dataset do Titanic (versão modificada) para uso em algoritmos de classificação binária, tendo como variável alvo a coluna **`Survived`**.


## Estrutura dos arquivos

```
Fase1/
├── Template - Fase 1 - Machine Learning I.ipynb   # Notebook com todo o código e análise
├── Titanic-Dataset-Modificado.csv                 # Dataset original (com inconsistências)
└── TitanicNovoDataset.csv                         # Dataset final preparado
```


## Etapas realizadas

### 1) Formatação dos atributos
- Remoção de colunas sem valor preditivo: `PassengerId`, `Name`, `Ticket`, `Cabin`, `cost`, `budget`, `day`, `month`, `year`, `time`
- Padronização da coluna `Age`: extração do valor numérico de strings heterogêneas como `"22 years old"`, `"Age 38"`, `"estimated 4"`, `"~14 yo"` via expressão regular
- Conversão de `Sex` para binário numérico (`male=0`, `female=1`)
- Conversão de `Survived` para inteiro (`0/1`)
- Remoção de **286 linhas duplicadas**

### 2) Análise e escolha dos atributos
Análise exploratória com visualizações:
- Distribuição da variável alvo
- Taxa de sobrevivência por classe (`Pclass`) e sexo (`Sex`)
- Matriz de correlação entre atributos numéricos
- Boxplots de `Age` e `Fare` por sobrevivência
- Pairplot geral colorido pela classe alvo

**Atributos selecionados:** `Pclass`, `Sex`, `Age`, `SibSp`, `Parch`, `Fare`, `Embarked`

### 3) Preenchimento de dados faltantes com K-means
Técnica de imputação baseada em agrupamento:

1. Identificação dos atributos com dados faltantes: `Pclass`, `Sex`, `Age`, `Embarked`
2. Criação de um dataset auxiliar (`dataset2`) sem esses atributos
3. Aplicação do **K-means** no `dataset2` (K=5, escolhido pelo método do cotovelo)
4. Para cada cluster: cálculo da **mediana** (Age) ou **moda** (variáveis categóricas)
5. Preenchimento dos valores faltantes com a estatística do cluster correspondente

Após o preenchimento: **one-hot encoding** de `Embarked` → `Embarked_C`, `Embarked_Q`, `Embarked_S`

### 4) Tratamento de outliers e reescala
- Outliers de `Fare` tratados com **capping no percentil 99**
- Normalização **Min-Max** `[0, 1]` em todas as colunas numéricas

### 5) Balanceamento da coluna alvo
- Distribuição original: desbalanceada (mais casos de não sobrevivência)
- Técnica aplicada: **oversampling aleatório** da classe minoritária (`Survived=1`)
- Resultado: **456 sobreviventes / 456 não sobreviventes** (912 linhas totais)

---

## Características do dataset final (`TitanicNovoDataset.csv`)

| Característica | Status |
|---|---|
| Sem linhas duplicadas | ok |
| Sem dados faltantes | ok |
| Todas as colunas numéricas | ok |
| Valores normalizados [0,1] | ok |
| Coluna alvo balanceada | ok |

**Shape final:** 912 linhas × 10 colunas


## 🛠️ Tecnologias utilizadas

- Python 3.10
- pandas
- numpy
- scikit-learn (`KMeans`, `MinMaxScaler`)
- matplotlib
- seaborn

---

## Uso de IA generativa

Este projeto utilizou ferramentas de IA generativa (Claude) como suporte para ideias, estruturação do código e explicação de conceitos. Todo o desenvolvimento, análise, interpretação dos resultados e tomada de decisões foi realizado pela autora, garantindo autoria intelectual do trabalho.