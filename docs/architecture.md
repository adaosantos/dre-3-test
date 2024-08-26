# Architecture

Uma visão geral sobre a arquitetura do projeto.

## Arquitetura atual

Hoje a arquitetura escolhida foi rodar o Airflow utilizando uma fila baseada em Redis para gerenciar o trabalho, essa arquitetura está descrita na documentação oficial do Apache Airflow: [Celery Executor](https://airflow.apache.org/docs/apache-airflow/2.5.1/core-concepts/executor/celery.html)


## Arquitetura proposta
Vamos disponibilizar o serviço através do Kubernetes (EKS, GKE, VKE, etc...).
As bases de dados estaráo fora do K8S e serão utilizadas como serviço (RDS, GCP SQL, etc...).
Para melhor proveito do Airflow no ambiente K8S vamos utilizar o executor [Kubernetes Executor](https://airflow.apache.org/docs/apache-airflow/2.5.1/core-concepts/executor/kubernetes.html), onde cada DAG vai rodar em um pod.


### Monitoring
É necessário alguns cuidados importantes para que o serviço satisfaça requisitos de performance e de orçamento, portanto uma monitoria ativa é crucial.
Precisamos exportar as métricas do Airflow, infelizmente na versão `2.5.1` ele possui apenas o exporter no formato [statsd](https://github.com/statsd/statsd), porém a partir da versão `2.7.0` ele já pode expor métricas no formato [OpenTelemetry](https://opentelemetry.io/).
- [2.5.1 Doc Reference](https://airflow.apache.org/docs/apache-airflow/2.5.1/administration-and-deployment/logging-monitoring/metrics.html)
- [2.8.0 Doc Reference](https://airflow.apache.org/docs/apache-airflow/2.8.0/administration-and-deployment/logging-monitoring/metrics.html)

Pontos que ainda precisam ser contemplados:
- Logs (Exportação e Visualização)

### Performance x Custo
O Airflow possui um recurso chamado [Pools](https://airflow.apache.org/docs/apache-airflow/2.5.1/administration-and-deployment/pools.html) onde podemos configurar qual o limite de tasks podemos executar em paralelo e também criar pools específica de workers que necessitem de mais recursos, otimizando assim a alocação de recursos no cluster.