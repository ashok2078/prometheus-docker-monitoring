## Prometheus Monitoring Setup using Docker Compose ##
** This repository contains a professional setup for monitoring Linux host metrics using Prometheus and Node Exporter. **
++ Prometheus is an open-source systems monitoring and alerting toolkit. In this project, it is configured to scrape hardware and OS metrics exposed by Node <img width="1319" height="678" alt="image" src="https://github.com/user-attachments/assets/1b887387-3907-4cae-b6ac-d7ae73d748c9" />
Exporter.

 Tech Stack

    Prometheus: Monitoring & Time-series database.

    Node Exporter: Metric exporter for machine metrics.

    Docker & Docker Compose: Container orchestration.

    Linux (CentOS/RHEL): Host Environment.

**Project Structure **

prometheus-project/
docker-compose.yml    # Defines the services and networking
prometheus.yml        # Main configuration for scraping targets

Configuration Details

Docker Compose

The docker-compose.yml file manages two services on a dedicated bridge network:

    Prometheus (Port 8082 mapped to 9090)

    Node Exporter (Port 9100)


******* Key Monitoring Queries *******

Use these PromQL expressions in the Prometheus dashboard:

    Current CPU Usage (%):
    100 - (avg by (instance) (rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)

    Available Memory (GB):
    node_memory_MemFree_bytes / 1024 / 1024 / 1024
