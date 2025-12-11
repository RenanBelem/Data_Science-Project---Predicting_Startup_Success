# 🚀 Predicting Startup Success: Data Science & Machine Learning

> **Projeto de Ciência de Dados - PUCPR** \>

Este repositório contém o código, apresentações e documentação de um projeto completo de Ciência de Dados focado na previsão do sucesso de startups. O objetivo é utilizar dados históricos para classificar se uma startup será **adquirida** (*acquired*) ou **fechada** (*closed*).

## 👥 Autores (Equipe 4)

  * Guilherme Schwarz
  * Júlia Cristina Moreira da Silva
  * Matheus Francisco Trevisan Del Zotto
  * Renan Belem Biavati

-----

## 📂 Estrutura do Projeto

O projeto foi dividido em duas grandes etapas:

### 1\. Etapa de Checkpoint (Análise Exploratória)

Foco no entendimento dos dados, limpeza inicial e validação de hipóteses de negócio.

  * **Arquivos:** `project_checkpoint.ipynb`, `checkpoint_presentation.pdf`
  * **Atividades:**
      * Carregamento e limpeza do dataset (`startup data.csv`).
      * Análise Univariada (distribuições, assimetria, curtose).
      * Análise Multivariada e teste de hipóteses (ex: impacto de crises econômicas, financiamento por setor).
      * Engenharia de Atributos inicial (criação de `is_technology`, `age_at_closing`).

### 2\. Etapa Final (Modelagem Preditiva)

Foco na construção de pipelines de Machine Learning, balanceamento de classes e seleção de atributos para maximizar métricas de classificação.

  * **Arquivos:** `final_project.ipynb`, `final_project_presentation.pdf`, `project_manuscript.pdf`
  * **Atividades:**
      * Pré-processamento avançado e *encoding*.
      * Implementação de Pipelines com `imblearn`.
      * Comparação de 19 combinações de modelos, seletores de \<em\>features\</em\> e balanceadores.
      * Validação Cruzada (*Stratified K-Fold*).

-----

## 📊 Sobre o Dataset

O conjunto de dados (`startup data.csv`) contém informações sobre aproximadamente **923 startups** norte-americanas fundadas entre 1998 e 2013.

  * **Target:** `status` (Binário: `acquired` ou `closed`).
  * **Desbalanceamento:** \~64.7% Acquired vs \~35.3% Closed.
  * **Atributos Principais:**
      * **Numéricos:** `funding_total_usd`, `milestones`, `relationships`, `age_at_closing`.
      * **Categóricos:** `state_code`, `category_code`, `is_CA` (Califórnia), `is_NY` (Nova Iorque).
      * **Temporais:** Datas de fundação, primeiro financiamento e encerramento.

-----

## 🛠️ Metodologia e Tecnologias

O projeto utilizou **Python** e as bibliotecas `pandas`, `seaborn`, `matplotlib`, `scikit-learn` e `imblearn`.

### Pipelines de Machine Learning

Para garantir a robustez e evitar *data leakage*, foram testadas combinações automatizadas de:

1.  **Balanceamento de Classes:**
      * `RandomUnderSampler` (RUS)
      * `SMOTE` (Oversampling)
2.  **Seleção de Atributos:**
      * `PCA` (Principal Component Analysis)
      * `RFE` (Recursive Feature Elimination)
      * `SelectKBest` (Univariado)
3.  **Modelos de Classificação:**
      * Random Forest
      * Gradient Boosting
      * Logistic Regression
      * Support Vector Machine (SVM)
      * K-Nearest Neighbors (KNN)

### Métricas de Avaliação

Devido ao desbalanceamento das classes, a métrica principal de decisão foi o **F1-Score (Weighted)**, apoiada por Acurácia, Precisão, Recall e Tempo de Execução.

-----

## 📈 Principais Resultados e Insights

### Descobertas da Análise Exploratória (EDA)

  * **Impacto de Crises:** Houve um aumento significativo no fechamento de startups nos anos seguintes à crise de 2008.
  * **Tech vs Non-Tech:** Empresas de tecnologia recebem, em média, mais financiamento que as de outros setores.
  * **Marcos Iniciais:** Atingir o primeiro marco (*milestone*) cedo não mostrou correlação forte com o sucesso final da empresa.

### Desempenho dos Modelos

A tabela abaixo resume os melhores e piores desempenhos encontrados nos experimentos:

| Modelo | Balanceamento | Seleção | F1-Score | Tempo (s) | Observação |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Random Forest** | SMOTE | RFE | **0.99** | 805s | Alto custo computacional |
| **Log. Regression**| RandomUnderSampler| SelectKBest | **0.99** | **0.63s** | **Melhor Custo-Benefício** |
| SVM | RandomUnderSampler| PCA | 0.81 | 1.16s | PCA prejudicou o desempenho |
| KNN | SMOTE | PCA | 0.78 | 1.06s | Pior combinação |

> **Conclusão:** O uso de **PCA reduziu o desempenho** em quase todos os cenários, indicando que a interpretabilidade e a variância original das *features* eram cruciais. Pipelines mais simples (Regressão Logística + SelectKBest) atingiram resultados de estado-da-arte com fração do custo computacional de modelos complexos (como Gradient Boosting + RFE).

-----

## 🔧 Como Executar

1.  **Pré-requisitos:**
    Certifique-se de ter instalado as bibliotecas listadas no início dos notebooks:

    ```bash
    pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn
    ```

2.  **Arquivos:**

      * Coloque o arquivo `startup data.csv` no mesmo diretório dos notebooks.
      * Execute o `final_project.ipynb` para reproduzir o pipeline de Machine Learning completo.
      * Execute o `project_checkpoint.ipynb` para visualizar a análise exploratória e os gráficos iniciais.

-----

## 📄 Conteúdo dos Arquivos

  * `project_manuscript.pdf`: Artigo científico completo formatado (IEEE style) descrevendo todo o projeto, fundamentação teórica e discussão aprofundada.
  * `checkpoint_presentation.pdf`: Slides apresentando a caracterização do dataset e os insights visuais da primeira etapa.
  * `final_project_presentation.pdf`: Slides finais com a arquitetura dos pipelines, análise comparativa dos modelos e conclusões.
  * `final_project.ipynb`: Notebook principal com o código de treinamento, validação e teste dos modelos.
  * `project_checkpoint.ipynb`: Notebook com a limpeza de dados e geração dos gráficos de EDA.
