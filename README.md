# dre-test

## Problema 1

O serviço `dre-3-test-airflow-init` não está subindo

### Causa

A env `AIRFLOW_UID` não está definida

### Solução

Adicionei um `.env` no projeto que lê o uid do user que está executando o projeto.

Alterei a definição do user no template dos serviços airflow de `user: "5000"` para `user: "${AIRFLOW_UID:-5000}:0"`, assim ele vai ler a definição da env para rodar o container e caso ela não exista vai pegar o fallback do valor `5000`.

Adicionei uma validação para que a env_var seja validada no init assim como no exemplo do `docker-compose.yaml` do airflow.
