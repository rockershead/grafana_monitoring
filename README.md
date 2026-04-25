Monitoring Stack: Node Exporter → Prometheus → Grafana


This project sets up a simple monitoring pipeline using:

Node Exporter → collects system metrics (CPU, memory, disk)
Prometheus → scrapes and stores metrics
Grafana → visualizes metrics via dashboards
🏗️ Architecture
Node Exporter (9100)  --->  Prometheus (9090)  --->  Grafana (3000)
     (metrics)             (scrapes data)           (visualization)
⚙️ Components
1. Node Exporter
Runs on target machine. we can use versions 1.11 or 1.7. Refer to https://docs.techdox.nz/node-exporter/ for setup instructions

Exposes system metrics at:

http://<node-ip>:9100/metrics

2. Prometheus
Scrapes metrics from Node Exporter
Stores time-series data

Example config:

scrape_configs:
  - job_name: node
    static_configs:
      - targets: ['<node-ip>:9100']
Setup:      
- cd prometheus
- docker compose up -d 

Access Prometheus UI:

http://<prometheus-ip>:9090

3. Grafana
Connects to Prometheus as a data source
Used to build dashboards
Setup:
- cd grafana
- docker compose up -d 

Access Grafana UI:

http://<grafana-ip>:3000

Default login:

Username: admin
Password: admin