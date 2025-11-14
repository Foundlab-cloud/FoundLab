<p align="center">
  <img src="docs/banner-memrag-gcp.png"
       alt="FoundLab — Mem-RAG V2 Compliance Orchestrator (GCP Edition)"
       width="100%" />
</p>

<p align="center">
  <a href="#-overview"><img alt="FoundLab - Mem-RAG V2" src="https://img.shields.io/badge/FoundLab-Mem--RAG%20V2-111827?style=for-the-badge" /></a>
  <a href="#-arquitetura-da-solução"><img alt="Google Cloud Stack" src="https://img.shields.io/badge/Google_Cloud-Run_%7C_Vertex_AI_%7C_BigQuery-4285F4?style=for-the-badge&logo=google-cloud" /></a>
  <a href="#-proposta-de-valor"><img alt="Architecture" src="https://img.shields.io/badge/Architecture-Serverless_%7C_Stateless-0F766E?style=for-the-badge" /></a>
  <a href="#-auditabilidade"><img alt="Compliance Ready" src="https://img.shields.io/badge/Compliance-Auditável_%7C_WORM_%7C_Veritas-7C3AED?style=for-the-badge" /></a>
  <a href="#-licença"><img alt="License" src="https://img.shields.io/badge/License-Apache--2.0-4B5563?style=for-the-badge" /></a>
</p>

<hr/>

# FoundLab — Mem-RAG V2 Compliance Orchestrator (GCP Edition)

> **O Kernel de Conformidade Serverless para IA Generativa em Ambientes Regulados.** > *Deploy em um clique via Google Cloud Marketplace.*

O **Mem-RAG V2** resolve o maior bloqueador da adoção de IA Generativa em empresas corporativas: **o risco de confiança**.

Esta solução **não é um chatbot**. É um orquestrador backend que se instala dentro do seu projeto Google Cloud, transformando modelos generativos (como Gemini ou Llama) de "caixas-pretas probabilísticas" em **mecanismos de decisão auditáveis, determinísticos e criptograficamente selados**.

### 🎯 Projetado para:
* 🏦 **Bancos, Fintechs, PSPs & BaaS** (Análise de Risco, Fraude, Crédito)
* 🛡️ **Seguradoras** (Underwriting, Sinistros)
* ⚖️ **Jurídico & Compliance** (Auditoria de Contratos, Due Diligence)

---

## 📚 Índice

