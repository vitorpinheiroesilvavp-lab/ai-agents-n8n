# AI Agents com n8n — RAG e Sistemas Multiagentes

Repositório de projetos pessoais de **agentes de IA** construídos em [n8n](https://n8n.io/), combinando orquestração multiagente, **RAG (Retrieval-Augmented Generation)** e integração com serviços do Google e OpenAI/Gemini.

Cada projeto é um sistema de atendimento por e-mail em que um **agente orquestrador** interpreta a mensagem recebida e a direciona para agentes especialistas, cada um com persona, escopo e base de conhecimento próprios.

> Projetos de portfólio. As empresas e os dados usados são **fictícios** — nenhuma informação real ou corporativa está presente.

---

## Projeto 1 — Sistema Multiagente de Atendimento (Academia)

Atendimento automático dos e-mails de uma academia, com um orquestrador que decide qual especialista deve responder.

**Arquitetura**
- **Orquestrador** (LLM Google Gemini): lê o e-mail e aciona o agente certo como ferramenta.
- **4 agentes especialistas**, cada um com sua persona e regras:
  - **Vendas** — conversão de interessados em matrícula
  - **Retenção / Cancelamento** — entende o motivo real antes de aceitar o cancelamento
  - **Treino** — orientação técnica de exercícios e progressão
  - **Nutrição** — orientação alimentar e de suplementação em nível geral
- **RAG** com **Supabase (pgvector)** + **embeddings OpenAI**, alimentado por uma ingestão automática de documentos (Google Drive → extração → *token splitter* → *embeddings* → *vector store*).
- **Memória de conversa** por janela de contexto.
- Resposta enviada automaticamente via **Gmail**.

**Stack:** n8n · Google Gemini · OpenAI Embeddings · Supabase (pgvector) · Gmail API · Google Drive API

<!-- Cole aqui o print do fluxo: arraste o arquivo .png para esta linha -->

---

## Projeto 2 — Agente de Vendas e Relacionamento (Agência de Turismo)

Atendimento por e-mail de uma agência de viagens que **primeiro identifica se o remetente já é cliente** e só então escolhe a abordagem certa.

**Arquitetura**
- **Avaliador**: consulta uma planilha (Google Sheets) para descobrir se o e-mail já é de um cliente cadastrado.
- **Orquestrador**: com base nisso, roteia para um dos três agentes:
  - **Vendedor de novos clientes** — abordagem de conversão
  - **Concierge** — acompanhamento de quem já fechou pacote
  - **Fidelizador** — reativação de quem já viajou
- **RAG** com **Supabase (pgvector)** + **embeddings OpenAI**.
- **Agendamento de ligações** via **Google Calendar**.
- Resposta automática via **Gmail**.

**Stack:** n8n · OpenAI · OpenAI Embeddings · Supabase (pgvector) · Gmail API · Google Calendar API · Google Sheets API

<!-- Cole aqui o print do fluxo: arraste o arquivo .png para esta linha -->

---

## Como importar os fluxos no n8n

1. Baixe o arquivo `.json` do projeto desejado.
2. No seu n8n, vá em **Workflows → Import from File**.
3. Selecione o `.json` importado.
4. Configure suas próprias credenciais (OpenAI, Gemini, Supabase, Google) — elas **não** acompanham o arquivo.

## Credenciais

Os arquivos exportados contêm apenas as **referências** de credenciais, nunca as chaves. Para rodar, cada usuário conecta as próprias contas dentro do n8n.

---

## 👤 Autor

**Vitor Pinheiro e Silva** — Analista Financeiro com foco em automação e IA aplicada.
[LinkedIn](https://www.linkedin.com/in/vitor-pinheiro-e-silva-136983346)
