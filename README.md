# 🌦️ Pipeline ETL — Dados Meteorológicos de Votuporanga

Pipeline automatizado de coleta, transformação e armazenamento de dados meteorológicos da cidade de **Votuporanga/SP**, orquestrado com Apache Airflow e containerizado com Docker.

---

## 🎯 Objetivo

Construir um pipeline ETL completo que:

- **Extrai** dados meteorológicos de Votuporanga via API
- **Transforma** e padroniza os dados coletados
- **Carrega** as informações em um banco de dados PostgreSQL
- **Orquestra** todo o fluxo com Apache Airflow de forma agendada e monitorada

---

## 🏛️ Arquitetura

```
pipeline_etl_weather_votu/
├── dags/                   ← DAGs do Apache Airflow
├── notebooks/              ← Notebooks de exploração e análise
├── src/                    ← Scripts Python do pipeline (extract, transform, load)
├── docker-compose.yaml     ← Orquestração dos containers (Airflow + Postgres)
├── main.py                 ← Ponto de entrada do pipeline
├── pyproject.toml          ← Dependências do projeto
└── README.md
```

### Fluxo do Pipeline

```
API Meteorológica
      ↓
   Extract (src/)
      ↓
   Transform (src/)
      ↓
   Load → PostgreSQL
      ↓
   Airflow DAG (agendamento + monitoramento)
```

---

## 🛠️ Tech Stack

| Tecnologia | Função |
|---|---|
| **Python** | Linguagem principal do pipeline |
| **Apache Airflow** | Orquestração e agendamento dos DAGs |
| **PostgreSQL** | Armazenamento dos dados transformados |
| **Docker / Docker Compose** | Containerização do ambiente completo |

---

## 🚀 Como Rodar

### Pré-requisitos

- [Docker](https://docs.docker.com/get-docker/) instalado e rodando
- [Docker Compose](https://docs.docker.com/compose/install/) disponível

### 1. Clone o repositório

```bash
git clone https://github.com/mateusvicentin/pipeline_etl_weather_votu.git
cd pipeline_etl_weather_votu
```

### 2. Suba os containers

```bash
docker-compose up -d
```

Esse comando inicializa:
- **Airflow Webserver** → `http://localhost:8080`
- **Airflow Scheduler** → agendamento dos DAGs
- **PostgreSQL** → banco de dados para os dados meteorológicos

### 3. Acesse o Airflow

```
URL:      http://localhost:8080
Usuário:  airflow
Senha:    airflow
```

### 4. Ative a DAG

No painel do Airflow, localize a DAG do pipeline meteorológico e ative-a. O pipeline irá executar automaticamente conforme o agendamento configurado, ou você pode dispará-lo manualmente clicando em **"Trigger DAG"**.

### 5. Executar manualmente (opcional)

```bash
python main.py
```

---

## 📊 Dados Coletados

Os dados meteorológicos referem-se à cidade de **Votuporanga, São Paulo, Brasil**, e incluem variáveis como temperatura, umidade, precipitação e demais métricas climáticas disponibilizadas pela fonte da API.

---

## 📁 Estrutura Detalhada

```
config/
└── .env                    ← Chave API, Database, User do Database, Senha Database

dags/
└── weather_dag.py          ← Definição das tasks e dependências no Airflow

src/
├── extract_data.py         ← Coleta dos dados via API meteorológica
├── transform_data.py       ← Limpeza e transformação dos dados
└── load_data.py            ← Inserção no banco PostgreSQL

notebooks/
└── *.ipynb                 ← Exploração e validação dos dados

docker-compose.yaml         ← Serviços: Airflow + PostgreSQL
main.py                     ← Execução manual do pipeline completo
pyproject.toml              ← Configuração de dependências Python
```

---

## 🔍 Monitoramento

Com o Airflow rodando, você pode:

- Visualizar o status de cada execução (run) da DAG
- Inspecionar logs de cada task individualmente
- Reprocessar execuções com falha
- Acompanhar o histórico de runs no gráfico de Gantt

Acesse tudo em: `http://localhost:8080`

---

## 🗄️ Banco de Dados

Os dados são armazenados no **PostgreSQL** provisionado via Docker. Para conectar com uma ferramenta como DBeaver ou TablePlus:

---

## 📦 Dependências

As dependências Python estão definidas em `pyproject.toml`. Para instalar localmente (fora do Docker):

```bash
pip install -e .
```

---

## 👤 Autor

**Mateus Vicentin**
[github.com/mateusvicentin](https://github.com/mateusvicentin)


