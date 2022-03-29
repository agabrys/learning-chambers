# Chamber 1 - Docker Monitoring with Prometheus and Grafana

- [Requirements](#requirements)
- [How To Run](#how-to-run)

## Requirements

* Docker 20.10.14
* Docker Compose 2.3.4

## How To Run

```shell
echo <password> | docker secret create grafana-admin -
```

```shell
docker compose up -d
```