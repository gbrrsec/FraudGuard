# 🛡️ FraudGuard — Detecção de Fraudes com Machine Learning

## 📌 Sobre o Projeto

O FraudGuard é um projeto de Machine Learning desenvolvido para detectar possíveis fraudes em transações financeiras.

O projeto utiliza técnicas de classificação supervisionada para analisar transações e identificar padrões associados a atividades fraudulentas.

Durante o desenvolvimento, foram abordadas etapas importantes de um projeto de Machine Learning, incluindo:

- Análise exploratória dos dados
- Análise do desbalanceamento das classes
- Feature Engineering
- Separação dos dados em treino e teste
- Escalonamento das variáveis
- Treinamento de modelos
- Avaliação de métricas
- Análise de diferentes thresholds
- Comparação entre modelos
- Classificação de nível de risco

Além da classificação tradicional entre transações normais e fraudulentas, o projeto também utiliza as probabilidades previstas pelo modelo para classificar as transações em diferentes níveis de risco.

---

## 🎯 Objetivo

O objetivo deste projeto é desenvolver e avaliar modelos de Machine Learning capazes de identificar transações potencialmente fraudulentas.

Um dos principais desafios analisados foi o forte desbalanceamento presente na base de dados. Por esse motivo, métricas além da accuracy foram utilizadas para avaliar o desempenho dos modelos.

As principais métricas analisadas foram:

- Precision
- Recall
- F1-score
- ROC-AUC
- Matriz de Confusão

Também foram realizados testes com diferentes thresholds de classificação para analisar o equilíbrio entre a identificação de fraudes e a quantidade de falsos positivos.

---

## 📊 Dataset

A base de dados utilizada possui informações sobre transações financeiras e foi utilizada para desenvolver um modelo de classificação entre transações normais e fraudulentas.

A base possui:

- **284.807 transações**
- **31 colunas**
- **284.315 transações normais**
- **492 transações fraudulentas**

A variável `Class` representa a classificação da transação:

- `0` → Transação normal
- `1` → Transação fraudulenta

### ⚠️ Desbalanceamento dos Dados

Um dos principais desafios encontrados no projeto foi o forte desbalanceamento entre as classes.

| Classe | Quantidade | Proporção |
|---|---:|---:|
| Transações normais | 284.315 | 99,83% |
| Transações fraudulentas | 492 | 0,17% |

Esse desbalanceamento torna a accuracy uma métrica insuficiente quando analisada isoladamente.

Um modelo poderia apresentar uma alta accuracy simplesmente classificando a maioria das transações como normais.

Por esse motivo, o projeto também utiliza métricas como Precision, Recall, F1-score e ROC-AUC para avaliar a capacidade dos modelos de identificar corretamente a classe minoritária.

---

## 🛠️ Tecnologias Utilizadas

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- Jupyter Notebook

---

# ⚙️ Etapas do Projeto

O desenvolvimento do FraudGuard foi dividido nas seguintes etapas.

## 1. Exploração dos Dados

Inicialmente, o dataset foi analisado para verificar:

- Quantidade de registros e colunas
- Tipos de dados
- Valores ausentes
- Estatísticas descritivas
- Distribuição das classes

Durante essa análise, não foram identificados valores ausentes na base de dados.

---

## 2. Análise do Desbalanceamento

Foi analisada a distribuição da variável `Class`, identificando uma grande diferença entre a quantidade de transações normais e fraudulentas.

Essa análise foi importante para definir métricas mais adequadas para a avaliação dos modelos.

---

## 3. Feature Engineering

Foi criada uma nova variável chamada `Amount_log` utilizando uma transformação logarítmica sobre o valor das transações.

```python
df["Amount_log"] = np.log1p(df["Amount"])
```

A transformação logarítmica foi utilizada para reduzir o impacto de valores muito altos presentes na variável `Amount`.

---

## 4. Separação dos Dados

Os dados foram divididos entre conjuntos de treinamento e teste utilizando `train_test_split()`.

A divisão foi realizada com:

- 70% dos dados para treinamento
- 30% dos dados para teste
- Estratificação utilizando `stratify=y`

A estratificação foi utilizada para preservar a proporção das classes nos conjuntos de treinamento e teste.

---

## 5. Escalonamento

Foi utilizado `StandardScaler` para padronizar as variáveis antes do treinamento dos modelos.

O escalonamento foi aplicado após a separação entre os dados de treino e teste.

---

## 6. Treinamento dos Modelos

Foram treinados e avaliados dois modelos de Machine Learning:

- Regressão Logística
- Random Forest

---

## 7. Avaliação dos Modelos

Os modelos foram avaliados utilizando métricas mais adequadas para o problema de detecção de fraude:

- Precision
- Recall
- F1-score
- ROC-AUC
- Matriz de Confusão

