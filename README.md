# Spotify Family Automation

Automação local para organizar operações recorrentes do Spotify Family usando **n8n**, **Docker**, **Google Sheets** e **Evolution API**.

> Este repositório é uma versão sanitizada e demonstrativa do projeto. Não contém credenciais, números de telefone, dados de participantes, IDs de planilhas ou workflows exportados de produção.

## O problema

A operação do Spotify Family envolve informações e tarefas recorrentes que podem ser difíceis de acompanhar manualmente: registros, notificações, confirmações e atualização de status. O projeto usa o WhatsApp como interface de comunicação e o Google Sheets como fonte de organização, deixando o n8n coordenar o fluxo.

## O que o projeto demonstra

- Orquestração de automações no n8n.
- Integração entre WhatsApp, Google Sheets e APIs HTTP.
- Execução local e reprodutível com Docker Compose.
- Separação de serviços com n8n, Evolution API, PostgreSQL e Redis.
- Uso de variáveis de ambiente para configuração e segredos.
- Pensamento de operação: persistência, healthchecks e reinicialização automática.

## Arquitetura

```text
WhatsApp
   │
   ▼
Evolution API ──► Webhook / HTTP ──► n8n
                                      │
                                      ├──► Google Sheets
                                      └──► Resposta via Evolution API

Persistência local:
n8n ─────────► volume n8n_data
Evolution API ─► PostgreSQL + Redis
```

Consulte [docs/architecture.md](docs/architecture.md) para conhecer os componentes e as responsabilidades de cada serviço.

## Estrutura atual

- `compose.yaml`: ambiente local com n8n, Evolution API, PostgreSQL e Redis.
- `.env.example`: modelo de configuração sem credenciais reais.
- `workflows/README.md`: orientação para exportar workflows sanitizados.
- `docs/`: documentação técnica e decisões do projeto.

## Como executar localmente

Requisitos:

- Docker Desktop;
- Docker Compose;
- uma instância de teste da Evolution API;
- uma planilha de teste no Google Sheets;
- credenciais de desenvolvimento configuradas apenas no `.env` local.

```powershell
Copy-Item .env.example .env
# Edite .env com valores locais e segredos que não serão versionados.
docker compose up -d
```

Depois, acesse os serviços locais conforme as portas configuradas no `compose.yaml`.

## Segurança e privacidade

Nunca publique:

- `.env` ou chaves de criptografia;
- tokens da Evolution API ou do Google;
- números de telefone, nomes e mensagens reais;
- URLs de webhook de produção;
- IDs ou links de planilhas reais;
- QR codes, dados de sessão ou volumes exportados;
- workflows n8n que ainda contenham credenciais embutidas.

Use dados fictícios e uma conta/planilha de demonstração para qualquer exemplo público.

## Próximas melhorias

1. Adicionar workflows n8n exportados e sanitizados em `workflows/public/`.
2. Documentar cada workflow com entrada, saída e tratamento de erros.
3. Criar uma planilha de demonstração com dados fictícios.
4. Adicionar screenshots ou um diagrama atualizado do fluxo.
5. Criar testes de payload para os webhooks principais.
6. Registrar decisões sobre idempotência, retries e falhas de comunicação.
7. Publicar uma release com instruções reproduzíveis.

## Status

**Case de automação em preparação para publicação pública.** A infraestrutura local está documentada; os workflows e exemplos públicos ainda precisam ser sanitizados antes da divulgação.

## Licença

MIT.
