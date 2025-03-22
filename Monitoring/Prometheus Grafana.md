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

## 🔹 Step 1: Install Docker & Docker Compose
#### Update system and install Docker:
```
sudo apt update && sudo apt upgrade -y
sudo apt install -y docker.io docker-compose
```

#### Start and enable Docker:
```
sudo systemctl enable docker
sudo systemctl start docker
````

Verify installation:
```
docker --version
docker-compose --version
```

## 🔹 Step 2: Deploy Prometheus & Grafana using Docker

#### Create a monitoring directory:
```
mkdir ~/monitoring && cd ~/monitoring
```

#### Create docker-compose.yml:
```
nano docker-compose.yml
```

Paste the following configuration:
```
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
```

#### Create Prometheus config file:
```
nano prometheus.yml
```

#### Paste the following configuration:
```
global:
  scrape_interval: 10s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']

  - job_name: 'node_exporter'
    static_configs:
      - targets: ['<instance-1-ip>:9100', '<instance-2-ip>:9100']
```
#### Replace <instance-1-ip> and <instance-2-ip> with actual AWS instance IPs.

#### Start Prometheus & Grafana:
```
docker-compose up -d
```

Verify running containers:
```
docker ps
```

## 🔹 Step 3: Install Node Exporter on Instance

#### Create a Node Exporter Directory
```
mkdir -p ~/node-exporter && cd ~/node-exporter
```

#### Create docker-compose.yml
```
nano docker-compose.yml
```

#### Paste the following content:
```
version: '3.8'

services:
  node-exporter:
    image: prom/node-exporter:latest
    container_name: node-exporter
    restart: always
    ports:
      - "9100:9100"
    networks:
      - monitoring
    command:
      - "--path.procfs=/host/proc"
      - "--path.sysfs=/host/sys"
    volumes:
      - "/proc:/host/proc:ro"
      - "/sys:/host/sys:ro"

networks:
  monitoring:
    driver: bridge
```

#### Explanation:

#### Exposes port 9100 (default for Node Exporter).
#### Mounts system directories to allow metric collection.
#### Uses bridge network for easier Prometheus integration.

#### Run the container using Docker Compose:
```
docker-compose up -d
```

## 🔹 Step 4: Add Prometheus as Data Source in Grafana
#### Open Grafana at http://<your-instance-ip>:3000.
#### Login with:
#### Username: admin
#### Password: admin
<img width="925" alt="image" src="https://github.com/user-attachments/assets/b6f6d32f-c9ab-4ed3-a610-1f3a5216f811" />

#### Go to Settings → Data Sources.
##### Click "Add Data Source" → Select Prometheus.
<img width="921" alt="prometheus1" src="https://github.com/user-attachments/assets/c7f83348-c6e2-40e7-a595-0d86df342879" />


#### Set URL as:
```
http://prometheus:9090
```
#### Click "Save & Test".

<img width="930" alt="prometheus2" src="https://github.com/user-attachments/assets/ef48c3fd-07c0-499b-b56d-3693d9115e0b" />

<img width="863" alt="prometheus3" src="https://github.com/user-attachments/assets/721bbdc8-cc79-436c-9ccb-b3f1f3dbc837" />
<img width="535" alt="prometheus4" src="https://github.com/user-attachments/assets/2e893f6c-acd3-4642-801d-95c34f2dbbd1" />


## 🔹 Step 5: Import Grafana Dashboard
#### Click Dashboards → Import.
<img width="931" alt="prometheus5" src="https://github.com/user-attachments/assets/cde272e0-5446-4d1d-991a-a883ae7a062d" />


#### Enter Dashboard ID 1860 (Node Exporter Full Dashboard).
<img width="941" alt="prometheu6" src="https://github.com/user-attachments/assets/cb915873-4282-4645-8202-ec8084995641" />

#### Click Load → Select Prometheus as data source.
#### Click Import.
### Now you should see real-time metrics! 🎯
<img width="943" alt="prometheus7" src="https://github.com/user-attachments/assets/f761d8bd-81c8-437b-8c24-96558b6127a3" />

