# Kafka Stack - Local Kafka Environment


This repository provides a Docker Compose setup for running a local Kafka environment using modern Kafka KRaft mode (no Zookeeper required). It includes a multi-broker Kafka cluster and a web-based Kafka UI for easy management and monitoring.

![Kafka Stack](./assets/kafka-stack.drawio.svg)

## 📁 Contents

- `docker-compose.yml`: Docker Compose configuration for a KRaft-based (no Zookeeper) Kafka cluster
- `assets/`: Architecture diagram
- `README.md`: This documentation file

## ⚙️ Prerequisites

- Docker 24+ and Docker Compose v2

## 🏗️ Architecture

The stack provides the following services:

- **Kafka (KRaft mode)**: Distributed event streaming platform and message broker, running in KRaft (Kafka Raft) mode with no Zookeeper dependency. Three brokers are started for high availability and replication.
- **Kafka UI**: Web-based interface for managing Kafka topics, consumers, and monitoring cluster health.

All containers run within a dedicated `kafka-stack` Docker bridge network for inter-service communication.

## 🚀 Setup & Usage

> This setup is designed for local development and learning. Do not use in production environments.


0.1 Create local directories for persistent data:
  ```bash
  mkdir -p "${HOME}/mnt"
  mkdir -p "${HOME}/mnt/kafka-stack"
  mkdir -p "${HOME}/mnt/kafka-stack/kafka-1-data"
  mkdir -p "${HOME}/mnt/kafka-stack/kafka-2-data"
  mkdir -p "${HOME}/mnt/kafka-stack/kafka-3-data"
  ```

1. Start the Kafka stack services:
  ```bash
  docker compose -p kafka-stack -f docker-compose.yml up -d
  ```

2. **Stop the services:**
  ```bash
  docker compose -p kafka-stack -f docker-compose.yml down -v
  ```

3. **Rebuild and restart a specific service:**
  ```bash
  docker compose -p kafka-stack -f docker-compose.yml up -d --force-recreate --no-deps --build <service_name>
  ```

4. **Check all services status:**
  ```bash
  docker compose ps
  ```

## 🛠️ Customization

- Modify `docker-compose.yml` to adjust service settings, ports, or environment variables.

## 📊 Service Endpoints & Ports


### Kafka (KRaft mode)
Distributed event streaming platform and message broker (no Zookeeper required).

- **Docs:** [Kafka KRaft mode](https://kafka.apache.org/documentation/#kraft)
- **Ports:**
  - Broker 1: `9092` (host) → `9092` (container)
  - Broker 2: `9094` (host) → `9092` (container)
  - Broker 3: `9096` (host) → `9092` (container)

### Kafka UI
Web-based interface for managing Kafka topics, consumers, and monitoring cluster health.

- **Docs:** [Kafka UI](https://github.com/provectus/kafka-ui)
- **UI:** [http://localhost:8088](http://localhost:8088)

## 🐞 Troubleshooting

- Check container logs:
  ```bash
  docker compose logs -f <service>
  ```
- If Kafka UI cannot connect, ensure all Kafka brokers are running and healthy.
- Reset stack state:
  ```bash
  docker compose down -v
  ```

## ⚙️ Configuration Insights

- All services are connected via the `kafka-stack` Docker bridge network.
- Ports can be changed in `docker-compose.yml` as needed.
- Service dependencies are managed via `depends_on` in the compose file.

## 🌐 Community & Support

- 🤝 Contributing Guide – see [.github/CONTRIBUTING.md](.github/CONTRIBUTING.md)
- 🤗 Code of Conduct – see [.github/CODE_OF_CONDUCT.md](.github/CODE_OF_CONDUCT.md)
- 🆘 Support Guide – see [.github/SUPPORT.md](.github/SUPPORT.md)
- 🔒 Security Policy – see [.github/SECURITY.md](.github/SECURITY.md)

## 📄 License

This project is licensed under the terms of the repository's main LICENSE file.
