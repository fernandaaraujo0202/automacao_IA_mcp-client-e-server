# Fluxo do Projeto n8n MCP 

Este documento descreve o funcionamento completo do projeto n8n baseado em MCP (Model Context Protocol), composto por dois workflows principais: MCP Client e MCP Server.
O fluxo permite que mensagens recebidas via chat sejam interpretadas por um agente de IA, que interage com um servidor MCP para executar operações retornar respostas estruturadas.

## Visão Geral

O projeto implementa uma arquitetura cliente-servidor MCP, onde:

O MCP Client recebe mensagens de chat e orquestra a execução

Um Agente de IA decide quando e como chamar ferramentas MCP

O MCP Server executa operações Cloud (Google Sheets)

O sistema retorna respostas estruturadas em JSON

# O MCP Client

O MCP Client é responsável por receber mensagens de chat, interpretá-las com um agente de IA e acionar ferramentas MCP expostas pelo servidor.

### Chat (LangChain)

* Ponto de entrada do sistema

* Dispara o workflow sempre que uma nova mensagem de chat é recebida

* Encaminha o conteúdo para o agente de IA

### agente IA (LangChain Agent)

* Interpretar a mensagem do usuário

* Decidir se uma ferramenta MCP deve ser chamada

* Orquestrar memória, modelo de linguagem e ferramentas

* Garantir respostas coerentes e estruturadas

* O agente está configurado com:

#### Limite de iterações

* Memória de curto prazo

* Modelo de linguagem

* Ferramentas MCP

### Memória (Buffer Window)

* Mantém conversas recentes
* Conectada no IA Agent

### Groq Chat Model (LLM)

* Modelo de linguagem do agente

* Auxilia na decisão de chamadas MCP e estrutura da resposta

### MCP Client Tool

* Responsável por se conectar oa MCP Server

* Usa autencicação OAuth2

* Permite o agente chamar ferramentas Cloud remotamente

# O MCP Server

O MCP Server tem ferramentas MCP que podem ser chamadas pelo cliente.

### MCP Server Trigger

* Recebe chamadas do MCP Client

* Encaminha para as ferramentas disponíveis

### Ferramentas disponíveis

####  Append or Update Row in Google Sheets

* Insere ou atualiza linhas em uma planilha Google Sheets

* Utilisa os campos: 
    * ID
    * Descrição
    * Status
    * Data
    * Responsável
    * Observações
    * PDF

#### Delete Rows or Columns from Google Sheets

* Exlui linhas ou colunas da planilha

# Fluxo de execução

1- O usuário envia uma mensagem no chat

2- O MCP Client é acionado pelo Chat Trigger

3- O IA Agent interpreta a mensagem

4- O agente consulta sua memória e o modelo de linguagem

5- O agente decide chamar a ferramenta MCP

6- O MCP Client Tool envia a requisição para o MCP Server

7- O MCP Server executa a operação

8- O resultado volta ao MCP Client

9- O agente estrutura a resposta

10- O usuário recebe um JSON estruturado como resposta

# Observações

* Os workflows são desacoplados e reutilizáveis
* O MCP permite expansão para novas ferramentas
* Ideal para automações com IA + Cloud