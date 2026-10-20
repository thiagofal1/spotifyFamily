# Workflows do n8n

Os workflows públicos devem ser exportados para `workflows/public/` somente depois de:

1. remover credenciais embutidas;
2. substituir números, nomes, mensagens e IDs reais por dados fictícios;
3. trocar URLs de produção por placeholders;
4. revisar nós HTTP, webhooks e expressões;
5. testar a importação em uma instância local limpa.

Workflows de produção ou que contenham dados reais não devem ser versionados neste repositório.
