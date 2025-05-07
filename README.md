# Análise de Atrasos em Voos Domésticos no Brasil

## Descrição do Projeto

Este projeto realiza uma análise aprofundada dos dados de atrasos em voos domésticos no Brasil, utilizando informações públicas da Agência Nacional de Aviação Civil (ANAC). O objetivo principal é identificar os principais fatores que contribuem para os atrasos e cancelamentos de voos, além de explorar a aplicação de técnicas de machine learning para prever a ocorrência de atrasos significativos. A análise visa fornecer insights valiosos que possam auxiliar passageiros e companhias aéreas no planejamento e na mitigação dos impactos causados por esses eventos.

## Problemática Abordada

Atrasos e cancelamentos de voos são problemas recorrentes que afetam milhões de passageiros anualmente, gerando custos financeiros, perda de tempo e frustração. Compreender as causas raízes desses problemas através da análise de dados é fundamental para desenvolver estratégias eficazes de minimização.

## Fonte dos Dados

Os dados utilizados neste projeto foram obtidos do portal de Dados Abertos da Agência Nacional de Aviação Civil (ANAC), referentes aos percentuais de atrasos e cancelamentos de voos para o mês de Dezembro de 2024. Especificamente, foram utilizados os arquivos "Anexo I.csv", "Anexo II.csv" e "Anexo III.csv".

## Principais Análises e Técnicas Utilizadas

O projeto foi desenvolvido em um Jupyter Notebook (`analise_atrasos_voos.ipynb`) e abrange as seguintes etapas:

1.  **Preparação do Ambiente e Carregamento dos Dados:** Importação das bibliotecas Python necessárias (Pandas, Matplotlib, Seaborn, Scikit-learn) e carregamento dos datasets.
2.  **Limpeza e Transformação dos Dados:** Tratamento de valores ausentes, conversão de tipos de dados (especialmente colunas de percentuais que utilizam vírgula como separador decimal) e renomeação de colunas para facilitar a manipulação.
3.  **Análise Exploratória de Dados (EDA):**
    *   Cálculo de estatísticas descritivas.
    *   Visualização da distribuição de atrasos.
    *   Identificação das empresas aéreas com maiores e menores índices de atraso/cancelamento.
    *   Análise de aeroportos de origem e destino com maior incidência de atrasos.
4.  **Engenharia de Features:**
    *   Criação de uma variável alvo para modelagem (ex: `Atraso_Significativo`, indicando atrasos superiores a 30 minutos).
    *   Codificação de variáveis categóricas (ex: Empresa Aérea, Aeroportos) utilizando Label Encoding.
5.  **Modelagem Preditiva com Machine Learning:**
    *   Divisão dos dados em conjuntos de treino e teste.
    *   Aplicação e avaliação de modelos de classificação para prever atrasos:
        *   Regressão Logística
        *   Árvore de Decisão (com análise de importância das features)
        *   Modelos de Ensemble: Random Forest e Gradient Boosting.
    *   Métricas de avaliação: Acurácia, Relatório de Classificação, Matriz de Confusão.
6.  **Técnicas Avançadas de Análise:**
    *   **Análise de Componentes Principais (PCA):** Para redução de dimensionalidade e identificação dos principais eixos de variação nos dados de atraso.
    *   **Clusterização com K-Means:** Para agrupar voos ou operações com características de atraso semelhantes, utilizando o método do cotovelo para determinar o número ótimo de clusters.

## Tecnologias Utilizadas

*   **Linguagem de Programação:** Python 3
*   **Principais Bibliotecas:**
    *   Jupyter Notebook
    *   Pandas (para manipulação e análise de dados)
    *   NumPy (para operações numéricas)
    *   Matplotlib e Seaborn (para visualização de dados)
    *   Scikit-learn (para machine learning: pré-processamento, modelagem, avaliação, PCA, K-Means)

## Como Executar o Projeto

1.  Clone este repositório.
2.  Certifique-se de ter o Python 3 e o Jupyter Notebook instalados.
3.  Instale as bibliotecas listadas acima. Um arquivo `requirements.txt` pode ser gerado e utilizado:
    ```bash
    pip install -r requirements.txt 
    ```
    (Nota: `requirements.txt` será adicionado posteriormente)
4.  Coloque os arquivos de dados da ANAC (`Anexo I.csv`, `Anexo II.csv`, `Anexo III.csv`) no diretório `/home/ubuntu/projeto_atrasos_voos/` (ou ajuste os caminhos no notebook).
5.  Abra e execute o notebook `analise_atrasos_voos.ipynb` em um ambiente Jupyter.

## Documentação Detalhada

Para uma explicação mais aprofundada sobre cada etapa do projeto, incluindo a coleta de dados, a modelagem realizada e as conclusões detalhadas, consulte o arquivo [DOCUMENTACAO.md](DOCUMENTACAO.md).



--

*Este projeto foi desenvolvido como parte de uma atividade prática, visando aplicar conhecimentos em análise de dados e machine learning para solucionar uma problemática real.*

