# Prometheus Monitoring

Docker-based Prometheus setup with Node Exporter.

## Quick Start

# Prerequisites

- **Docker** installed (Version 20.10+)
- **Docker Compose** installed (Version 2.0+)
- **Linux VM** (CentOS)
- Minimum 2GB RAM, 10GB disk space
- <img width="1345" height="679" alt="image" src="https://github.com/user-attachments/assets/e986ee05-4219-4f32-bbf1-c1f480720f4b" />


**Check versions:**
```bash
docker --version
docker-compose --version

Create Project Directory
bash
mkdir -p ~/prometheus-project
cd ~/prometheus-project

**Create Prometheus Configuration**
*prometheus.yml

cat > prometheus.yml <<'EOF'
global:
  scrape_interval: 15s      # How often to scrape metrics
  evaluation_interval: 15s  # How often to evaluate rules

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']

  - job_name: 'node-exporter'
    static_configs:
      - targets: ['node-exporter:9100']
EOF

**Create Docker Compose File ***

File ** docker-compose.yml **

cat > docker-compose.yml <<'EOF'
version: '3.8'

services:
  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    restart: unless-stopped
    ports:
      - "9091:9090"
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml:ro
      - prometheus_data:/prometheus
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.path=/prometheus'

  node-exporter:
    image: prom/node-exporter:latest
    container_name: node-exporter
    restart: unless-stopped
    ports:
      - "9100:9100"
    volumes:
      - /proc:/host/proc:ro
      - /sys:/host/sys:ro
      - /:/rootfs:ro

volumes:
  prometheus_data:
EOF
Step 4: Start the Stack
bash

** Start the Stack **

docker-compose up -d
# Start all services in background
docker-compose up -d

# Check if containers are running
docker-compose ps

# View logs
docker-compose logs -f

# check docker status
systemctl status docker

# Restart docker again
systemctl restart docker

#check for all container
docker ps -a

# all in firewall port 8082
firewall-cmd --permanent --add-port=8082/tcp




```bash
docker-compose up -d
