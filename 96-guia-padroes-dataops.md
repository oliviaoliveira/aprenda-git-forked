# 📐 Guia de Padrões e Boas Práticas Git para DataOps

Um guia completo de organização, estrutura e padrões para projetos de dados usando Git.

## 🎯 Índice

1. [Conventional Commits - Padrão de Mensagens](#conventional-commits)
2. [Estrutura de Branches para DataOps](#estrutura-de-branches)
3. [Estrutura de Repositórios](#estrutura-de-repositórios)
4. [Nomenclatura e Organização](#nomenclatura)
5. [Versionamento de Dados](#versionamento-de-dados)
6. [.gitignore para DataOps](#gitignore-dataops)
7. [Documentação Obrigatória](#documentação)
8. [Code Review e Qualidade](#code-review)
9. [Workflows DataOps](#workflows-dataops)
10. [Segurança e Compliance](#segurança)
11. [Checklist de Projeto](#checklist)

---

## 📝 Conventional Commits - Padrão de Mensagens {#conventional-commits}

### Por Que Usar Padrão?

✅ **Histórico legível** - Fácil entender o que mudou
✅ **Automatização** - Gerar CHANGELOGs automaticamente
✅ **Semantic Versioning** - Determinar versões (1.2.3)
✅ **Rastreabilidade** - Encontrar mudanças específicas
✅ **Comunicação clara** - Time todo entende

### Formato Padrão

```
<tipo>(<escopo>): <descrição curta>

<corpo opcional - detalhes>

<rodapé opcional - breaking changes, issues>
```

### Tipos de Commit

#### Para Código/Scripts:

```bash
feat:      Nova funcionalidade
fix:       Correção de bug
refactor:  Refatoração sem mudar comportamento
perf:      Melhoria de performance
style:     Formatação, ponto e vírgula, etc
test:      Adicionar ou corrigir testes
docs:      Documentação apenas
build:     Sistema de build (npm, pip, etc)
ci:        CI/CD (GitHub Actions, Jenkins)
chore:     Manutenção (atualizar deps, configs)
revert:    Reverter commit anterior
```

#### Específicos para DataOps:

```bash
data:      Mudanças em datasets ou schemas
pipeline:  Mudanças em pipelines de dados
model:     Mudanças em modelos (ML, estatísticos)
schema:    Mudanças em schemas de dados
query:     Mudanças em queries SQL/NoSQL
etl:       Mudanças em processos ETL/ELT
viz:       Mudanças em visualizações/dashboards
config:    Mudanças em configurações de infra
```

### Exemplos Práticos

#### ✅ Bons Exemplos:

```bash
# Código
feat(api): adiciona endpoint de autenticação
fix(pipeline): corrige erro de encoding em CSV
refactor(etl): otimiza processo de extração do S3
perf(query): adiciona índice na tabela de vendas

# Dados
data(vendas): adiciona dataset de Q4 2025
schema(usuarios): adiciona campo email_verificado
pipeline(vendas): implementa validação de dados
model(churn): atualiza modelo de Random Forest para XGBoost

# Documentação
docs(readme): adiciona guia de instalação
docs(api): documenta endpoints de relatórios

# Infraestrutura
ci(github): adiciona workflow de testes
config(airflow): atualiza configuração de memória
build(docker): otimiza imagem para produção

# Breaking Changes
feat(api)!: remove endpoint legado de clientes

BREAKING CHANGE: O endpoint /api/v1/clients foi removido.
Use /api/v2/customers no lugar.
```

#### ❌ Exemplos Ruins:

```bash
# Muito vago
"update"
"fix"
"changes"
"stuff"

# Sem tipo
"adiciona validação"
"corrige bug"

# Muito longo
"feat: adiciona nova funcionalidade super importante que valida dados e envia email e atualiza dashboard"

# Sem contexto
"fix: bug"
"feat: feature"
```

### Escopos Sugeridos para DataOps

```bash
# Por camada de dados
(bronze)      Dados brutos
(silver)      Dados limpos/transformados
(gold)        Dados analíticos/agregados

# Por domínio
(vendas)      Domínio de vendas
(marketing)   Domínio de marketing
(financeiro)  Domínio financeiro
(clientes)    Domínio de clientes

# Por componente
(airflow)     Apache Airflow
(dbt)         dbt (Data Build Tool)
(spark)       Apache Spark
(snowflake)   Snowflake
(redshift)    Amazon Redshift
(databricks)  Databricks

# Por tipo de ativo
(dashboard)   Dashboards/Viz
(report)      Relatórios
(alert)       Alertas/Monitoramento
```

### Estrutura Completa de Commit

```bash
# Commit com tudo
git commit -m "feat(pipeline): adiciona validação de qualidade de dados

- Implementa validação de nulos
- Adiciona checagem de tipos de dados
- Cria alertas para dados fora do padrão
- Integra com Great Expectations

Refs: JIRA-123
Reviewed-by: Maria Silva"
```

### Template de Commit

Crie arquivo `.gitmessage`:

```bash
# <tipo>(<escopo>): <descrição curta>
# |<----  Máximo 50 caracteres  ---->|

# <corpo - explicação detalhada>
# |<----  Máximo 72 caracteres por linha  ---->|

# <rodapé>
# Refs: #issue
# Reviewed-by: Nome
# BREAKING CHANGE: descrição

# Tipos disponíveis:
# feat:     Nova funcionalidade
# fix:      Correção de bug
# data:     Mudanças em dados
# pipeline: Mudanças em pipeline
# model:    Mudanças em modelos
# schema:   Mudanças em schema
# docs:     Documentação
# refactor: Refatoração
# test:     Testes
# ci:       CI/CD
# config:   Configuração
```

Configure:
```bash
git config --global commit.template ~/.gitmessage
```

---

## 🌿 Estrutura de Branches para DataOps {#estrutura-de-branches}

### GitFlow Adaptado para DataOps

```
production (main)
    ↓
staging (develop)
    ↓
feature/*       Novas funcionalidades/pipelines
    ↓
hotfix/*        Correções urgentes em produção
    ↓
data/*          Mudanças em dados/schemas
    ↓
experiment/*    Experimentos/análises temporárias
```

### Branches Principais

#### 1. **production** (ou **main**)
```
✅ Código em produção
✅ Sempre estável
✅ Deploy automático
✅ Protected branch
✅ Requer aprovação
```

**Regras:**
- ❌ Nunca commit direto
- ✅ Apenas via Pull Request
- ✅ CI/CD deve passar
- ✅ Code review obrigatório
- ✅ Testes 100% passing

#### 2. **staging** (ou **develop**)
```
✅ Ambiente de staging
✅ Integração contínua
✅ Testes antes de produção
✅ Validação de stakeholders
```

**Regras:**
- ✅ Merge de features aqui primeiro
- ✅ Testes de integração
- ✅ Validação de dados
- ✅ QA review

### Branches de Trabalho

#### **feature/\*** - Novas Features

```bash
# Nomenclatura
feature/nome-da-feature
feature/DAT-123-pipeline-vendas
feature/implementa-modelo-churn

# Exemplos
feature/vendas-pipeline-mensal
feature/DAT-456-dashboard-executivo
feature/integracao-salesforce
```

**Ciclo de vida:**
```bash
# Criar
git checkout staging
git pull
git checkout -b feature/DAT-123-pipeline-vendas

# Desenvolver
git add .
git commit -m "feat(pipeline): implementa extração de vendas"

# Finalizar
git push origin feature/DAT-123-pipeline-vendas
# Abrir PR para staging
# Após merge, deletar branch
```

#### **hotfix/\*** - Correções Urgentes

```bash
# Nomenclatura
hotfix/nome-do-bug
hotfix/BUG-789-erro-calculo

# Exemplos
hotfix/corrige-encoding-utf8
hotfix/BUG-789-erro-agregacao-vendas
```

**Ciclo:**
```bash
# Criar DIRETO da production
git checkout production
git pull
git checkout -b hotfix/BUG-789-erro-agregacao

# Corrigir
git commit -m "fix(vendas): corrige cálculo de agregação"

# Merge em production E staging
git checkout production
git merge hotfix/BUG-789-erro-agregacao
git checkout staging
git merge hotfix/BUG-789-erro-agregacao
```

#### **data/\*** - Mudanças em Dados

```bash
# Nomenclatura
data/nome-da-mudanca
data/adiciona-dataset-q4
data/schema-v2-usuarios

# Exemplos
data/adiciona-vendas-2025
data/migracao-schema-usuarios-v2
data/corrige-tipos-coluna-data
```

**Uso:**
```bash
# Para mudanças em schemas, seeds, fixtures
git checkout -b data/schema-v2-clientes

# Commits específicos
git commit -m "schema(clientes): adiciona campo cpf_validado"
git commit -m "data(clientes): adiciona dataset de teste"
```

#### **experiment/\*** - Experimentos

```bash
# Nomenclatura
experiment/nome-experimento
experiment/EXP-123-teste-modelo-xgboost

# Exemplos
experiment/teste-feature-engineering
experiment/analise-outliers-vendas
experiment/poc-dbt-incremental
```

**Características:**
- ⏰ Temporário
- 🧪 Exploratório
- 🗑️ Pode ser deletado depois
- 📊 Para notebooks/análises

#### **model/\*** - Modelos ML

```bash
# Nomenclatura
model/nome-do-modelo
model/churn-v2
model/recomendacao-produtos

# Exemplos
model/churn-random-forest-v3
model/segmentacao-clientes-kmeans
model/previsao-demanda-prophet
```

### Nomenclatura de Branches

#### ✅ Boas Práticas:

```bash
# Formato
<tipo>/<descrição-kebab-case>
<tipo>/<ticket>-<descrição>

# Exemplos
feature/pipeline-vendas-diario
feature/DAT-123-etl-vendas
hotfix/corrige-timezone-logs
data/schema-v2-produtos
experiment/teste-apache-iceberg
model/churn-xgboost-v2
```

#### ❌ Evite:

```bash
# Muito genérico
feature/update
feature/fix

# Com espaços ou caracteres especiais
feature/Pipeline de Vendas
feature/vendas_pipeline

# Muito longo
feature/implementa-novo-pipeline-de-vendas-com-validacao-e-alertas

# Sem contexto
feature/123
feature/test
```

### Proteção de Branches

Configure no GitHub/GitLab:

```yaml
# production
protections:
  - require_pull_request: true
  - require_reviews: 2
  - require_status_checks: true
  - require_up_to_date: true
  - no_force_push: true
  - no_delete: true

# staging
protections:
  - require_pull_request: true
  - require_reviews: 1
  - require_status_checks: true
```

---

## 📁 Estrutura de Repositórios {#estrutura-de-repositórios}

### Mono-repo vs Multi-repo

#### **Mono-repo** (Recomendado para DataOps)

```
data-platform/
├── pipelines/          Todos os pipelines
├── models/             Todos os modelos
├── transformations/    Transformações dbt
├── config/             Configurações
└── docs/               Documentação
```

**Vantagens:**
- ✅ Versionamento unificado
- ✅ Refatoração fácil
- ✅ Dependências claras
- ✅ CI/CD simplificado

#### **Multi-repo** (Para times grandes)

```
vendas-pipeline/        Repositório de vendas
marketing-pipeline/     Repositório de marketing
ml-models/             Repositório de modelos
data-quality/          Repositório de qualidade
```

**Vantagens:**
- ✅ Autonomia de times
- ✅ Deploys independentes
- ✅ Controle de acesso granular

### Estrutura Padrão de Projeto DataOps

```
meu-projeto-data/
│
├── .github/                          # GitHub configs
│   ├── workflows/                    # GitHub Actions
│   │   ├── ci.yml                   # CI pipeline
│   │   ├── cd-staging.yml           # Deploy staging
│   │   └── cd-production.yml        # Deploy prod
│   ├── PULL_REQUEST_TEMPLATE.md     # Template de PR
│   └── ISSUE_TEMPLATE/              # Templates de issues
│
├── airflow/                          # Apache Airflow
│   ├── dags/                        # DAGs
│   │   ├── vendas_diario.py
│   │   ├── etl_clientes.py
│   │   └── ml_pipeline.py
│   ├── plugins/                     # Plugins customizados
│   ├── config/                      # Configurações
│   └── tests/                       # Testes de DAGs
│
├── dbt/                              # dbt (Data Build Tool)
│   ├── models/                      # Modelos SQL
│   │   ├── staging/                # Camada bronze/staging
│   │   ├── intermediate/           # Camada silver
│   │   └── marts/                  # Camada gold
│   ├── macros/                      # Macros reutilizáveis
│   ├── tests/                       # Testes de dados
│   ├── seeds/                       # Dados estáticos (CSV)
│   ├── snapshots/                   # Snapshots SCD
│   └── dbt_project.yml             # Configuração
│
├── notebooks/                        # Jupyter Notebooks
│   ├── exploratory/                 # Análises exploratórias
│   ├── experiments/                 # Experimentos
│   └── reports/                     # Relatórios
│
├── src/                              # Código fonte
│   ├── pipelines/                   # Pipelines ETL
│   │   ├── extract/
│   │   ├── transform/
│   │   └── load/
│   ├── models/                      # Modelos ML
│   │   ├── training/
│   │   ├── inference/
│   │   └── evaluation/
│   ├── utils/                       # Utilitários
│   └── config/                      # Configs em código
│
├── tests/                            # Testes
│   ├── unit/                        # Testes unitários
│   ├── integration/                 # Testes integração
│   └── fixtures/                    # Dados de teste
│
├── data/                             # Dados (NÃO commitar grandes arquivos)
│   ├── raw/                         # Dados brutos (samples)
│   ├── processed/                   # Dados processados
│   └── seeds/                       # Dados estáticos pequenos
│
├── sql/                              # Queries SQL
│   ├── ddl/                         # CREATE, ALTER, DROP
│   ├── dml/                         # INSERT, UPDATE, DELETE
│   └── queries/                     # SELECT queries
│
├── config/                           # Configurações
│   ├── dev.yml                      # Ambiente dev
│   ├── staging.yml                  # Ambiente staging
│   ├── production.yml               # Ambiente prod
│   └── schema.yml                   # Schemas de dados
│
├── docs/                             # Documentação
│   ├── architecture/                # Arquitetura
│   ├── runbooks/                    # Runbooks operacionais
│   ├── data_catalog/                # Catálogo de dados
│   └── decisions/                   # ADRs (Architecture Decision Records)
│
├── scripts/                          # Scripts auxiliares
│   ├── setup/                       # Setup ambiente
│   ├── migration/                   # Migrações de dados
│   └── utilities/                   # Utilitários
│
├── docker/                           # Docker
│   ├── Dockerfile
│   ├── docker-compose.yml
│   └── .dockerignore
│
├── .gitignore                        # Git ignore
├── .env.example                      # Exemplo de .env
├── README.md                         # Documentação principal
├── CONTRIBUTING.md                   # Guia de contribuição
├── CHANGELOG.md                      # Histórico de mudanças
├── requirements.txt                  # Dependências Python
├── pyproject.toml                    # Config Python (alternativa)
├── Makefile                          # Comandos úteis
└── VERSION                           # Versão do projeto
```

### Arquivos Essenciais

#### **README.md**

```markdown
# Nome do Projeto

## 📊 Descrição
Pipeline de dados de vendas que extrai, transforma e carrega dados...

## 🏗️ Arquitetura
[Diagrama da arquitetura]

## 🚀 Quick Start
\`\`\`bash
# Clone
git clone https://github.com/org/projeto.git

# Setup
make setup

# Run
make run
\`\`\`

## 📁 Estrutura
- `/airflow` - DAGs do Airflow
- `/dbt` - Modelos dbt
- `/src` - Código fonte

## 🧪 Testes
\`\`\`bash
make test
\`\`\`

## 🚢 Deploy
Ver [DEPLOY.md](docs/DEPLOY.md)

## 📖 Documentação
Ver [docs/](docs/)

## 👥 Time
- Data Engineer: João Silva
- Data Analyst: Maria Santos
```

#### **CONTRIBUTING.md**

```markdown
# Guia de Contribuição

## Workflow
1. Crie branch: `git checkout -b feature/sua-feature`
2. Comite: `git commit -m "feat: descrição"`
3. Push: `git push origin feature/sua-feature`
4. Abra Pull Request

## Padrões
- Conventional Commits
- Code review obrigatório
- Testes devem passar
- Documentar mudanças

## Code Review
- [ ] Código limpo e legível
- [ ] Testes incluídos
- [ ] Documentação atualizada
- [ ] CI passa
```

#### **CHANGELOG.md**

```markdown
# Changelog

## [2.1.0] - 2026-01-13
### Added
- Pipeline de vendas diário
- Dashboard executivo

### Fixed
- Correção de timezone em logs

### Changed
- Atualização do modelo de churn para XGBoost

## [2.0.0] - 2025-12-01
### Added
- Migração para dbt
- Implementação de data quality

### Breaking Changes
- Schema de clientes alterado
```

---

## 🏷️ Nomenclatura e Organização {#nomenclatura}

### Arquivos

#### ✅ Boas Práticas:

```python
# Lowercase com underscores (snake_case)
pipeline_vendas_diario.py
extract_salesforce.py
transform_clientes.py
model_churn_v2.py

# SQL
dim_clientes.sql
fct_vendas.sql
stg_erp_pedidos.sql

# Notebooks (data + descrição)
2026_01_13_analise_churn.ipynb
2025_12_exploracao_vendas_q4.ipynb

# Config
config_dev.yml
schema_vendas.json
```

#### ❌ Evite:

```python
# CamelCase ou mixed
PipelineVendas.py
Extract-Salesforce.py

# Nomes genéricos
pipeline.py
script.py
analysis.ipynb

# Espaços ou caracteres especiais
pipeline vendas.py
análise_vendas.py  # evite acentos
```

### Variáveis e Funções

```python
# Python: snake_case
def extract_salesforce_data():
    client_name = "Acme Corp"
    total_revenue = 1000000
    
# SQL: lowercase
SELECT
    client_id,
    client_name,
    total_revenue
FROM dim_clients

# Constantes: UPPER_CASE
DATABASE_URL = "postgresql://..."
MAX_RETRIES = 3
DEFAULT_BATCH_SIZE = 1000
```

### Tabelas e Schemas

```sql
-- Prefixos por camada
-- Bronze/Raw: raw_
raw_salesforce_accounts
raw_erp_orders

-- Silver/Staging: stg_
stg_salesforce_accounts
stg_erp_orders

-- Gold/Marts: dim_ (dimensões), fct_ (fatos)
dim_clients
dim_products
fct_sales
fct_orders

-- Agregações: agg_
agg_sales_daily
agg_revenue_monthly

-- Snapshots: snap_
snap_clients_scd2

-- Views: v_ ou vw_
v_sales_summary
vw_active_clients
```

### Colunas

```sql
-- Padrão: lowercase com underscore
client_id
client_name
created_at
updated_at

-- IDs: <tabela>_id
client_id
product_id
order_id

-- Datas: <evento>_at ou <evento>_date
created_at
updated_at
deleted_at
order_date
birth_date

-- Booleanos: is_ ou has_
is_active
is_deleted
has_subscription
has_children

-- Valores monetários: especificar moeda
revenue_usd
price_brl
cost_eur
```

---

## 📦 Versionamento de Dados {#versionamento-de-dados}

### Semantic Versioning para Dados

```
MAJOR.MINOR.PATCH
  2  . 1  .  3

MAJOR: Breaking changes (schema incompatível)
MINOR: Novos campos/tabelas (compatível)
PATCH: Correções de dados
```

### Exemplos:

```sql
-- v1.0.0 - Schema inicial
CREATE TABLE clients (
    id INTEGER PRIMARY KEY,
    name VARCHAR(100)
);

-- v1.1.0 - Adiciona campo (compatível)
ALTER TABLE clients ADD COLUMN email VARCHAR(100);

-- v2.0.0 - Breaking change (renomeia campo)
ALTER TABLE clients RENAME COLUMN name TO full_name;

-- v2.0.1 - Correção de dados
UPDATE clients SET email = LOWER(email);
```

### Versionamento de Modelos ML

```
models/
├── churn/
│   ├── v1/
│   │   ├── model.pkl
│   │   ├── metadata.json
│   │   └── metrics.json
│   ├── v2/
│   │   ├── model.pkl
│   │   ├── metadata.json
│   │   └── metrics.json
│   └── CHANGELOG.md
```

```json
// metadata.json
{
  "version": "2.1.0",
  "created_at": "2026-01-13",
  "algorithm": "XGBoost",
  "features": ["idade", "renda", "tempo_cliente"],
  "performance": {
    "accuracy": 0.92,
    "precision": 0.89,
    "recall": 0.91
  },
  "training_data": {
    "start_date": "2024-01-01",
    "end_date": "2025-12-31",
    "n_samples": 100000
  }
}
```

### Tags Git para Versões

```bash
# Criar tag de versão
git tag -a v2.1.0 -m "Release 2.1.0 - Novo pipeline de vendas"
git push origin v2.1.0

# Listar versões
git tag -l

# Checkout de versão específica
git checkout v2.0.0
```

### Versionamento em Arquivos

```python
# No código
__version__ = "2.1.0"

# No nome do arquivo (quando necessário)
schema_clientes_v2.json
modelo_churn_v3.pkl

# Em metadados
"""
Pipeline de Vendas
Version: 2.1.0
Last Updated: 2026-01-13
Author: João Silva
"""
```

---

## 🚫 .gitignore para DataOps {#gitignore-dataops}

### Template Completo

```gitignore
# ============================================
# Python
# ============================================
__pycache__/
*.py[cod]
*$py.class
*.so
.Python
venv/
env/
ENV/
.venv
pip-log.txt
pip-delete-this-directory.txt
.pytest_cache/
.coverage
htmlcov/
*.egg
*.egg-info/
dist/
build/
*.whl

# ============================================
# Jupyter Notebooks
# ============================================
.ipynb_checkpoints/
*/.ipynb_checkpoints/*
*.ipynb_checkpoints

# Notebook temporários
.jupyter/
.local/

# ============================================
# Dados (NÃO commitar dados grandes!)
# ============================================
data/raw/*
data/processed/*
!data/raw/.gitkeep
!data/processed/.gitkeep

# Datasets
*.csv
*.parquet
*.avro
*.orc
*.json
*.xml
*.xlsx
*.xls

# Exceto exemplos pequenos
!data/seeds/*.csv
!data/examples/*.json

# ============================================
# Modelos ML (arquivos grandes)
# ============================================
*.pkl
*.joblib
*.h5
*.hdf5
*.pb
*.ckpt
*.pth
*.pt
*.safetensors

# Exceto modelos pequenos ou metadados
!models/*/metadata.json
!models/*/metrics.json

# ============================================
# Logs e Outputs
# ============================================
logs/
*.log
*.out
*.err

# Airflow
airflow/logs/
airflow.db
airflow.cfg
webserver_config.py
unittests.cfg

# dbt
dbt/logs/
dbt/target/
dbt/dbt_packages/

# Spark
spark-warehouse/
metastore_db/
derby.log

# ============================================
# Credenciais e Secrets (NUNCA commitar!)
# ============================================
.env
.env.*
!.env.example
*.key
*.pem
*.crt
secrets/
credentials/
*.credentials
*secret*
*password*
*token*

# Cloud provider credentials
.aws/
.gcp/
.azure/

# Database connection strings
connection_strings.txt
db_credentials.json

# ============================================
# IDEs e Editores
# ============================================
# VS Code
.vscode/
*.code-workspace

# PyCharm
.idea/
*.iml

# Jupyter
.ipynb_checkpoints/

# Vim
*.swp
*.swo
*~

# Emacs
*~
\#*\#

# ============================================
# Sistema Operacional
# ============================================
# macOS
.DS_Store
.AppleDouble
.LSOverride

# Windows
Thumbs.db
desktop.ini
$RECYCLE.BIN/

# Linux
.directory

# ============================================
# Docker
# ============================================
.dockerignore

# ============================================
# Temporários e Cache
# ============================================
tmp/
temp/
cache/
.cache/
*.tmp
*.temp
*.bak
*.swp

# ============================================
# Build e Compilados
# ============================================
*.class
*.o
*.so
*.dylib

# ============================================
# Testes
# ============================================
.tox/
.coverage
.coverage.*
htmlcov/
.pytest_cache/

# ============================================
# Específicos de Ferramentas
# ============================================

# Terraform
.terraform/
*.tfstate
*.tfstate.backup

# Spark
spark-warehouse/
derby.log
metastore_db/

# Kafka
/logs/

# Prefect
.prefect/

# Great Expectations
uncommitted/
```

### .gitkeep para Pastas Vazias

Adicione arquivo `.gitkeep` em pastas que precisam existir mas começam vazias:

```bash
data/raw/.gitkeep
data/processed/.gitkeep
logs/.gitkeep
models/.gitkeep
```

---

## 📚 Documentação Obrigatória {#documentação}

### 1. README.md (Raiz do Projeto)

```markdown
# 📊 Nome do Projeto

[![CI](https://github.com/org/proj/workflows/CI/badge.svg)](https://github.com/org/proj/actions)
[![Coverage](https://codecov.io/gh/org/proj/branch/main/graph/badge.svg)](https://codecov.io/gh/org/proj)

## 🎯 Objetivo
Pipeline de dados que processa vendas diárias...

## 🏗️ Arquitetura

\`\`\`
[Diagrama Mermaid ou imagem]
\`\`\`

## 📋 Pré-requisitos
- Python 3.9+
- PostgreSQL 13+
- Docker & Docker Compose

## 🚀 Instalação

\`\`\`bash
# Clone
git clone repo-url

# Setup
make setup

# Teste
make test
\`\`\`

## 📊 Pipelines

### Pipeline Vendas Diário
- **Frequência**: Diário às 6h
- **Fonte**: Salesforce API
- **Destino**: Data Warehouse (tabela fct_sales)
- **SLA**: 2 horas
- **Owner**: João Silva (@joao)

## 🗂️ Estrutura de Dados

Ver [Data Catalog](docs/data_catalog/README.md)

## 🧪 Testes

\`\`\`bash
make test
make test-integration
make test-data-quality
\`\`\`

## 🚢 Deploy

Ver [DEPLOY.md](docs/DEPLOY.md)

## 📖 Documentação

- [Arquitetura](docs/architecture/README.md)
- [Runbooks](docs/runbooks/README.md)
- [Data Catalog](docs/data_catalog/README.md)

## 🆘 Suporte

- **On-call**: @data-eng-team
- **Slack**: #data-engineering
- **Email**: data-eng@company.com

## 👥 Time

| Papel | Nome | GitHub |
|-------|------|--------|
| Tech Lead | João Silva | @joao |
| Data Engineer | Maria Santos | @maria |
| Data Analyst | Pedro Costa | @pedro |

## 📜 Licença
MIT
```

### 2. Data Catalog (docs/data_catalog/)

```markdown
# 📊 Data Catalog

## Tabelas

### dim_clients
**Descrição**: Dimensão de clientes

**Schema**:
| Coluna | Tipo | Descrição | Exemplo |
|--------|------|-----------|---------|
| client_id | INTEGER | ID único | 12345 |
| client_name | VARCHAR(100) | Nome completo | "João Silva" |
| email | VARCHAR(100) | Email | "joao@email.com" |
| created_at | TIMESTAMP | Data criação | 2025-01-01 10:00:00 |
| is_active | BOOLEAN | Cliente ativo | true |

**Fonte**: Salesforce API
**Atualização**: Diária (6h)
**Owner**: @joao
**SLA**: 2 horas
**Retenção**: 5 anos

**Relacionamentos**:
- fct_sales.client_id → dim_clients.client_id
- fct_orders.client_id → dim_clients.client_id

**Queries Comuns**:
\`\`\`sql
-- Clientes ativos
SELECT * FROM dim_clients WHERE is_active = true;

-- Novos clientes no mês
SELECT * FROM dim_clients 
WHERE created_at >= DATE_TRUNC('month', CURRENT_DATE);
\`\`\`
```

### 3. Runbook (docs/runbooks/)

```markdown
# 🚨 Runbook: Pipeline Vendas Diário

## Informações Básicas
- **Nome**: pipeline_vendas_diario
- **Frequência**: Diário às 6h
- **SLA**: 2 horas
- **Owner**: João Silva (@joao)
- **On-call**: Data Engineering Team

## Monitoramento
- **Dashboard**: [Grafana Dashboard](url)
- **Alertas**: Slack #data-alerts
- **Logs**: DataDog

## Troubleshooting

### ❌ Pipeline Falhou
**Sintoma**: Alerta "Pipeline Failed"

**Diagnóstico**:
1. Verificar logs no Airflow
2. Verificar conectividade com fonte
3. Verificar espaço em disco

**Resolução**:
\`\`\`bash
# 1. Ver logs
docker logs airflow-scheduler

# 2. Reprocessar data específica
airflow dags trigger pipeline_vendas_diario \
  --conf '{"date": "2026-01-13"}'
\`\`\`

### ⚠️ Dados Atrasados
**Sintoma**: Dados não atualizados

**Diagnóstico**:
1. Verificar se pipeline rodou
2. Verificar horário da fonte
3. Verificar timezone

**Resolução**:
\`\`\`sql
-- Verificar última atualização
SELECT MAX(updated_at) FROM fct_sales;

-- Reprocessar se necessário
-- [comandos]
\`\`\`

## Rollback

\`\`\`bash
# Voltar para versão anterior
git checkout v2.0.0
make deploy-staging
# Validar
make deploy-production
\`\`\`

## Contatos
- **Tech Lead**: João Silva (@joao)
- **On-call**: @data-eng-team
- **Escalation**: CTO
```

### 4. ADR - Architecture Decision Records

```markdown
# ADR 001: Escolha de dbt para Transformações

## Status
Aceito

## Contexto
Precisávamos escolher ferramenta para transformações SQL.

Opções avaliadas:
- dbt
- Stored Procedures
- Airflow + SQL

## Decisão
Usar dbt para todas as transformações SQL.

## Consequências

### Positivas
- Versionamento de transformações
- Testes de dados integrados
- Documentação automática
- Lineage de dados
- Reusabilidade (macros)

### Negativas
- Curva de aprendizado
- Necessita setup adicional
- Dependency management

## Alternativas Consideradas
1. **Stored Procedures**: Menos versionamento
2. **Airflow + SQL**: Menos estruturado

## Referências
- [dbt Docs](https://docs.getdbt.com)
- [Benchmark interno](link)
```

---

## ✅ Code Review e Qualidade {#code-review}

### Checklist de Pull Request

```markdown
## 📋 Checklist

### Código
- [ ] Segue padrões de nomenclatura
- [ ] Código limpo e legível
- [ ] Sem código comentado/morto
- [ ] Sem credenciais hardcoded
- [ ] Tratamento de erros adequado
- [ ] Logging apropriado

### Testes
- [ ] Testes unitários incluídos
- [ ] Testes de integração (se aplicável)
- [ ] Testes de qualidade de dados
- [ ] Cobertura > 80%
- [ ] Todos os testes passando

### Dados
- [ ] Schema documentado
- [ ] Validações de qualidade
- [ ] Impacto em downstream documentado
- [ ] Backfill plan (se necessário)

### Documentação
- [ ] README atualizado
- [ ] Data catalog atualizado
- [ ] Runbook criado/atualizado
- [ ] CHANGELOG atualizado
- [ ] Comentários em código complexo

### Performance
- [ ] Queries otimizadas
- [ ] Índices apropriados
- [ ] Particionamento considerado
- [ ] Volume de dados testado

### Segurança
- [ ] Sem dados sensíveis expostos
- [ ] Credenciais em secrets
- [ ] Acesso por roles/permissions
- [ ] PII tratado adequadamente

### CI/CD
- [ ] CI passa
- [ ] Linting passa
- [ ] Type checking passa (se Python)
- [ ] Build Docker funciona
```

### Template de Pull Request

```markdown
## 📝 Descrição
[Descrição clara do que foi mudado e por quê]

## 🎯 Tipo de Mudança
- [ ] Feature (nova funcionalidade)
- [ ] Bugfix (correção)
- [ ] Hotfix (correção urgente)
- [ ] Refactor (refatoração)
- [ ] Data (mudança em dados/schema)
- [ ] Docs (documentação)
- [ ] CI/CD

## 🔗 Links
- Jira: DAT-123
- Design Doc: [link]
- Dashboard: [link]

## 🧪 Como Testar
\`\`\`bash
# Passos para testar
make test
make run-local
\`\`\`

## 📊 Impacto
### Dados
- Tabelas afetadas: `fct_sales`, `dim_clients`
- Breaking changes: Não
- Backfill necessário: Sim (últimos 30 dias)

### Downstream
- Dashboards: Dashboard Executivo precisa atualização
- APIs: Nenhum impacto
- Reports: Report mensal precisa atualização

## 📸 Screenshots
[Se aplicável]

## ✅ Checklist
[Copiar checklist acima]

## 👥 Reviewers
@joao @maria
```

### Code Review Guidelines

#### Para Reviewers:

```markdown
## O que revisar:

### 1. Funcionalidade
✅ O código faz o que deveria?
✅ Edge cases cobertos?
✅ Tratamento de erros adequado?

### 2. Qualidade
✅ Código limpo e legível?
✅ Nomes descritivos?
✅ Sem duplicação?
✅ Padrões seguidos?

### 3. Performance
✅ Queries eficientes?
✅ Índices necessários?
✅ Pode escalar?

### 4. Segurança
✅ Sem credenciais expostas?
✅ Validação de inputs?
✅ PII protegida?

### 5. Testes
✅ Testes cobrem mudanças?
✅ Testes passam?
✅ Qualidade de dados validada?

### 6. Documentação
✅ Código complexo comentado?
✅ README atualizado?
✅ Data catalog atualizado?

## Como dar feedback:

### ✅ Bom feedback:
```
"Sugiro usar índice em `client_id` pois essa query roda 
em milhões de linhas. Exemplo:
CREATE INDEX idx_sales_client ON fct_sales(client_id);
"
```

### ❌ Feedback ruim:
```
"Isso tá ruim"
"Não funciona"
```

### Tags úteis:
- **[nit]**: Nitpick, opcional
- **[question]**: Pergunta, não bloqueante
- **[blocking]**: Deve ser resolvido antes de merge
- **[suggestion]**: Sugestão de melhoria
```

---

## 🔄 Workflows DataOps {#workflows-dataops}

### Workflow 1: Nova Feature

```mermaid
graph LR
    A[Create Branch] --> B[Develop]
    B --> C[Test Locally]
    C --> D[Commit]
    D --> E[Push]
    E --> F[Create PR]
    F --> G[CI/CD]
    G --> H{Passou?}
    H -->|Não| B
    H -->|Sim| I[Code Review]
    I --> J{Aprovado?}
    J -->|Não| B
    J -->|Sim| K[Merge to Staging]
    K --> L[Deploy Staging]
    L --> M[Validate]
    M --> N{OK?}
    N -->|Não| O[Rollback]
    O --> B
    N -->|Sim| P[Merge to Main]
    P --> Q[Deploy Production]
    Q --> R[Monitor]
    R --> S[Delete Branch]
```

#### Comandos:

```bash
# 1. Create branch
git checkout staging
git pull
git checkout -b feature/DAT-123-pipeline-vendas

# 2. Develop
# ... código ...

# 3. Test locally
make test
make test-integration

# 4. Commit
git add .
git commit -m "feat(pipeline): implementa extração de vendas"

# 5. Push
git push origin feature/DAT-123-pipeline-vendas

# 6. Create PR (via GitHub/GitLab UI)

# 7-10. CI/CD e Review automaticamente

# 11. Após aprovação e merge
git checkout staging
git pull
# Deploy staging automático

# 12. Validar staging
make validate-staging

# 13. Merge to main (via PR)

# 14. Deploy production (automático)

# 15. Monitor
# Ver Grafana, DataDog, etc

# 16. Cleanup
git checkout main
git pull
git branch -d feature/DAT-123-pipeline-vendas
git push origin --delete feature/DAT-123-pipeline-vendas
```

### Workflow 2: Hotfix

```bash
# 1. Create hotfix branch DIRETO da production
git checkout production
git pull
git checkout -b hotfix/BUG-789-erro-calculo-vendas

# 2. Fix
# ... código ...

# 3. Test
make test

# 4. Commit
git commit -m "fix(vendas): corrige cálculo de comissão"

# 5. Push e PR para production
git push origin hotfix/BUG-789-erro-calculo-vendas
# PR para production

# 6. Após aprovação, merge em production
# Deploy automático

# 7. Fazer merge também em staging
git checkout staging
git merge hotfix/BUG-789-erro-calculo-vendas
git push

# 8. Cleanup
git branch -d hotfix/BUG-789-erro-calculo-vendas
```

### Workflow 3: Mudança de Schema

```bash
# 1. Branch específica para dados
git checkout -b data/schema-v2-clientes

# 2. Criar migration
# migrations/002_add_cpf_to_clients.sql
ALTER TABLE dim_clients ADD COLUMN cpf VARCHAR(11);

# 3. Atualizar dbt models
# models/marts/dim_clients.sql
# ... adicionar cpf ...

# 4. Atualizar data catalog
# docs/data_catalog/dim_clients.md
# Documentar nova coluna

# 5. Criar backfill script se necessário
# scripts/migration/backfill_cpf.py

# 6. Testar
make test-data-quality

# 7. Commit
git commit -m "schema(clientes): adiciona campo cpf

- Adiciona coluna cpf em dim_clients
- Atualiza modelo dbt
- Documenta no data catalog
- Inclui script de backfill

BREAKING CHANGE: Schema de dim_clients alterado.
Requer reprocessamento de dados."

# 8. PR com atenção especial
# Tag: [BREAKING]
# Reviewers: @tech-lead @data-steward

# 9. Deploy gradual
# Staging primeiro, validar bem
# Depois production
```

### Workflow 4: Experimento/Análise

```bash
# 1. Branch de experimento
git checkout -b experiment/analise-churn-q4

# 2. Desenvolver notebook
# notebooks/experiments/2026_01_13_analise_churn.ipynb

# 3. Commitar resultados (não dados!)
git add notebooks/experiments/
git commit -m "experiment: análise de churn Q4 2025

Insights:
- Taxa de churn aumentou 15% em dezembro
- Principais motivos: preço e concorrência
- Recomendações: programa de retenção

Refs: JIRA-456"

# 4. Não fazer merge!
# Ou fazer merge apenas se virar feature permanente
# Caso contrário, manter branch ou deletar após apresentação

# 5. Se virar feature
git checkout staging
git checkout -b feature/modelo-previsao-churn
# Transformar notebook em pipeline produtivo
# ... desenvolvimento ...
# PR normal
```

---

## 🔒 Segurança e Compliance {#segurança}

### Secrets Management

#### ❌ NUNCA faça isso:

```python
# ERRADO!
DATABASE_PASSWORD = "senha123"
API_KEY = "abc123xyz"

# ERRADO!
connection_string = "postgresql://user:password@host/db"
```

#### ✅ Faça isso:

```python
# CERTO!
import os
from dotenv import load_dotenv

load_dotenv()

DATABASE_PASSWORD = os.getenv("DATABASE_PASSWORD")
API_KEY = os.getenv("API_KEY")
```

```.env
# .env (NÃO commitar!)
DATABASE_PASSWORD=senha_segura
API_KEY=chave_api_secreta
```

```bash
# .env.example (SIM commitar!)
DATABASE_PASSWORD=sua_senha_aqui
API_KEY=sua_chave_aqui
```

### Uso de Secrets Managers

```python
# AWS Secrets Manager
import boto3

def get_secret(secret_name):
    client = boto3.client('secretsmanager')
    response = client.get_secret_value(SecretId=secret_name)
    return response['SecretString']

DATABASE_PASSWORD = get_secret('prod/database/password')
```

### PII (Personally Identifiable Information)

#### Identificar PII:

```python
# Dados considerados PII:
- CPF, RG, Passaporte
- Nome completo
- Email
- Telefone
- Endereço completo
- Data de nascimento
- Dados financeiros (cartão de crédito, conta bancária)
- Dados de saúde
- Dados biométricos
```

#### Tratamento de PII:

```python
# Hash de PII
import hashlib

def hash_pii(value):
    """Hash irreversível de PII"""
    return hashlib.sha256(value.encode()).hexdigest()

# Uso
cpf_hash = hash_pii("12345678901")

# Mascaramento
def mask_email(email):
    """Mascara email: jo**@ex***.com"""
    username, domain = email.split('@')
    return f"{username[:2]}**@{domain[:2]}***.com"

# Tokenização (reversível com chave)
from cryptography.fernet import Fernet

key = Fernet.generate_key()
cipher = Fernet(key)

def tokenize_pii(value):
    """Tokeniza PII de forma reversível"""
    return cipher.encrypt(value.encode())

def detokenize_pii(token):
    """Destokeniza PII"""
    return cipher.decrypt(token).decode()
```

### Níveis de Acesso

```sql
-- Criar roles
CREATE ROLE data_analyst;
CREATE ROLE data_engineer;
CREATE ROLE data_admin;

-- Permissões por camada
-- Bronze/Raw: Apenas engineers
GRANT SELECT ON raw.* TO data_engineer;

-- Silver/Staging: Engineers e alguns analysts
GRANT SELECT ON staging.* TO data_engineer;
GRANT SELECT ON staging.* TO data_analyst;

-- Gold/Marts: Todos
GRANT SELECT ON marts.* TO data_analyst;

-- PII: Apenas admin com justificativa
GRANT SELECT ON sensitive.clients_pii TO data_admin;

-- Views sem PII para análise
CREATE VIEW marts.clients_analytics AS
SELECT
    client_id,
    hash(cpf) as cpf_hash,  -- hash ao invés de CPF real
    age_group,  -- faixa etária ao invés de data nascimento
    city  -- cidade ao invés de endereço completo
FROM sensitive.clients_pii;

GRANT SELECT ON marts.clients_analytics TO data_analyst;
```

### Auditoria

```sql
-- Log de acessos a dados sensíveis
CREATE TABLE audit.data_access_log (
    id SERIAL PRIMARY KEY,
    user_name VARCHAR(100),
    table_name VARCHAR(100),
    action VARCHAR(50),
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    query_text TEXT
);

-- Trigger para log
CREATE TRIGGER log_access
AFTER SELECT ON sensitive.clients_pii
FOR EACH STATEMENT
EXECUTE FUNCTION log_data_access();
```

### LGPD/GDPR Compliance

```python
# Direito ao esquecimento
def delete_user_data(user_id):
    """
    Remove todos os dados de um usuário (LGPD Art. 18)
    """
    # Deletar dados pessoais
    db.execute("""
        DELETE FROM clients WHERE client_id = %s
    """, (user_id,))
    
    # Anonimizar dados históricos
    db.execute("""
        UPDATE orders 
        SET client_name = 'ANONYMIZED',
            client_email = 'ANONYMIZED'
        WHERE client_id = %s
    """, (user_id,))
    
    # Log da ação
    audit_log(f"User {user_id} data deleted - LGPD request")

# Exportação de dados (LGPD Art. 18)
def export_user_data(user_id):
    """
    Exporta todos os dados de um usuário
    """
    data = {
        'personal_info': get_personal_info(user_id),
        'orders': get_orders(user_id),
        'interactions': get_interactions(user_id)
    }
    return data
```

### Checklist de Segurança

```markdown
## 🔒 Security Checklist

### Código
- [ ] Sem credenciais hardcoded
- [ ] Secrets em secrets manager
- [ ] .env não commitado
- [ ] .env.example commitado

### Dados
- [ ] PII identificado
- [ ] PII protegido (hash/tokenização)
- [ ] Acesso por roles/permissions
- [ ] Auditoria configurada
- [ ] Retenção de dados definida

### Infraestrutura
- [ ] Conexões criptografadas (SSL/TLS)
- [ ] Rede privada (VPC)
- [ ] Firewall configurado
- [ ] Backups criptografados

### Compliance
- [ ] LGPD/GDPR compliance
- [ ] Política de privacidade
- [ ] Consentimento documentado
- [ ] Processo de exclusão de dados

### Code Review
- [ ] Scan de secrets automático
- [ ] Dependency scan (vulnerabilidades)
- [ ] SAST (Static Analysis)
- [ ] Aprovação de security team
```

---

## ✅ Checklist Completo de Projeto {#checklist}

### Checklist de Setup Inicial

```markdown
## 📋 Setup de Novo Projeto DataOps

### Repositório
- [ ] Criar repositório no GitHub/GitLab
- [ ] Adicionar descrição clara
- [ ] Configurar .gitignore (use template DataOps)
- [ ] Adicionar LICENSE
- [ ] Configurar branch protection (main/staging)
- [ ] Adicionar PR template
- [ ] Adicionar issue templates

### Estrutura
- [ ] Criar estrutura de pastas padrão
- [ ] Adicionar .gitkeep em pastas vazias
- [ ] Configurar pré-commit hooks
- [ ] Setup Makefile com comandos úteis

### Documentação
- [ ] README.md completo
- [ ] CONTRIBUTING.md
- [ ] CHANGELOG.md
- [ ] CODE_OF_CONDUCT.md
- [ ] Docs de arquitetura
- [ ] Data catalog inicial
- [ ] Runbooks de operação

### CI/CD
- [ ] Configurar GitHub Actions / GitLab CI
- [ ] Pipeline de testes
- [ ] Pipeline de deploy (staging)
- [ ] Pipeline de deploy (production)
- [ ] Linting automático
- [ ] Security scanning
- [ ] Dependency checking

### Segurança
- [ ] Secrets configurados
- [ ] Roles e permissões
- [ ] Scan de secrets automático
- [ ] .env.example criado
- [ ] Compliance checklist

### Qualidade
- [ ] Testes unitários setup
- [ ] Testes integração setup
- [ ] Data quality tests
- [ ] Code coverage > 80%
- [ ] Linting configurado (black, flake8, mypy)

### Monitoramento
- [ ] Logging configurado
- [ ] Métricas definidas
- [ ] Alertas configurados
- [ ] Dashboard criado
- [ ] On-call rotation

### Time
- [ ] CODEOWNERS configurado
- [ ] Reviewers definidos
- [ ] On-call definido
- [ ] Documentação de papéis
```

### Checklist de Pull Request

```markdown
## 📋 Antes de Abrir PR

### Código
- [ ] Código limpo e legível
- [ ] Segue padrões do projeto
- [ ] Conventional commits
- [ ] Sem código morto/comentado
- [ ] Tratamento de erros
- [ ] Logging adequado

### Testes
- [ ] Testes unitários escritos
- [ ] Testes passando localmente
- [ ] Coverage mantido/melhorado
- [ ] Testes de integração (se necessário)
- [ ] Data quality tests

### Documentação
- [ ] Código complexo comentado
- [ ] README atualizado
- [ ] Data catalog atualizado
- [ ] CHANGELOG atualizado
- [ ] Runbook atualizado (se necessário)

### Dados
- [ ] Schema documentado
- [ ] Validações implementadas
- [ ] Impacto analisado
- [ ] Backfill planejado (se necessário)

### Segurança
- [ ] Sem secrets expostos
- [ ] PII tratado adequadamente
- [ ] Permissões corretas
- [ ] Scan de segurança passou

### Performance
- [ ] Queries otimizadas
- [ ] Índices considerados
- [ ] Volume de dados testado
- [ ] Particionamento avaliado

### CI/CD
- [ ] CI passa localmente
- [ ] Build bem-sucedido
- [ ] Linting passa
- [ ] Type checking passa
```

### Checklist de Deploy

```markdown
## 📋 Antes de Deploy

### Pre-Deploy
- [ ] PR aprovado por 2+ reviewers
- [ ] CI/CD verde
- [ ] Testes passando (100%)
- [ ] Code coverage > 80%
- [ ] Security scan passou
- [ ] Staging testado e validado

### Comunicação
- [ ] Time notificado
- [ ] Stakeholders informados
- [ ] Janela de manutenção (se necessário)
- [ ] Runbook atualizado

### Dados
- [ ] Backfill planejado
- [ ] Migration scripts prontos
- [ ] Rollback plan documentado
- [ ] Data quality validado

### Deploy
- [ ] Backup realizado
- [ ] Deploy executado
- [ ] Smoke tests passaram
- [ ] Monitoramento OK
- [ ] Métricas normais

### Post-Deploy
- [ ] Validação em produção
- [ ] Dashboard atualizado
- [ ] Documentação atualizada
- [ ] Time notificado (sucesso)
- [ ] Post-mortem (se problemas)
```

---

## 🎓 Resumo e Boas Práticas Gerais

### ✅ SEMPRE Faça:

1. **Commits frequentes e pequenos**
2. **Mensagens de commit claras** (Conventional Commits)
3. **Pull antes de push**
4. **Code review obrigatório**
5. **Testes automatizados**
6. **Documentação atualizada**
7. **Secrets em secrets manager**
8. **PII protegido**
9. **Branch por feature**
10. **CI/CD funcionando**

### ❌ NUNCA Faça:

1. **Commitar credenciais**
2. **Commitar dados grandes**
3. **Commit direto em main/production**
4. **Force push em branches compartilhadas**
5. **Deixar código morto**
6. **Mensagens vagas ("fix", "update")**
7. **Skip de testes**
8. **Deploy sem validação**
9. **Ignorar code review**
10. **Esquecer documentação**

### 📊 Métricas de Qualidade

Acompanhe estas métricas:

```
✅ Code Coverage: > 80%
✅ PR Merge Time: < 24h
✅ CI/CD Success Rate: > 95%
✅ Mean Time to Recovery: < 1h
✅ Deployment Frequency: Daily
✅ Lead Time for Changes: < 1 day
✅ Change Failure Rate: < 5%
```

---

## 🔗 Recursos Adicionais

### Templates e Exemplos

- **GitHub Templates**: [github.com/github/gitignore](https://github.com/github/gitignore)
- **Conventional Commits**: [conventionalcommits.org](https://www.conventionalcommits.org/)
- **Semantic Versioning**: [semver.org](https://semver.org/)

### Ferramentas Recomendadas

- **Pre-commit hooks**: [pre-commit.com](https://pre-commit.com)
- **Commitizen**: Auxilia em conventional commits
- **GitLeaks**: Scan de secrets
- **Black**: Code formatter Python
- **Flake8**: Linting Python
- **MyPy**: Type checking Python

### Leitura Complementar

- **Pro Git Book**: [git-scm.com/book](https://git-scm.com/book)
- **GitHub Flow**: [docs.github.com/en/get-started/quickstart/github-flow](https://docs.github.com/en/get-started/quickstart/github-flow)
- **Data Engineering Best Practices**: Blogs e documentação de Airflow, dbt, etc.

---

**Última atualização:** Janeiro 2026

**Mantenedor:** Time de Data Engineering

**Versão:** 1.0.0
