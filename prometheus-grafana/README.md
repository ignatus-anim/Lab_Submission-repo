# Monitoring A Server with Prometheus, Grafana, and Node Exporter

This repository provides a simple monitoring stack using **Prometheus**, **Grafana**, and **Node Exporter**. It allows you to monitor system metrics and visualize them using Grafana dashboards.

---

## **Overview**

The monitoring stack consists of the following components:

- **Prometheus**: A powerful open-source monitoring and alerting toolkit.
- **Grafana**: A visualization tool for creating interactive dashboards.
- **Node Exporter**: Exposes hardware and OS-level metrics (CPU, memory, disk, etc.) to Prometheus.


## **Features**

- Pre-configured Prometheus to scrape metrics from Node Exporter.
- Grafana dashboard to visualize system metrics.
- Persistent storage for Grafana data using Docker volumes.
- Easy setup with Docker Compose.

---

## **Prerequisites**

- Docker and Docker Compose installed on your system.
- Basic knowledge of Docker and monitoring tools.
- Docker compose file 
- Prometheus rules 

---

## **Getting Started**

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/ignatus-anim/prometheus-grafana-repo.git
   cd prometheus_lab
   ```

2. **Start the Stack**:
   Run the following command to start Prometheus, Grafana, and Node Exporter:
   ```bash
   cd assets
   docker-compose up -d
   ```

3. **Access the Tools**:
   - **Prometheus**: Open [http://localhost:9090](http://localhost:9090) in your browser.
   - **Grafana**: Open [http://localhost:3000](http://localhost:3000) in your browser.
     - **Default Login**:
       - Username: `admin`
       - Password: `admin`

4. **Import Grafana Dashboard**:
   - Use the provided JSON file or create your own dashboard to visualize metrics.

---

## **Services**

### **Prometheus**
- Scrapes metrics from Node Exporter.
- Accessible at [http://localhost:9090](http://localhost:9090).

### **Grafana**
- Visualizes metrics collected by Prometheus.
- Accessible at [http://localhost:3000](http://localhost:3000).
- Default admin credentials: `admin/admin`.

### **Node Exporter**
- Collects system-level metrics (CPU, memory, disk, etc.).
- Metrics are exposed at [http://localhost:9100/metrics](http://localhost:9100/metrics).

---

## **Stopping the Stack**

To stop the monitoring stack, run:
```bash
docker-compose down
```

---

## **Notes**

- The `grafana-storage` volume ensures that your Grafana dashboards and settings persist even after restarting the containers.
- You can customize the `prometheus.yml` file to add additional scrape targets or alerting rules.

---