A utilização dessas métricas foi importante devido ao forte desbalanceamento entre as classes.

---

## 8. Análise de Threshold

Foram realizados testes com diferentes thresholds para analisar como a alteração do limite de decisão afeta o desempenho da classificação.

Os thresholds analisados foram:

- `0.1`
- `0.2`
- `0.3`
- `0.4`
- `0.5`

Essa análise permitiu observar o trade-off entre Precision e Recall.

---

## 9. Classificação de Risco

As probabilidades previstas pelo modelo foram utilizadas para criar uma camada adicional de classificação de risco.

As transações foram classificadas em:

- 🟢 **Baixo risco**
- 🟡 **Médio risco**
- 🔴 **Alto risco**

Essa abordagem permite transformar as probabilidades previstas pelo modelo em uma informação mais interpretável para análise e priorização de transações suspeitas.

---

# 🤖 Resultados dos Modelos

## Regressão Logística

A Regressão Logística foi utilizada como modelo inicial para estabelecer uma base de comparação.

Com o threshold padrão de `0.5`, o modelo apresentou os seguintes resultados para a classe de fraude:

| Métrica | Resultado |
|---|---:|
| Precision | 85,98% |
| Recall | 62,16% |
| F1-score | 72,16% |

Os resultados mostram que o modelo apresentou uma boa precisão na identificação de fraudes, mas deixou de identificar parte das transações fraudulentas.

---

## 🎯 Análise de Threshold

Para analisar o impacto do threshold na classificação, foram testados diferentes valores.

| Threshold | Precision | Recall | F1-score |
|---:|---:|---:|---:|
| 0.1 | 75,18% | 71,62% | 73,36% |
| 0.2 | 78,63% | 69,59% | 73,84% |
| 0.3 | 79,51% | 65,54% | 71,85% |
| 0.4 | 84,21% | 64,86% | 73,28% |
| 0.5 | 85,98% | 62,16% | 72,16% |

A análise demonstra o trade-off entre Precision e Recall.

Thresholds menores aumentaram a capacidade do modelo de identificar fraudes, mas também reduziram a precisão das classificações.

Entre os valores analisados, o threshold `0.2` apresentou o melhor F1-score, enquanto o threshold `0.1` apresentou o maior Recall.

---

## 🌲 Random Forest

O modelo Random Forest foi treinado e avaliado utilizando o mesmo conjunto de dados de teste.

Entre os modelos avaliados, o Random Forest apresentou o melhor desempenho na identificação de transações fraudulentas.

Os resultados obtidos para a classe de fraude foram:

| Métrica | Resultado |
|---|---:|
| Precision | 95,73% |
| Recall | 75,68% |
| F1-score | 84,53% |

O modelo apresentou uma alta precisão e também conseguiu identificar uma quantidade maior de transações fraudulentas quando comparado à Regressão Logística.

O Recall de aproximadamente 75,68% indica que o modelo conseguiu identificar uma parcela significativa das fraudes presentes no conjunto de teste.

O F1-score de aproximadamente 84,53% apresentou o melhor equilíbrio entre Precision e Recall entre os modelos avaliados.

---

## 🏆 Comparação Final dos Modelos

A comparação entre os modelos permite analisar qual abordagem apresentou o melhor desempenho na identificação de transações fraudulentas.

| Modelo | Precision | Recall | F1-score |
|---|---:|---:|---:|
| Regressão Logística (`0.5`) | 85,98% | 62,16% | 72,16% |
| Regressão Logística (`0.2`) | 78,63% | 69,59% | 73,84% |
| Random Forest | **95,73%** | **75,68%** | **84,53%** |

### 🥇 Melhor Modelo

Entre os modelos e configurações avaliadas, o **Random Forest** apresentou o melhor desempenho geral.

O modelo obteve:

- Maior Precision
- Maior Recall
- Maior F1-score

Isso indica que, entre os modelos testados neste projeto, o Random Forest apresentou o melhor equilíbrio entre a capacidade de identificar fraudes e a precisão das classificações realizadas.

A Regressão Logística também apresentou resultados relevantes e permitiu analisar como a alteração do threshold influencia diretamente o equilíbrio entre Precision e Recall.

A comparação reforça a importância de avaliar diferentes métricas e modelos, especialmente em problemas com dados altamente desbalanceados, como a detecção de fraudes.

---

# 🚨 Sistema de Classificação de Risco

Além de classificar uma transação como normal ou fraudulenta, o projeto também utiliza as probabilidades previstas pelo modelo para criar uma classificação adicional de risco.

Essa abordagem permite transformar a saída do modelo em uma informação mais interpretável e pode ajudar na priorização de transações suspeitas.

As transações foram classificadas em três níveis:

