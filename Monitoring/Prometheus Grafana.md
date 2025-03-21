# AWS Instance Monitoring using Prometheus & Grafana

### 🔹 Introduction to Prometheus & Grafana
### 🔹 What is Prometheus?
#### Prometheus is an open-source monitoring system used for metrics collection, storage, and querying. It pulls real-time data from various sources (such as servers, containers, and applications) and allows users to query the data using PromQL.

#### Key Features:

#### Pull-based monitoring (scrapes metrics from targets like Node Exporter).
#### Powerful querying with PromQL.
#### Time-series database optimized for performance.
#### Alerting system integrated with tools like Alertmanager.


### 🔹 What is Grafana?
#### Grafana is a visualization tool used to create dashboards for monitoring metrics collected by Prometheus. It provides:

#### Rich dashboards with graphs, tables, and alerts.
#### Support for multiple data sources (Prometheus, MySQL, AWS CloudWatch, etc.).
#### User-friendly interface for monitoring and analytics.

🔹 Step 1: Install Docker & Docker Compose
Update system and install Docker:

bash
Copy
Edit
sudo apt update && sudo apt upgrade -y
sudo apt install -y docker.io docker-compose
Start and enable Docker:

bash
Copy
Edit
sudo systemctl enable docker
sudo systemctl start docker
Verify installation:

bash
Copy
Edit
docker --version
docker-compose --version
🔹 Step 2: Deploy Prometheus & Grafana using Docker
Create a monitoring directory:

bash
Copy
Edit
mkdir ~/monitoring && cd ~/monitoring
Create docker-compose.yml:

bash
Copy
Edit
nano docker-compose.yml
Paste the following configuration:

yaml
Copy
Edit
version: '3.8'

services:
  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    restart: always
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
    ports:
      - "9090:9090"

  grafana:
    image: grafana/grafana:latest
    container_name: grafana
    restart: always
    ports:
      - "3000:3000"
    environment:
      - GF_SECURITY_ADMIN_USER=admin
      - GF_SECURITY_ADMIN_PASSWORD=admin
    volumes:
      - grafana-storage:/var/lib/grafana

volumes:
  grafana-storage:
Create Prometheus config file:

bash
Copy
Edit
nano prometheus.yml
Paste the following configuration:

yaml
Copy
Edit
global:
  scrape_interval: 10s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']

  - job_name: 'node_exporter'
    static_configs:
      - targets: ['<instance-1-ip>:9100', '<instance-2-ip>:9100']
Replace <instance-1-ip> and <instance-2-ip> with actual AWS instance IPs.

Start Prometheus & Grafana:

bash
Copy
Edit
docker-compose up -d
Verify running containers:

bash
Copy
Edit
docker ps

