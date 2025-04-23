# <img alt="Simbolo Python" height="35" width="45" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg"> Classificação de Precipitação em Brasília

Este repositório contém um Jupyter Notebook que realiza uma análise exploratória, pré-processamento de dados e treinamento de modelos de Machine Learning para classificar níveis de precipitação na cidade de Brasília (base de dados de 2001 a 2019 do INMET).

---

## Índice

1. [Sobre o Projeto](#sobre-o-projeto)
3. [Pré-requisitos](#pr%C3%A9-requisitos)
4. [Instalação](#instala%C3%A7%C3%A3o)
5. [Estrutura dos Dados](#estrutura-dos-dados)
6. [Descrição do Notebook](#descri%C3%A7%C3%A3o-do-notebook)
7. [Metodologia](#metodologia)
8. [Resultados](#resultados)
9. [Como Executar](#como-executar)
10. [Salvar e Carregar Modelos](#salvar-e-carregar-modelos)
11. [Autores](#autores)

---

## Sobre o Projeto

O objetivo deste projeto é construir e avaliar modelos de classificação capazes de prever eventos de precipitação (chuva ou não chuva) e categorias de intensidade de chuva em Brasília, utilizando dados meteorológicos históricos. O projeto inclui:

- Importação e tratamento de dados meteorológicos (2001–2019).
- Transformação da variável alvo em classificações binárias e multiclasse.
- Balanceamento de classes para mitigar vieses.
- Treinamento de modelos de referência (Dummy), Árvore de Decisão e Perceptron Multicamadas (MLP).
- Avaliação usando matrizes de confusão, relatórios de classificação e taxas de acurácia.
- Serialização (pickle) dos modelos finalizados e demonstração de inferência em novos dados.


## Pré-requisitos

- Python 3.8+  
- Jupyter Notebook ou JupyterLab

## Instalação

1. Clone este repositório:
```
git clone https://github.com/joaoweslen/Classificacao_de_chuva_Brasilia.git
```

2. Crie e ative um ambiente virtual (opcional):
 ```
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows
```

3. Instale as dependências:
```
pip install -r requirements.txt
```

## Estrutura dos Dados

- **Arquivo CSV**: `dados_A001_D_2001-01-01_2019-12-31.csv`  
- **Formato**: delimitado por ponto e vírgula (`;`), codificação Latin-1, separador decimal vírgula.
- **Skiprows**: as 10 primeiras linhas são cabeçalhos não estruturados.

As colunas principais incluem:

| Coluna                                                          | Descrição                             |
|-----------------------------------------------------------------|---------------------------------------|
| `DATA MEDICAO`                                                  | Data da medição                       |
| `PRECIPITACAO`                                                  | Precipitação diária (mm)              |
| `TEMPERATURA MAXIMA`                                            | Temperatura máxima diária (°C)        |
| `TEMPERATURA MINIMA`                                            | Temperatura mínima diária (°C)        |
| `PRESSAO ATMOSFERICA MEDIA DIARIA`                              | Pressão atmosférica (mB)              |
| `TEMPERATURA DO PONTO DE ORVALHO MEDIA DIARIA`                  | Ponto de orvalho médio (°C)           |

## Descrição do Notebook

O notebook está organizado em seções:

1. **Importação de Bibliotecas**  
2. **Leitura e Visualização Inicial dos Dados**  
3. **Tratamento de Dados**  
   - Exclusão de colunas e valores nulos  
   - Conversão de tipos e criação de variáveis (meses, estações)  
4. **Exploração de Dados (EDA)**  
5. **Engenharia de Atributos**  
6. **Transformação da Variável Alvo**  
   - Classificação binária (chuva vs. não chuva)  
   - Classificação multiclasse (intensidade de chuva)  
7. **Balanceamento de Classes**  
   - Uso de técnicas como `NearMiss` do imbalanced-learn  
8. **Modelagem**  
   - Baseline DummyClassifier  
   - DecisionTreeClassifier  
   - MLPClassifier  
9. **Avaliação dos Modelos**  
   - Matriz de confusão  
   - Relatório de classificação  
   - Acurácia comparativa  
10. **Serialização dos Modelos**  
11. **Exemplo de Inferência em Novos Dados**

## Metodologia

1. **Pré-processamento**:
   - Leitura dos dados CSV com Pandas.
   - Tratamento de dados ausentes e tipos de dados.
   - Criação de colunas auxiliares (mês, estação do ano).
2. **Definição da variável alvo**:
   - Traduzir precipitação contínua em classes.
   - Binarizar para chuva x não chuva.
   - Criar faixas para classificação multiclasse.
3. **Divisão treino/teste**:
   - Train-test split com stratify para manter proporções.
4. **Balanceamento**:
   - Aplicação de `NearMiss` para reduzir sobreamostragem na classe majoritária.
5. **Treinamento de Modelos**:
   - DummyClassifier para baseline.
   - DecisionTree para interpretabilidade.
   - MLP como modelo não linear.
6. **Avaliação**:
   - Cálculo de acurácia, matriz de confusão e classification_report.
7. **Implantação**:
   - Serializar (pickle) encoder e modelo.
   - Demonstrar predição em novo exemplo.

## Resultados

> **Observação**: execute o notebook para obter métricas exatas (acurácia, precision, recall). Em geral, constatou-se:

- O **DummyClassifier** apresenta acurácia baixa (baseline).  
- A **Árvore de Decisão** atingiu acurácia intermediária e é facilmente interpretável.  
- O **MLPClassifier** (rede neural) geralmente apresentou melhor desempenho em dados balanceados.

Consulte o notebook para visualizar plots de comparação e matrizes de confusão.

## Como Executar

1. Abra o Jupyter Notebook:
```bash
jupyter notebook Classificacao_brasilia_PROD.ipynb
```
2. Execute as células em ordem.  
3. Verifique outputs, gráficos e métricas.

## Salvar e Carregar Modelos

No final do notebook, há exemplos de como serializar (`pickle.dump`) e recarregar (`pd.read_pickle`) o encoder e o modelo:

```python
import pickle
# Salvar
with open('modelo_onehotenc.pkl', 'wb') as f:
    pickle.dump(one_hot_encoder, f)
with open('modelo_mlp.pkl', 'wb') as f:
    pickle.dump(mlp_model, f)

# Carregar
modelo_onehot = pd.read_pickle('modelo_onehotenc.pkl')
modelo_mlp = pd.read_pickle('modelo_mlp.pkl')
```

## Autores

Este projeto foi desenvolvido em colaboração por:

- Caio Augusto de Oliveira Lara Lima - [@hyskoniho](https://github.com/hyskoniho)
- Gabriel Caldeira Bernardo - [@1caldeira](https://github.com/1caldeira)
- Gustavo da Rocha Marchiori - [@gustavomarchiori](https://github.com/gustavomarchiori)
- João Weslen Gonçalves Vieira - [@joaoweslen](https://github.com/joaoweslen)
- Jonathan Santiago Relva - [@JhowSantiago](https://github.com/JhowSantiago)
