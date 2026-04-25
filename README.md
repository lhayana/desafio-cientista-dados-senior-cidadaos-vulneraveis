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
