
# Monitoring with Prometheus, Grafana, and Alertmanager

This repository contains a hands-on lab for setting up a complete **monitoring solution** using **Prometheus**, **Grafana**, **Node Exporter**, **cAdvisor**, and **Alertmanager**. It also includes a custom app, **obs-sim-app**, to simulate observability metrics and trigger alerts.

---

## 🧭 Overview

The monitoring stack includes:

- **Prometheus** – Collects and stores metrics from system, containers, and apps.
- **Grafana** – Visualizes all metrics in dashboards.
- **Node Exporter** – Exposes system-level metrics (CPU, memory, disk).
- **cAdvisor** – Monitors container-level metrics like CPU and memory usage.
- **obs-sim-app** – A simulator app used to generate CPU and memory load (monitored by cAdvisor).
- **Alertmanager** – Sends alerts (e.g., to Slack) when metrics cross thresholds like high CPU.

---

## ✨ Features

- Preconfigured Prometheus that scrapes metrics from:
  - `Node Exporter` (System monitoring)
  - `cAdvisor` (Container monitoring)
  - `obs-sim-app` (Custom simulator app for testing alerts)
- Grafana dashboards to visualize:
  - System metrics
  - Container metrics
- Alertmanager triggers **Slack notifications** when CPU usage goes beyond **60%**
- Docker volumes for persistent Grafana dashboards
- Simple setup using Docker Compose

---

## ⚙️ Prerequisites

- Docker and Docker Compose installed
- Basic understanding of monitoring tools (Prometheus, Grafana)
- Slack Webhook URL if using Slack alerts

---

## 🚀 Getting Started

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/ignatus-anim/prometheus-grafana-repo.git
   cd prometheus_lab
   ```

2. **Start the Monitoring Stack**:
   ```bash
   docker-compose up -d
   ```

3. **Access the Interfaces**:
   - **Prometheus**: [http://localhost:9090](http://localhost:9090)
   - **Grafana**: [http://localhost:3000](http://localhost:3000)  
     - Username: `admin`, Password: `admin`
   - **Node Exporter**: [http://localhost:9100/metrics](http://localhost:9100/metrics)
   - **cAdvisor**: [http://localhost:8080](http://localhost:8080)
   - **obs-sim-app**: [http://localhost:5000](http://localhost:5000)
   - **Alertmanager**: [http://localhost:9093](http://localhost:9093)

4. **Import Grafana Dashboards**:
   - Use the provided JSONs or create your own to visualize system and container metrics.

5. **Trigger an Alert**:
   - Open `obs-sim-app` and raise the CPU load above 60% to trigger a Slack alert via Alertmanager.

---

## 🔧 Prometheus Configuration

Here’s a summary of the `prometheus.yml` config used:

```yaml
global:
  scrape_interval: 15s

alerting:
  alertmanagers:
    - static_configs:
        - targets: ['alertmanager:9093']

rule_files:
  - "alert.rules.yml"

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['prometheus:9090']

  - job_name: 'node-exporter'
    static_configs:
      - targets: ['node-exporter:9100']

  - job_name: 'cadvisor'
    static_configs:
      - targets: ['cadvisor:8080']

  - job_name: 'obs-sim-app'
    static_configs:
      - targets: ['obs-sim-app:5000']
```

---

## 🛠️ Service Descriptions

- **Node Exporter**: Collects system-level metrics from the host machine.
- **cAdvisor**: Tracks CPU and memory usage of running containers.
- **obs-sim-app**: Lets you simulate CPU/memory pressure to test alerting.
- **Prometheus**: Scrapes metrics from the above services and stores them.
- **Grafana**: Displays metrics in dashboards.
- **Alertmanager**: Sends Slack notifications based on Prometheus alert rules.

---

## 📸 Screenshots

Screenshots are available in the `assets` folder, including:
- Grafana dashboards (showing system and container metrics)
- Slack notifications for high CPU alerts

---

## 📝 Notes

- `grafana-storage` volume ensures dashboards and config are saved.
- You can modify `prometheus.yml` to add more scrape targets.
- Edit `alert.rules.yml` to create new alert conditions.
- `obs-sim-app` is very useful for testing real-time alerts.

