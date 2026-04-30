# Document Pipeline Development Infrastructure

This repo contains the local development infrastructure for the document pipeline project, using Docker Compose to run the required services locally.

## Services

| Service | Description | URL |
|---|---|---|
| `kafka` | Message broker | `localhost:9092` |
| `kafka-ui` | Web UI for inspecting Kafka topics and messages | http://localhost:8080 |

## Prerequisites

- Docker Desktop

## Getting Started

1. **Clone the repo**
   ```bash
   git clone <repo-url>
   cd dev-infrastructure
   ```

2. **Create your `.env` file**
   ```bash
   cp .env.example .env
   ```
   Fill in the required values in `.env` (see `.env.example` for reference).

3. **Start the services**
   ```bash
   docker-compose up -d
   ```

4. **Verify everything is running**
   ```bash
   docker-compose ps
   ```
   Then open http://localhost:8080 — if Kafka UI shows the `local` cluster as connected, everything is working.

5. **Stop the services**
   ```bash
   docker-compose down
   ```

## Microservices

This infrastructure supports the following microservices:

- **Ingestion Service** — receives documents and publishes them to the `documents` Kafka topic
- **Summarization Service** — consumes documents from the `documents` Kafka topic, summarizes them, and stores results in Postgres

Both services connect to Kafka at `localhost:9092` when running locally outside of Docker.