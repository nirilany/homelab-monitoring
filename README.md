# Homelab Monitoring Stack

A self-hosted monitoring stack built on Docker Compose using Prometheus, Grafana, Loki, and exporters.

This project monitors two Linux servers in a home lab environment:

- **nir-server** – monitoring node (Prometheus, Grafana, Loki)
- **merrygo** – compute node (containers, workloads, metrics source)

---

## Architecture

+------------------+ +------------------+
| merrygo | | nir-server |
|------------------| |------------------|
| Node Exporter | -----> | Prometheus |
| cAdvisor | -----> | |
| Docker workloads | | Grafana |
| | | Alertmanager |
+------------------+ | Loki (logs) |
+------------------+


All services are containerized and orchestrated with Docker Compose.

---

## Stack Components

### Metrics
- **Prometheus** – metrics collection and querying
- **Node Exporter** – host-level metrics (CPU, RAM, disk, network)
- **cAdvisor** – container-level metrics (CPU, memory, restarts)

### Visualization
- **Grafana**
  - Provisioned data sources
  - Auto-loaded dashboards:
    - Node Exporter Full
    - Docker / cAdvisor

### Logs
- **Loki** – log storage
- **Promtail** – log shipping (optional / expandable)

### Alerting
- **Alertmanager**
  - Configured and wired to Prometheus
  - Alert rules defined under `prometheus/rules/`

---

## Repository Structure

homelab-monitoring/
├── docker-compose.yml
├── prometheus/
│ ├── prometheus.yml
│ └── rules/
│ └── alerts.yml
├── grafana/
│ └── provisioning/
│ ├── datasources/
│ └── dashboards/
├── alertmanager/
│ └── alertmanager.yml
├── docs/
└── README.md


---

## Usage

```bash
docker compose up -d

Grafana
http://<nir-server-ip>:3000

Prometheus
http://<nir-server-ip>:9090

## Goals of This Project

- Practice real-world observability tooling
- Build production-like monitoring patterns
- Serve as a base for future extensions:
 - Database monitoring
 - Service-level alerts
 - GitOps workflows
 - CI validation of configs

## Future Work
- Telegram / Slack alerting
- PostgreSQL + exporter
- Backup strategy
- TLS + authentication
- Multi-environment support

## Author
- built and maintained by Nir Ilany

