# Chamber 1 - Docker Monitoring with Prometheus and Grafana

- [Requirements](#requirements)
- [How To Run](#how-to-run)

## Requirements

* Docker 20.10.14
* Docker Compose 2.3.4

## How To Run

1. Create the `grafana/secrets/admin-password.txt` file with the Grafana admin user
1. Create and starts the containers:
   ```shell
   docker compose up -d
   ```
