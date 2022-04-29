# Chamber 1 - Docker Monitoring with Prometheus and Grafana

- [Requirements](#requirements)
- [How To Run](#how-to-run)
- [Applications](#applications)
- [How To Test Alerting](#how-to-test-alerting)

## Requirements

* Docker 20.10.14
* Docker Compose 2.4.1

## How To Run

1. Create the `alertmanager/config/templates/default-receiver.tmpl` file with the content as follows
   ```
   {{define "receiver.default-receiver.email.to"}}%EMAILS_PLACEHOLDER%{{end}}
   ```
   where `%EMAILS_PLACEHOLDER%` should be replaced with a comma separated list of the alert recipients, examples:
   ```
   {{define "receiver.default-receiver.email.to"}}admins@example.org{{end}}
   ```
   ```
   {{define "receiver.default-receiver.email.to"}}bob@example.org, dave@example.org, kate@example.org{{end}}
   ```
1. Create the `grafana/secrets/admin-password.txt` file with the Grafana admin user password
1. Create and starts the containers:
   ```shell
   docker compose up -d
   ```

## Applications

| Application | Url |
| --- | --- |
| [Alertmanager](https://github.com/prometheus/alertmanager) | http://localhost:9093 |
| [Grafana](https://grafana.com/grafana/) | http://localhost:3000 |
| [Node Exporter](https://github.com/prometheus/node_exporter) | http://localhost:9100 |
| [Prometheus](https://prometheus.io/) | http://localhost:9090 |

## How To Test Alerting

1. Open the [Prometheus Alerts tab](http://localhost:9090/alerts)
1. Stop the Node Exporter instance
   ```shell
   docker kill 1-docker-monitoring-node-exporter-1
   ```
1. The alert should be moved to the Pending state after around 1 minute and next to the Firing state after around 20 seconds

The alert won't send an email to the configured recipients if there is no open SMTP server on `localhost:25` (resolved from the Alertmanager application)

> ts=<timestamp> caller=notify.go:732 level=warn component=dispatcher receiver=default-receiver integration=email[0] msg="Notify attempt failed, will retry later" attempts=1 err="establish connection to server: dial tcp 127.0.0.1:25: connect: connection refused"

The event is visible in the Alertmanager application so it is good enough for the exercise purposes.