- [🏛️ Proposta de Valor: Por que Mem-RAG?](#%EF%B8%8F-proposta-de-valor-por-que-mem-rag)
- [🗺️ Arquitetura da Solução](#%EF%B8%8F-arquitetura-da-solu%C3%A7%C3%A3o)
- [🚀 Guia de Implementação (3 Passos)](#-guia-de-implementa%C3%A7%C3%A3o-3-passos)
- [🧪 O Selo Veritas: Exemplo de Saída](#-o-selo-veritas-exemplo-de-sa%C3%ADda)
- [⚙️ API Reference](#%EF%B8%8F-api-reference)
- [🧩 Variáveis do Terraform](#-vari%C3%A1veis-do-terraform)
- [⚠️ Riscos & Mitigações](#%EF%B8%8F-riscos--mitiga%C3%A7%C3%B5es)

---

## 🏛️ Proposta de Valor: Por que Mem-RAG?

Elimine a alucinação e o "drift" de modelo com uma arquitetura focada em **segurança jurídica**.

### 🔒 1. Auditabilidade Total (Protocolo Veritas)
Cada interação com a IA deixa um rastro imutável. O sistema valida a decisão contra um schema rigoroso, gera um hash **SHA-256** combinando *Pedido + Contexto + Resposta*, e grava um "Selo Veritas" em uma tabela **WORM (Write-Once, Read-Many)** no BigQuery. O regulador pode auditar o exato estado que levou à decisão.

### 🧠 2. Controle de Decoerência (Anti-Alucinação)
A arquitetura força o LLM a colapsar sua resposta em um **schema JSON determinístico**. Se o modelo alucinar ou violar o contrato de dados, a transação falha de forma segura (fail-safe), impedindo que dados corrompidos entrem no seu sistema de produção.

### 🧬 3. Memória Híbrida Inteligente
Combina o melhor dos dois mundos para contexto de alta precisão:
* **Memória Semântica (Vertex AI Vector Search):** Entende regras, leis e políticas internas.
* **Memória Episódica (BigQuery / Cloud SQL):** Lembra do histórico transacional e comportamento recente do usuário.

### 🛡️ 4. Privacidade "Zero Trust"
A solução é **100% serverless e stateless**. Nenhum dado sensível é persistido no orquestrador. Todo o processamento ocorre dentro do perímetro de segurança do seu projeto Google Cloud (VPC-SC ready).

---

## 🗺️ Arquitetura da Solução

A solução implanta um endpoint único no **Cloud Run** que orquestra todo o fluxo cognitivo.

### Fluxo de Decisão

1.  **Input:** Microsserviço envia `user_id` e `transacao_id`.
2.  **RAG Híbrido:** Orquestrador busca regras (Vector Search) e histórico (BigQuery).
3.  **Inferência Privada:** Contexto consolidado é enviado ao **Vertex AI Model Garden** (Gemini/Llama).
4.  **Protocolo Veritas:**
    * Validação de Schema (Pydantic).
    * Cálculo de Hash (SHA-256).
    * Persistência WORM (Log de Auditoria).
5.  **Output:** Decisão selada retornada à aplicação.

```mermaid
graph LR
    A[App Cliente] -->|JSON| B(Cloud Run Orchestrator)
    B -->|Busca Vetorial| C[Vertex AI Vector Search]
    B -->|SQL Query| D[BigQuery Episódico]
    B -->|Contexto + Prompt| E[Vertex AI LLM]
    E -->|Decisão Bruta| B
    B -->|Validação & Hash| B
    B -->|Write Only| F[BigQuery Audit Log]
    B -->|Decisão Selada| A
````

-----

## 🚀 Guia de Implementação (3 Passos)

Este blueprint utiliza **Terraform** para provisionamento automático via Marketplace ou CLI.

### ✅ Pré-requisitos

No seu projeto GCP, certifique-se de ter:

1.  Um endpoint de modelo na **Vertex AI** (ex: Gemini 1.5 Pro).
2.  Um índice no **Vector Search** (Memória Semântica).
3.  Uma tabela no **BigQuery** ou **Cloud SQL** (Memória Episódica).

### 🛠️ Passo 1: Deploy

Clone o repositório e inicie o Terraform:

```bash
git clone [https://github.com/foundlab-cloud/mem-rag-gcp-marketplace.git](https://github.com/foundlab-cloud/mem-rag-gcp-marketplace.git)
cd mem-rag-gcp-marketplace/deployment

# Preencha o terraform.tfvars com seu Project ID e Endpoints
terraform init
terraform apply
```

> **Nota:** Ao usar o Google Cloud Marketplace, estas variáveis são preenchidas via interface gráfica.

### 📦 Passo 2: Ingestão e Configuração (CLI)

Utilize nossa ferramenta de Developer Experience, `memragctl`, para popular suas memórias.

```bash
# Instalar CLI
pip install ./cli

# Ingerir Regras de Compliance (PDF/Txt -> Vector Search)
memragctl ingest rules ./docs/compliance_policy.pdf --index-endpoint "projects/..."

# Conectar Histórico (CSV -> BigQuery)
memragctl ingest history ./data/transacoes_passadas.csv --bq-table "dataset.tabela"
```

### 🚦 Passo 3: Teste de Sanidade

Valide se o orquestrador está assinando decisões corretamente:

```bash
memragctl test ./payload_teste.json --url "[https://memrag-prod-xxxxx.a.run.app](https://memrag-prod-xxxxx.a.run.app)"
```

-----

## 🧪 O Selo Veritas: Exemplo de Saída

Ao chamar a API, você não recebe apenas um texto. Você recebe um objeto de decisão auditável. Veja o campo `veritas_hash` e `rationale`:

```json
{
  "veritas_hash": "a45b0f6c2e9d4f...9f2c",
  "timestamp": "2025-11-14T12:34:56.789Z",
  "decision_data": {
    "decision": "REVIEW",
    "rationale": "A transação excede o limite diário estabelecido na política REG-004 e o histórico do cliente é recente (< 30 dias).",
    "evidence_refs": ["REG-004", "user_history:txn-abc"],
    "risk_score": 0.75
  },
  "request_data": {
    "user_id": "user-123",
    "transacao_id": "txn-abc"
  }
}
```

-----

## ⚙️ API Reference

### `POST /v1/execute`

O endpoint principal para submeter transações para análise.

| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| `user_id` | `string` | Identificador único do usuário para busca de memória episódica. |
| `transacao_id` | `string` | ID do evento ou transação atual. |
| `dados_contextuais` | `object` | Payload arbitrário com os detalhes da transação atual. |

**Retorno de Sucesso (200 OK):** Objeto JSON contendo o `SeloVeritas` (estrutura acima).
**Erro de Compliance (422 Unprocessable Entity):** Retornado se o LLM não conseguir aderir ao schema ou se as regras de negócio bloquearem a execução.

-----

## 🧩 Variáveis do Terraform

Parâmetros configuráveis durante o deploy:

| Variável | Obrigatório | Descrição |
| :--- | :---: | :--- |
| `project_id` | Sim | ID do Projeto Google Cloud. |
| `region` | Sim | Região dos recursos (ex: `us-central1`). |
| `vertex_model_endpoint` | Sim | Recurso do modelo (Gemini/Llama) na Vertex AI. |
| `vertex_vector_index` | Sim | Endpoint do índice do Vector Search. |
| `episodic_store_bq_table` | Sim\* | Tabela BigQuery para histórico (\*se usar BQ). |
| `audit_table_name` | Não | Nome da tabela WORM de auditoria (Default: `memrag_v2_decisions`). |

-----

## ⚠️ Riscos & Mitigações

| Desafio | Solução Mem-RAG |
| :--- | :--- |
| **Alucinação do Modelo** | Validação rígida de Schema Pydantic. Se o JSON quebrar, a transação é abortada antes de causar dano. |
| **Custo de Inferência** | Arquitetura 100% Serverless (Cloud Run). Você paga apenas por invocação, sem servidores ociosos. |
| **Auditoria Regulatória** | Tabelas WORM no BigQuery garantem que os logs de decisão nunca sejam alterados ou deletados. |

-----

## ⚖️ Licença

Distribuído sob a licença **Apache 2.0**. Veja `LICENSE` para mais informações.

-----

\<p align="center"\>
\<b\>FoundLab\</b\> — \<i\>Building the Trust Layer for Enterprise AI.\</i\>
\</p\>
