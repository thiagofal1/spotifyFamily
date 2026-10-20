# Arquitetura

## Fluxo principal

1. Uma mensagem ou evento chega pela Evolution API.
2. A Evolution API encaminha o evento ao webhook do n8n.
3. O n8n valida e normaliza os dados recebidos.
4. O workflow consulta ou atualiza uma planilha do Google Sheets.
5. O n8n decide a ação necessária e envia uma resposta pela Evolution API.
6. Serviços locais mantêm estado e filas conforme a configuração do ambiente.

## Componentes

| Componente | Responsabilidade |
|---|---|
| n8n | Orquestração dos workflows, regras e integrações |
| Evolution API | Entrada e saída de mensagens pelo WhatsApp |
| Google Sheets | Registro operacional e visão simples dos dados |
| PostgreSQL | Persistência da Evolution API |
| Redis | Cache e suporte ao estado da Evolution API |
| Docker Compose | Inicialização, rede e volumes do ambiente local |

## Princípios

- Segredos ficam apenas no `.env` local.
- Dados públicos de demonstração devem ser fictícios.
- Workflows devem ser idempotentes quando uma mensagem for reenviada.
- Falhas de API precisam produzir logs úteis e respostas previsíveis.
- O ambiente de demonstração deve ser separado de qualquer instância de produção.
