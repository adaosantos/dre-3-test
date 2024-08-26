# Issues
Lista de problemas encontrados na stack:

<details>
<summary>O serviço `airflow-init` não está subindo.</summary>
O serviço não consegue se conectar ao postgres.
No arquivo compose a env `POSTGRES_USER` está setada com o user `admin` e a string de conexão está setada como `airflow`

**Correção:** Mudei o user do postgres de `admin` para `airflow`
</details>

<details>
<summary>O serviço `airflow-worker` não está subindo.</summary>
Ele não consegue manipular algumas pastas que foram montadas no container por problemas de permissão.

**Correção:** É preciso setar o `uid` do user que está rodando a stack pro container poder criar as pastas com a permissão correta.
A forma recomendada de fazer isso é setando ela no arquivo `.env`
> https://airflow.apache.org/docs/apache-airflow/stable/howto/docker-compose/index.html#setting-the-right-airflow-user
</details>

<details>
<summary>Os DAGs não estão sendo carregados.</summary>
O volume definido no template dos serviços airflow está apontando para a pasta errada.
O DAG `smooth.py` está com um erro de sintaxe na definição do método `smooth()`

**Correção:** Apontamento do volume foi modificado de `./dag` para `./dags` no arquivo `compose.yaml`
Corrigido a definição do método `smooth` no arquivo `./dags/smooth.py`
> Pasta `./dag` foi removida, visto que não há uso para ela.
</details>