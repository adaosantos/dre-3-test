# dre-test
Apache Airflow local stack

## Running
- `echo -e "AIRFLOW_UID=$(id -u)" > .env`
- `docker compose up -d`
- Navegue até (http://localhost:8080)[http://localhost:8080] e faça login com o usuário `airflow` e a senha `airflow`

## Docs
- [Issues](docs/issues.md)
- [Architecture](docs/architecture.md)