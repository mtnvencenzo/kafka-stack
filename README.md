
# Kafka Stack - Local Kafka Environment

This repository provides a Docker Compose setup for running a local Kafka environment in **two modes**:
- **KRaft mode** (no Zookeeper required, modern Kafka architecture)
- **Zookeeper mode** (classic Kafka architecture with Schema Registry)

Both modes include a web-based Kafka UI for easy management and monitoring.



## 📁 Contents

- `docker-compose.yml`: Docker Compose configuration for a KRaft-based (no Zookeeper) Kafka cluster
- `docker-compose-zoo.yml`: Docker Compose configuration for a classic Zookeeper-based Kafka cluster with Schema Registry
- `assets/`: Architecture diagram
- `README.md`: This documentation file

## ⚙️ Prerequisites

- Docker 24+ and Docker Compose v2

## 🏗️ Architecture

### KRaft Mode (No Zookeeper)
- **Kafka (KRaft mode)**: Distributed event streaming platform and message broker, running in KRaft (Kafka Raft) mode with no Zookeeper dependency. Three brokers are started for high availability and replication.
- **Kafka UI**: Web-based interface for managing Kafka topics, consumers, and monitoring cluster health.

![Kafka Stack](./assets/kafka-stack-kraft.drawio.svg)

### Zookeeper Mode (Classic)
- **Zookeeper**: Centralized service for maintaining configuration information and providing distributed synchronization.
- **Kafka Broker**: Classic Kafka broker connected to Zookeeper.
- **Schema Registry**: Service for managing Avro schemas for Kafka topics.
- **Kafka UI**: Web-based interface for managing Kafka topics, consumers, and monitoring cluster health.

<br/>

![Kafka Stack](./assets/kafka-stack-zoo.drawio.svg)

All containers run within a dedicated `kafka-stack` Docker bridge network for inter-service communication.

## 🚀 Setup & Usage

> This setup is designed for local development and learning. Do not use in production environments.

---

### 1. Start the Kafka stack services

#### KRaft mode:
```bash
docker compose -p kafka-stack -f docker-compose.yml up -d
```

#### Zookeeper mode:
```bash
docker compose -p kafka-stack -f docker-compose-zoo.yml up -d
```

---

### 2. Stop the services

#### KRaft mode:
```bash
docker compose -p kafka-stack -f docker-compose.yml down -v
```

#### Zookeeper mode:
```bash
docker compose -p kafka-stack -f docker-compose-zoo.yml down -v
```

---

### 3. Rebuild and restart a specific service

#### KRaft mode:
```bash
docker compose -p kafka-stack -f docker-compose.yml up -d --force-recreate --no-deps --build <service_name>
```

#### Zookeeper mode:
```bash
docker compose -p kafka-stack -f docker-compose-zoo.yml up -d --force-recreate --no-deps --build <service_name>
```

---

### 4. Check all services status
```bash
docker compose ps
```

## 🛠️ Customization

- Modify the relevant compose file to adjust service settings, ports, or environment variables.

## 📊 Service Endpoints & Ports

### KRaft Mode (`docker-compose.yml`)
Distributed event streaming platform and message broker (no Zookeeper required).

- **Docs:** [Kafka KRaft mode](https://kafka.apache.org/documentation/#kraft)
- **Ports:**
  - Broker 1: `9092` (host) → `9092` (container)
  - Broker 2: `9094` (host) → `9092` (container)
  - Broker 3: `9096` (host) → `9092` (container)
- **Kafka UI:** [http://localhost:8088](http://localhost:8088)

---

### Zookeeper Mode (`docker-compose-zoo.yml`)
Classic Kafka stack with Zookeeper and Schema Registry.

- **Docs:** [Kafka with Zookeeper](https://docs.confluent.io/platform/current/installation/docker/docs/quickstart.html)
- **Ports:**
  - Zookeeper: `2181` (host) → `2181` (container)
  - Broker: `9092` (host) → `9092` (container), `29092` (host) → `29092` (container)
  - Schema Registry: `8988` (host) → `8081` (container)
- **Kafka UI:** [http://localhost:8088](http://localhost:8088)

---

## 🐞 Troubleshooting

- Check container logs:
  ```bash
  docker compose logs -f <service>
  ```
- If Kafka UI cannot connect, ensure all Kafka brokers (and Zookeeper, if using classic mode) are running and healthy.
- Reset stack state:
  ```bash
  docker compose down -v
  ```

## ⚙️ Configuration Insights

- All services are connected via the `kafka-stack` Docker bridge network.
- Ports can be changed in the relevant compose file as needed.
- Service dependencies are managed via `depends_on` in the compose files.

## 🌐 Community & Support

- 🤝 Contributing Guide – see [.github/CONTRIBUTING.md](.github/CONTRIBUTING.md)
- 🤗 Code of Conduct – see [.github/CODE_OF_CONDUCT.md](.github/CODE_OF_CONDUCT.md)
- 🆘 Support Guide – see [.github/SUPPORT.md](.github/SUPPORT.md)
- 🔒 Security Policy – see [.github/SECURITY.md](.github/SECURITY.md)

## 📄 License

This project is licensed under the terms of the repository's main LICENSE file.
