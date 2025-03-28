# Kafka Message Broker

## Overview
This project sets up an Apache Kafka cluster with Zookeeper using Docker Compose. It includes:
- **Zookeeper** for managing Kafka brokers.
- **Kafka** for message streaming.
- **Kafka-init** for initializing required topics.

## Prerequisites
- [Docker](https://www.docker.com/get-started)

## Services Configuration

### 1. **Zookeeper**
Zookeeper manages brokers' metadata, leader election and service discovery.
- **Port**: `2181`
- **Volumes**: Persists Zookeeper data to prevent metadata loss.
- **Environment Variables**:
  - `ZOOKEEPER_CLIENT_PORT`: Defines the client connection port (default: `2181`).

### 2. **Kafka**
Kafka is the core message broker.
- **Port**: `9093`
- **Volumes**: Persists Kafka logs to maintain topic data and messages.
- **Environment Variables**:
  - `KAFKA_BROKER_ID`: Unique identifier for the broker.
  - `KAFKA_ZOOKEEPER_CONNECT`: Zookeeper address and port.
  - `KAFKA_ADVERTISED_LISTENERS`: Specifies the advertised addresses for clients. (Uses .env file for public ip)
  - `KAFKA_LOG_DIRS`: Storage location for Kafka logs.
  - `KAFKA_DEFAULT_REPLICATION_FACTOR`: Default replication factor for topics.

### 3. **Kafka-init**
A helper service that creates predefined topics after Kafka starts.
- **Topics Created**:
  - `sensor-data`
  - `processed-data`
  - `alerts`

## Running the Project
To start the services, run:
```sh
docker-compose up -d
```
To stop the services:
```sh
docker-compose down
```
To remove all data (Warning: This will delete persisted volumes therefore messages):
```sh
docker-compose down -v
```

## Notes
- Ensure `PUBLIC_IP` is correctly set in .env file.
- Modify replication and partitions according to deploy environment.
