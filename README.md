# Desafio Cientista de Dados Sênior - Cidadãos Vulneráveis (Prefeitura do Rio)

## Visão Geral
Este repositório contém a solução desenvolvida para o "Desafio Cientista de Dados Sênior" da Prefeitura do Rio de Janeiro. O projeto visa analisar e aprimorar a resposta a demandas urbanas da **Central de Atendimento 1746**.

## Estrutura do Projeto

O fluxo de dados foi consolidado na pasta `notebooks/`, dividida de forma lógica em três etapas principais:

* **`01_analise_apis_clima.ipynb`**: Correspondente a Parte 1: Análise Exploratória com APIs Externas
* **`02_modelagem_resolucao.ipynb`**: Correspondente a Parte 2: Modelagem Preditiva - Resolução de Chamados
* **`03_sistema_priorizacao.ipynb`**: Correspondente a Parte 3: Sistema de Priorização

## Tecnologias e Bibliotecas Utilizadas
* **Linguagem**: Python
* **Manipulação de Dados**: `numpy`, `pandas`
* **Visualização de Dados**: `matplotlib`, `seaborn`
* **Integração de APIs climáticas**: `requests`, `requests-cache`, `openmeteo-requests`, `retry-requests`
* **Conexão com BigQuery**: `basedosdados`
* **Modelagem Preditiva**: `scikit-learn`, `lightgbm` (e artefatos `catboost`)
* **Gestão de Configuração**: `python-dotenv`

## Como Rodar

Caso queira replicar as análises ou treinar os modelos em sua máquina:

1. **Configuração do Virtual Environment (Recomendado)**
   É aconselhado rodar a aplicação num ambiente virtual para isolar as dependências.
   ```bash
   python -m venv .venv
   # Ativando no Windows
   .venv\Scripts\activate
   # Ativando no Linux/Mac
   source .venv/bin/activate
   ```

2. **Instalação das Dependências**
   ```bash
   pip install -r requirements.txt
   ```

3. **Configuração de Variáveis de Caminho/Ambiente**
   Para conseguir consultar as informações dentro do pacote `basedosdados`, você deve possuir um projeto no Google Cloud (GCP) com o faturamento (billing) ativo ou cota gratuita disponível. Crie um arquivo `.env` na raiz do projeto com o seguinte formato:
   ```env
   BILLING_PROJECT_ID=id-do-seu-projeto-gcp
   ```

4. **Servidor Jupyter**
   Com tudo configurado, levante a interface dos notebooks:
   ```bash
   jupyter notebook
   # Acesse os arquivos presentes na pasta notebooks/ e rode as células sequencialmente.
   ```

## Principais Resultados

**1. Análise Exploratória (Parte 1)**

- Temperatura máxima é o preditor climático mais relevante para volume de chamados, superando a chuva pontual
- O efeito da chuva se manifesta com defasagem: a chuva acumulada dos últimos 3 dias é mais preditiva do que a precipitação do dia
- Fins de semana reduzem o volume em até 40% — sinal de que a demanda é real mas o registro é reprimido

**2. Padrões Geoespaciais (Parte 2)**

- AP 5 (Zona Oeste) e AP 3 (Zona Norte) concentram maior demanda per capita e maior tempo mediano de resolução — evidência de desigualdade estrutural de serviço
- Comunidades vulneráveis acionam menos o canal 1746 do que sua densidade habitacional sugeriria, indicando que há sub-notificação

**3. Modelo Preditivo (Parte 2)**

- LightGBM (previsão de volume de chamados): R² de 0,827 no conjunto de teste (2024) — o modelo explica 83% da variação diária de demanda por região e tipo
- XGBoost (previsão de resolução em 7 dias): Recall de 0,999, F1 de 0,886 e AUC-ROC de 0,868 no conjunto de teste — priorizado pelo Recall por ser a métrica mais relevante no contexto de gestão pública, onde deixar passar um atraso tem custo maior do que um alerta desnecessário

**4. Sistema de Priorização (Parte 3)**

- Score multidimensional combinando risco do modelo (45%), equidade territorial (20%), urgência por tipo (20%), clima prospectivo (10%) e backlog (5%)
- Comparado à seleção aleatória de 20% dos chamados, o score captura 2,52x mais atrasos com a mesma capacidade operacional
- Recall de 50,3% vs. 18,8% do aleatório: priorizando apenas 1 em cada 5 chamados, o score antecipa metade de todos os atrasos do município