| Nível de Risco | Interpretação |
|---|---|
| 🟢 Baixo risco | Baixa probabilidade estimada de fraude |
| 🟡 Médio risco | Probabilidade intermediária de fraude |
| 🔴 Alto risco | Alta probabilidade estimada de fraude |

No conjunto de teste, a distribuição obtida foi:

| Nível de Risco | Quantidade de Transações |
|---|---:|
| 🟢 Baixo risco | 85.291 |
| 🟡 Médio risco | 45 |
| 🔴 Alto risco | 107 |

A maior parte das transações foi classificada como baixo risco, o que está de acordo com o forte desbalanceamento presente na base de dados.

As transações classificadas como médio e alto risco representam casos que poderiam receber maior prioridade em uma possível análise manual.

> ⚠️ A classificação de risco é uma camada adicional baseada nas probabilidades previstas pelo modelo e deve ser interpretada de acordo com os thresholds definidos no projeto.

---

## 📁 Estrutura do Projeto

A estrutura principal do projeto está organizada da seguinte forma:

```text
FraudGuard/
│
├── fraud_detection.ipynb
├── README.md
└── requirements.txt
```

---
---

# 🔮 Possíveis Melhorias Futuras

Como evolução do projeto, algumas melhorias podem ser implementadas:

- Aplicação de técnicas para tratamento de dados desbalanceados, como SMOTE.
- Teste de outros algoritmos de Machine Learning.
- Ajuste e otimização de hiperparâmetros.
- Utilização de validação cruzada.
- Análise da importância das variáveis para identificar quais características possuem maior influência na detecção de fraudes.
- Teste de diferentes estratégias para definição do threshold.
- Criação de uma API para realizar previsões com o modelo treinado.
- Desenvolvimento de um dashboard para visualização e monitoramento das transações.
- Implementação de técnicas de monitoramento do desempenho do modelo em novos dados.

---

# 🧠 Principais Aprendizados

Durante o desenvolvimento do FraudGuard, foram explorados e praticados conceitos importantes relacionados a Ciência de Dados e Machine Learning.

Entre os principais aprendizados estão:

- Análise exploratória de dados.
- Identificação de dados desbalanceados.
- Importância de não utilizar apenas a accuracy como métrica de avaliação.
- Feature Engineering utilizando transformação logarítmica.
- Separação dos dados em conjuntos de treinamento e teste.
- Utilização de estratificação para preservar a distribuição das classes.
- Escalonamento de variáveis com StandardScaler.
- Treinamento de modelos de classificação.
- Avaliação utilizando Precision, Recall e F1-score.
- Utilização da Matriz de Confusão para análise dos resultados.
- Análise de diferentes thresholds de classificação.
- Comparação entre diferentes modelos de Machine Learning.
- Utilização de probabilidades para criação de uma classificação de nível de risco.

O desenvolvimento do projeto também permitiu compreender melhor o trade-off entre Precision e Recall em problemas de classificação.

Em um cenário de detecção de fraudes, identificar corretamente uma fraude pode ser mais importante do que obter uma alta accuracy geral. Por esse motivo, a escolha das métricas e do threshold deve considerar o objetivo do sistema e os possíveis impactos de falsos positivos e falsos negativos.

---

# 📌 Conclusão

O desenvolvimento do FraudGuard demonstrou os desafios envolvidos na criação de modelos de Machine Learning para detecção de fraudes.

Um dos principais pontos observados foi o forte desbalanceamento entre as classes. Esse cenário demonstrou que métricas como accuracy não devem ser utilizadas isoladamente para avaliar modelos de classificação.

A utilização de métricas como Precision, Recall e F1-score permitiu uma análise mais adequada da capacidade dos modelos de identificar transações fraudulentas.

Também foi possível observar como a alteração do threshold influencia diretamente o equilíbrio entre Precision e Recall.

Entre os modelos avaliados, o Random Forest apresentou o melhor desempenho geral, obtendo os maiores valores de Precision, Recall e F1-score para a identificação de transações fraudulentas.

Além da classificação tradicional entre transações normais e fraudulentas, o projeto também implementou uma camada de classificação de risco baseada nas probabilidades previstas pelo modelo.

O FraudGuard representa a aplicação prática de conceitos de análise de dados, preparação de dados e Machine Learning em um problema real de classificação.

---

# 👨‍💻 Autor

**Gabriel Almeida de Sousa**

Estudante de Análise e Desenvolvimento de Sistemas (ADS), com interesse em:

- Python
- Machine Learning
- Cibersegurança
- Cloud Security

Este projeto foi desenvolvido como parte da prática e evolução dos conhecimentos em Python, Análise de Dados e Machine Learning.

---

⭐ Se este projeto foi interessante para você, considere deixar uma estrela no repositório.