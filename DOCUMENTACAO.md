# Documentação Detalhada: Análise de Atrasos em Voos Domésticos no Brasil

Este documento fornece uma visão detalhada do projeto de análise de atrasos em voos domésticos no Brasil, complementando as informações presentes no `README.md` e no Jupyter Notebook `analise_atrasos_voos.ipynb`.

## Sumário

1.  [Introdução e Problemática](#1-introdução-e-problemática)
2.  [Coleta de Dados](#2-coleta-de-dados)
    *   [Fonte dos Dados](#21-fonte-dos-dados)
    *   [Descrição dos Arquivos](#22-descrição-dos-arquivos)
    *   [Processo de Obtenção](#23-processo-de-obtenção)
3.  [Preparação e Limpeza dos Dados](#3-preparação-e-limpeza-dos-dados)
    *   [Carregamento dos Dados](#31-carregamento-dos-dados)
    *   [Tratamento de Cabeçalhos e Codificação](#32-tratamento-de-cabeçalhos-e-codificação)
    *   [Conversão de Tipos de Dados](#33-conversão-de-tipos-de-dados)
    *   [Renomeação de Colunas](#34-renomeação-de-colunas)
    *   [Tratamento de Valores Ausentes (se aplicável)](#35-tratamento-de-valores-ausentes-se-aplicável)
4.  [Análise Exploratória de Dados (EDA)](#4-análise-exploratória-de-dados-eda)
    *   [Estatísticas Descritivas Gerais](#41-estatísticas-descritivas-gerais)
    *   [Análise de Atrasos por Empresa Aérea](#42-análise-de-atrasos-por-empresa-aérea)
    *   [Análise de Atrasos por Aeroporto de Origem](#43-análise-de-atrasos-por-aeroporto-de-origem)
    *   [Análise de Atrasos por Aeroporto de Destino](#44-análise-de-atrasos-por-aeroporto-de-destino)
    *   [Visualizações Chave](#45-visualizações-chave)
5.  [Engenharia de Features e Pré-processamento para Modelagem](#5-engenharia-de-features-e-pré-processamento-para-modelagem)
    *   [Criação da Variável Alvo](#51-criação-da-variável-alvo)
    *   [Seleção de Features para Modelagem](#52-seleção-de-features-para-modelagem)
    *   [Codificação de Variáveis Categóricas](#53-codificação-de-variáveis-categóricas)
    *   [Padronização de Features Numéricas](#54-padronização-de-features-numéricas)
    *   [Divisão em Conjuntos de Treino e Teste](#55-divisão-em-conjuntos-de-treino-e-teste)
6.  [Modelagem Preditiva](#6-modelagem-preditiva)
    *   [6.1 Regressão Logística](#61-regressão-logística)
    *   [6.2 Árvore de Decisão](#62-árvore-de-decisão)
    *   [6.3 Modelos de Ensemble](#63-modelos-de-ensemble)
        *   [Random Forest](#random-forest)
        *   [Gradient Boosting](#gradient-boosting)
    *   [Avaliação dos Modelos](#64-avaliação-dos-modelos)
7.  [Análises Avançadas](#7-análises-avançadas)
    *   [7.1 Análise de Componentes Principais (PCA)](#71-análise-de-componentes-principais-pca)
    *   [7.2 Clusterização com K-Means](#72-clusterização-com-k-means)
8.  [Conclusões](#8-conclusões)
    *   [Principais Fatores de Atraso Identificados](#81-principais-fatores-de-atraso-identificados)
    *   [Desempenho dos Modelos Preditivos](#82-desempenho-dos-modelos-preditivos)
    *   [Insights da Clusterização e PCA](#83-insights-da-clusterização-e-pca)
    *   [Limitações do Estudo](#84-limitações-do-estudo)
    *   [Sugestões para Trabalhos Futuros](#85-sugestões-para-trabalhos-futuros)
9.  [Apêndice: Gráficos Gerados](#9-apêndice-gráficos-gerados)

---

## 1. Introdução e Problemática

Conforme detalhado no `README.md`, este projeto foca na análise dos atrasos em voos domésticos no Brasil. Atrasos e cancelamentos representam um desafio significativo para a indústria da aviação e para os passageiros, resultando em inconvenientes e perdas financeiras. O objetivo é utilizar dados públicos para entender melhor esses fenômenos e, se possível, prever sua ocorrência.

## 2. Coleta de Dados

### 2.1 Fonte dos Dados

Os dados foram coletados do portal de **Dados Abertos da Agência Nacional de Aviação Civil (ANAC)** do Brasil. A ANAC disponibiliza diversas informações sobre o setor aéreo, incluindo estatísticas de voos.

*   **URL Principal:** [https://www.anac.gov.br/acesso-a-informacao/dados-abertos/areas-de-atuacao/todos-os-dados-abertos](https://www.anac.gov.br/acesso-a-informacao/dados-abertos/areas-de-atuacao/todos-os-dados-abertos)

### 2.2 Descrição dos Arquivos

Para este estudo, foram utilizados os dados referentes a **Dezembro de 2024** (ou o período mais recente disponível no momento da coleta que se assemelhasse a este, conforme os arquivos baixados anteriormente), especificamente os seguintes anexos da seção "Percentuais de atrasos e cancelamentos - mensal":

*   **Anexo I.csv:** Contém dados detalhados de percentuais de atrasos e cancelamentos por empresa, número do voo, aeroportos de origem e destino.
*   **Anexo II.csv:** (Se utilizado, descrever seu conteúdo e relevância para o projeto. No desenvolvimento atual, o foco foi no Anexo I).
*   **Anexo III.csv:** (Se utilizado, descrever seu conteúdo e relevância para o projeto. No desenvolvimento atual, o foco foi no Anexo I).

O foco principal da análise recaiu sobre o `Anexo I.csv` devido à sua granularidade e riqueza de informações sobre as operações de voo.

### 2.3 Processo de Obtenção

Os arquivos foram baixados diretamente do portal da ANAC. O processo envolveu:

1.  Navegar até a página de Dados Abertos da ANAC.
2.  Localizar a seção "Percentuais de atrasos e cancelamentos - mensal".
3.  Selecionar o período desejado (Dezembro de 2024).
4.  Baixar os arquivos CSV correspondentes (Anexo I, II, III).

Os arquivos foram salvos no diretório `/home/ubuntu/projeto_atrasos_voos/` para serem acessados pelo notebook.

## 3. Preparação e Limpeza dos Dados

Esta etapa é crucial para garantir a qualidade dos dados e prepará-los para análise e modelagem.

### 3.1 Carregamento dos Dados

O principal arquivo, `Anexo I.csv`, foi carregado utilizando a biblioteca Pandas do Python.

```python
import pandas as pd

path_anexo_i = "/home/ubuntu/projeto_atrasos_voos/Anexo I.csv"
df_anexo_i = pd.read_csv(path_anexo_i, sep=";", encoding="latin1", skiprows=1, low_memory=False)
```

### 3.2 Tratamento de Cabeçalhos e Codificação

*   **Cabeçalho:** Observou-se que a primeira linha do arquivo CSV não continha os nomes das colunas, sendo necessário pular esta linha (`skiprows=1`) durante a leitura.
*   **Codificação:** Foi utilizada a codificação `latin1` (ou `iso-8859-1` como alternativa) para correta leitura dos caracteres especiais presentes no arquivo.

### 3.3 Conversão de Tipos de Dados

As colunas que representam percentuais (`Percentuais_de_Cancelamentos`, `Percentuais_de_Atrasos_superiores_a_30_minutos`, `Percentuais_de_Atrasos_superiores_a_60_minutos`) estavam formatadas como `object` (string) e utilizavam vírgula como separador decimal. Elas foram convertidas para o tipo numérico (`float`) da seguinte forma:

```python
colunas_percentuais = [
    'Percentuais_de_Cancelamentos',
    'Percentuais_de_Atrasos_superiores_a_30_minutos',
    'Percentuais_de_Atrasos_superiores_a_60_minutos'
]

for coluna in colunas_percentuais:
    if coluna in df_anexo_i.columns:
        df_anexo_i[coluna] = df_anexo_i[coluna].str.replace(',', '.').astype(float)
```

### 3.4 Renomeação de Colunas

Algumas colunas possuíam espaços no final de seus nomes. Para facilitar o acesso e evitar erros, esses espaços foram removidos:

```python
df_anexo_i.columns = df_anexo_i.columns.str.strip()
```

### 3.5 Tratamento de Valores Ausentes (se aplicável)

Durante a análise exploratória e o pré-processamento para modelagem, valores ausentes (NaN) em features numéricas relevantes (como as usadas para PCA e K-Means) foram preenchidos com a média da respectiva coluna para não perder registros.

```python
# Exemplo para uma feature específica durante o preparo para PCA/K-Means
# df_pca_data[col].fillna(df_pca_data[col].mean(), inplace=True)
```

## 4. Análise Exploratória de Dados (EDA)

A EDA teve como objetivo entender a estrutura dos dados, identificar padrões, anomalias e obter insights iniciais.

### 4.1 Estatísticas Descritivas Gerais

Foram calculadas estatísticas descritivas para as colunas numéricas e contagem de valores únicos para colunas categóricas.

```python
print(df_anexo_i.info())
print(df_anexo_i.describe(include='all'))
```

### 4.2 Análise de Atrasos por Empresa Aérea

Investigou-se quais empresas aéreas apresentaram os maiores e menores percentuais médios de atrasos e cancelamentos.

```python
media_atrasos_empresa = df_anexo_i.groupby('Empresa_Aerea')[
    ['Percentuais_de_Atrasos_superiores_a_30_minutos', 'Percentuais_de_Cancelamentos']
].mean().sort_values(by='Percentuais_de_Atrasos_superiores_a_30_minutos', ascending=False)

print("--- Média de Atrasos e Cancelamentos por Empresa Aérea ---")
print(media_atrasos_empresa.head(10))
```

### 4.3 Análise de Atrasos por Aeroporto de Origem

Identificaram-se os aeroportos de origem com os maiores percentuais médios de voos atrasados.

```python
media_atrasos_origem = df_anexo_i.groupby('Aeroporto_Origem_Designador_OACI')[
    'Percentuais_de_Atrasos_superiores_a_30_minutos'
].mean().sort_values(ascending=False)

print("--- Média de Atrasos (>30 min) por Aeroporto de Origem (Top 10) ---")
print(media_atrasos_origem.head(10))
```

### 4.4 Análise de Atrasos por Aeroporto de Destino

Similarmente, analisaram-se os aeroportos de destino.

```python
media_atrasos_destino = df_anexo_i.groupby('Aeroporto_Destino_Designador_OACI')[
    'Percentuais_de_Atrasos_superiores_a_30_minutos'
].mean().sort_values(ascending=False)

print("--- Média de Atrasos (>30 min) por Aeroporto de Destino (Top 10) ---")
print(media_atrasos_destino.head(10))
```

### 4.5 Visualizações Chave

Gráficos de barras foram utilizados para ilustrar as análises acima, facilitando a compreensão dos resultados. Por exemplo, para empresas aéreas:

```python
plt.figure(figsize=(18, 8))
sns.barplot(x=media_atrasos_empresa.head(15).index, y='Percentuais_de_Atrasos_superiores_a_30_minutos', data=media_atrasos_empresa.head(15), palette='viridis')
plt.title('Top 15 Empresas Aéreas por Média de Atrasos > 30 min')
plt.xlabel('Empresa Aérea')
plt.ylabel('Média de Percentual de Atrasos > 30 min')
plt.xticks(rotation=90)
plt.tight_layout()
plt.show()
```
*(Gráficos similares foram gerados para aeroportos de origem e destino, e podem ser encontrados no Apêndice ou no notebook)*

## 5. Engenharia de Features e Pré-processamento para Modelagem

### 5.1 Criação da Variável Alvo

Para os modelos de classificação, foi criada uma variável binária `Atraso_Significativo` que indica se um voo teve um percentual de atrasos superiores a 30 minutos maior que um limiar (ex: 10%).

```python
limiar_atraso = 10 # Definindo que mais de 10% de atrasos > 30 min é significativo
df_anexo_i['Atraso_Significativo'] = (df_anexo_i['Percentuais_de_Atrasos_superiores_a_30_minutos'] > limiar_atraso).astype(int)
```

### 5.2 Seleção de Features para Modelagem

Foram selecionadas features relevantes para a predição, como `Empresa_Aerea`, `Aeroporto_Origem_Designador_OACI`, `Aeroporto_Destino_Designador_OACI` e `Etapas_Previstas`.

### 5.3 Codificação de Variáveis Categóricas

Variáveis categóricas foram transformadas em numéricas usando `LabelEncoder`.

```python
from sklearn.preprocessing import LabelEncoder

le_empresa = LabelEncoder()
df_anexo_i['Empresa_Aerea_Cod'] = le_empresa.fit_transform(df_anexo_i['Empresa_Aerea'])
# ... (similar para outras colunas categóricas)
```

### 5.4 Padronização de Features Numéricas

Features numéricas contínuas (como `Etapas_Previstas` e os percentuais usados em PCA/K-Means) foram padronizadas usando `StandardScaler` para que tivessem média zero e desvio padrão unitário, o que é importante para algoritmos sensíveis à escala.

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
# Exemplo: scaled_data = scaler.fit_transform(df_pca_data)
```

### 5.5 Divisão em Conjuntos de Treino e Teste

Os dados foram divididos em 70% para treino e 30% para teste.

```python
from sklearn.model_selection import train_test_split

X = df_anexo_i[['Empresa_Aerea_Cod', 'Aeroporto_Origem_Cod', 'Aeroporto_Destino_Cod', 'Etapas_Previstas_Scaled']]
y = df_anexo_i['Atraso_Significativo']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42, stratify=y)
```

## 6. Modelagem Preditiva

Foram aplicados e avaliados diferentes modelos de classificação.

### 6.1 Regressão Logística

Um modelo linear simples e interpretável.

```python
from sklearn.linear_model import LogisticRegression

log_reg = LogisticRegression(random_state=42, max_iter=1000)
log_reg.fit(X_train, y_train)
y_pred_log_reg = log_reg.predict(X_test)
```

### 6.2 Árvore de Decisão

Permite visualizar as regras de decisão e a importância das features.

```python
from sklearn.tree import DecisionTreeClassifier

dtree = DecisionTreeClassifier(random_state=42, max_depth=5) # max_depth para evitar overfitting
dtree.fit(X_train, y_train)
y_pred_dtree = dtree.predict(X_test)

# Análise de importância das features
importances = pd.Series(dtree.feature_importances_, index=X_train.columns).sort_values(ascending=False)
```

### 6.3 Modelos de Ensemble

#### Random Forest
Combina múltiplas árvores de decisão para melhorar a robustez e precisão.

```python
from sklearn.ensemble import RandomForestClassifier

rf_clf = RandomForestClassifier(n_estimators=100, random_state=42, max_depth=10, class_weight='balanced')
rf_clf.fit(X_train, y_train)
y_pred_rf = rf_clf.predict(X_test)
```

#### Gradient Boosting
Constrói modelos de forma sequencial, onde cada novo modelo corrige os erros do anterior.

```python
from sklearn.ensemble import GradientBoostingClassifier

gb_clf = GradientBoostingClassifier(n_estimators=100, learning_rate=0.1, max_depth=3, random_state=42)
gb_clf.fit(X_train, y_train)
y_pred_gb = gb_clf.predict(X_test)
```

### 6.4 Avaliação dos Modelos

Os modelos foram avaliados usando Acurácia, Relatório de Classificação (precisão, recall, F1-score) e Matriz de Confusão.

```python
from sklearn.metrics import accuracy_score, classification_report, confusion_matrix

print("Acurácia (Regressão Logística):", accuracy_score(y_test, y_pred_log_reg))
print(classification_report(y_test, y_pred_log_reg))
# ... (similar para outros modelos)
```

## 7. Análises Avançadas

### 7.1 Análise de Componentes Principais (PCA)

PCA foi aplicado às features de percentuais de atraso e cancelamento para reduzir a dimensionalidade e visualizar a variância nos dados.

```python
from sklearn.decomposition import PCA

pca_features = ['Percentuais_de_Cancelamentos', 'Percentuais_de_Atrasos_superiores_a_30_minutos', 'Percentuais_de_Atrasos_superiores_a_60_minutos']
# ... (código para preparar dados, aplicar PCA e visualizar variância explicada e componentes)
```

### 7.2 Clusterização com K-Means

K-Means foi utilizado para agrupar as operações de voo com base em suas características de atraso (utilizando os dados padronizados do PCA). O método do cotovelo ajudou a determinar um número razoável de clusters.

```python
from sklearn.cluster import KMeans

# ... (código para aplicar K-Means, método do cotovelo e visualizar clusters nos componentes principais)
```

## 8. Conclusões

### 8.1 Principais Fatores de Atraso Identificados

A análise exploratória e a importância das features dos modelos de árvore indicaram que:
*   **Empresas Aéreas Específicas:** Algumas companhias apresentaram consistentemente maiores percentuais de atraso.
*   **Aeroportos de Origem/Destino:** Certos aeroportos (provavelmente os mais movimentados ou com infraestrutura mais crítica) foram associados a maiores taxas de atraso.
*   **Número de Etapas Previstas:** Embora não tenha sido o fator mais dominante nos modelos simples, pode ter alguma influência indireta.

### 8.2 Desempenho dos Modelos Preditivos

Os modelos de machine learning, especialmente os de ensemble como Random Forest e Gradient Boosting, apresentaram um desempenho razoável na previsão de atrasos significativos, superando modelos mais simples. No entanto, a previsibilidade de atrasos é inerentemente complexa devido a fatores não capturados nos dados (ex: meteorologia em tempo real, problemas técnicos inesperados).

### 8.3 Insights da Clusterização e PCA

*   **PCA:** A análise de componentes principais ajudou a condensar as informações das diferentes métricas de atraso/cancelamento em menos dimensões, facilitando a visualização e o uso em algoritmos como K-Means.
*   **K-Means:** A clusterização permitiu identificar grupos de operações de voo com perfis de atraso distintos. Por exemplo, um cluster pode representar operações com alta pontualidade, enquanto outro pode agrupar operações cronicamente atrasadas. A análise das características médias de cada cluster (ex: quais empresas, rotas predominam em clusters problemáticos) pode fornecer insights valiosos para as companhias.

### 8.4 Limitações do Estudo

*   **Dados Agregados Mensalmente:** Os dados são percentuais mensais por rota/voo, o que limita a análise de eventos de atraso individuais e suas causas imediatas.
*   **Ausência de Fatores Externos:** Os dados não incluem informações cruciais como condições meteorológicas detalhadas, tráfego aéreo em tempo real, ou problemas técnicos específicos, que são grandes causadores de atrasos.
*   **Período Limitado:** A análise se baseou em dados de um único mês (Dezembro de 2024), o que pode não capturar sazonalidades ou tendências de longo prazo.

### 8.5 Sugestões para Trabalhos Futuros

*   Analisar dados de um período mais longo para identificar tendências e sazonalidades.
*   Incorporar dados externos, como informações meteorológicas (METAR/TAF), dados de tráfego aéreo, e notícias sobre eventos que possam impactar o sistema aéreo.
*   Utilizar dados mais granulares (ex: dados de voos individuais com horários reais de partida/chegada e motivos de atraso, se disponíveis publicamente).
*   Explorar modelos de séries temporais para prever volumes de atraso.
*   Desenvolver modelos mais sofisticados, considerando interações complexas entre features.

## 9. Apêndice: Gráficos Gerados

*(Esta seção pode ser preenchida com os principais gráficos gerados no notebook, ou referenciar diretamente o notebook para visualização. Exemplos incluem: histogramas de atraso, barras de atraso por empresa/aeroporto, gráfico de cotovelo do K-Means, scatter plot dos clusters em componentes principais, etc.)*

**Exemplo de como referenciar um gráfico que estaria no notebook:**

*Gráfico 1: Distribuição do Percentual de Atrasos Superiores a 30 Minutos (Ver célula X do notebook `analise_atrasos_voos.ipynb`)*

*Gráfico 2: Média de Atrasos por Empresa Aérea (Ver célula Y do notebook `analise_atrasos_voos.ipynb`)*

---

Fim da Documentação.

