# dre-test

## Problem
O serviço `airflow-init` não está subindo.
### Cause
O serviço não consegue se conectar ao postgres.
No arquivo compose a env `POSTGRES_USER` está setada com o user `admin` e a string de conexão está setada como `airflow`
### Fix
Mudei o user do postgres de `admin` para `airflow`


## Problem
O serviço `airflow-worker` não está subindo.
### Cause
Ele não consegue manipular algumas pastas que foram montadas no container por problemas de permissão.
### Fix
É preciso setar o `uid` do user que está rodando a stack pro container poder criar as pastas com a permissão correta.
A forma recomendada de fazer isso é setando ela no arquivo `.env`
> https://airflow.apache.org/docs/apache-airflow/stable/howto/docker-compose/index.html#setting-the-right-airflow-user
Também é recomendado ajustar o user definido no template dos serviços airflow para usar essa env.