# Detecção de Anomalias em Transações Financeiras com Isolation Forest

## Sobre o Projeto

Este projeto foi desenvolvido em **Python** utilizando **Jupyter Notebook** com o objetivo de aplicar técnicas de **Machine Learning** para identificar transações financeiras potencialmente fraudulentas.

A solução utiliza o algoritmo **Isolation Forest**, um método de aprendizado de máquina não supervisionado especializado na detecção de anomalias em conjuntos de dados com elevado desbalanceamento.

Para o estudo foi utilizada a base de dados **Credit Card Fraud Detection**, amplamente empregada em pesquisas acadêmicas e projetos de Ciência de Dados voltados à detecção de fraudes em cartões de crédito.

---

## Objetivos

- Aplicar técnicas de Inteligência Artificial na detecção de fraudes financeiras.
- Implementar o algoritmo **Isolation Forest** utilizando a biblioteca Scikit-learn.
- Realizar análise exploratória dos dados (EDA).
- Preparar e tratar os dados para treinamento do modelo.
- Avaliar o desempenho da solução através de métricas de classificação.
- Demonstrar a aplicação prática de Machine Learning em problemas do mercado financeiro.

---

## Base de Dados

O projeto utiliza o conjunto de dados **Credit Card Fraud Detection**, composto por milhares de transações realizadas com cartões de crédito.

A variável **Class** representa o objetivo da análise:

- **0** → Transação legítima
- **1** → Transação fraudulenta

### Distribuição das Classes

| Classe | Quantidade |
|---------|-----------:|
| 0 (Normal) | 284.315 |
| 1 (Fraude) | 492 |

A base apresenta um elevado desbalanceamento, característica comum em problemas de detecção de fraude.

---

## Etapas do Projeto

- Importação das bibliotecas
- Carregamento da base de dados
- Análise exploratória (EDA)
- Visualização gráfica das variáveis
- Preparação dos dados
- Separação entre variáveis preditoras e variável alvo
- Treinamento do modelo Isolation Forest
- Predição das anomalias
- Avaliação dos resultados
- Análise das métricas de desempenho

---

## Tecnologias Utilizadas

- Python 3
- Jupyter Notebook
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- Isolation Forest

---

## Resultados

Os resultados demonstraram que o algoritmo **Isolation Forest** foi capaz de identificar padrões anômalos em uma base altamente desbalanceada, detectando parte das transações fraudulentas por meio da análise das características estatísticas dos dados.

Além da implementação do modelo, foram realizadas análises exploratórias e visualizações gráficas que auxiliaram na compreensão da distribuição das informações e do comportamento das anomalias presentes na base.

---

## Estrutura do Projeto

Deteccao-Anomalias-IsolationForest/
│
├── dados/
│   └── creditcard.csv
│
├── notebook/
│   └── Deteccao_Anomalias_IsolationForest.ipynb
│
├── imagens/
│   ├── distribuicao_classes.png
│   ├── matriz_confusao.png
│   └── resultados.png
│
├── README.md
└── requirements.txt
