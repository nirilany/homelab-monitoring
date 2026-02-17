# Homelab Monitoring Stack (Prometheus + Grafana)

Two Ubuntu servers:
- **nir-server** (monitoring host): Prometheus + Grafana (+ Loki optional)
- **merrygo** (workhorse): node_exporter + cAdvisor

## Architecture
- Prometheus scrapes:
  - node_exporter on both servers (host metrics)
  - cAdvisor on merrygo (container metrics)
- Grafana visualizes dashboards (Node Exporter Full + cAdvisor)

## Quick start
1) Copy env:
```bash
cp .env.example .env

