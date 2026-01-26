# MCP client + server para gerenciar google sheet

![Status do Projeto](https://img.shields.io/badge/status-Em_andamento-yellow)
 
Automação criada no **n8n** integrando **MCP Server** e **MCP Client** para permitir que um agente de IA **crie, atualize e exclua linhas** em uma planilha do Google Sheets de forma controlada.

---

## 🧠 O que este projeto faz

- Recebe comandos em linguagem natural via **MCP Client**
- Processa as intenções usando um **AI Agent**
- Executa ações no Google Sheets via **n8n tools**
- Retorna respostas estruturadas ao agente

---

## 🧩 Arquitetura

- **MCP Server**: expõe ferramentas (tools) para o n8n
- **n8n MCP Trigger**: recebe chamadas do MCP Server
- **MCP Client**: permite que o agente de IA chame essas tools
- **Google Sheets Tool**: persiste os dados

> ⚠️ Este repositório não contém credenciais reais nem endpoints ativos.

---

## 🚀 Como usar

1. Clone o repositório
2. Importe os workflows no n8n
3. Configure as credenciais:
   - Google Sheets
   - LLM (Groq / OpenAI / outro)
4. No MCP server: 
   - abra as tools do sheet e conecte a planilha no campo "document"
   - configure com o nome das colunas da sua planilha
5. No MCP Client
   - abra o MCP e coloque o ENDPOINT do MCP server
5. Ative os workflows

> obs: O MCP client pode ser conectado a qualquer outro MCP server, desde que seja vínculado a ele o ENDPOINT do MCP server desejado. 

> Novas tools também podem ser anexadas ao MCP server deste projeto

---

## 📦 Requisitos

- n8n (self-hosted ou cloud)
- Conta Google com acesso ao Google Sheets
- Node.js / Python 

---

## 📄 Licença

Uso educacional e experimental. 
