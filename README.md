# Federated Learning–Based Smoker Classification System

## Overview

This project implements a **Federated Learning (FL)** system for smoker classification while preserving data privacy. Instead of centralizing sensitive data on a single server, model training is distributed across multiple clients, each maintaining its own local dataset. Only model updates (weights) are shared with a central server, enabling collaborative learning without exposing raw data.

## Key Features

* **Privacy-Preserving Federated Learning**
  Local training is performed on private client data, and only model weights are communicated to the server.
* **Smoker Classification Model**
  A machine learning classification model trained on the Smoking dataset.
* **Dockerized Federated Simulation**
  The system simulates a real-world federated learning environment using Docker containers.
* **Multi-Client Setup**
  Two client containers represent independent data holders.
* **Central Server Container**
  Aggregates client model weights and updates the global model.
* **Docker Compose Workflow**
  Manages synchronization between clients and the server to support multiple federated training rounds.

## Project Structure

```text
/                           # Project root
├── client1/                # Client 1 code and local data subset
├── client2/                # Client 2 code and local data subset
├── server/                 # Central server code and global model
├── Smoking/                # Smoking dataset used for classification
├── docker-compose.yml      # Container orchestration and workflow synchronization
└── README.md               # Project documentation
```

## Components Description

### Clients (client1 & client2)

Each client trains a local model on its respective subset of the Smoking dataset and sends the updated model weights to the server.

### Server

The server receives model updates from all clients, aggregates them using **federated averaging (FedAvg)**, and updates the global model. The updated model is then redistributed to the clients for the next training round.

### Docker Compose

Docker Compose is used to launch and synchronize the three containers (two clients and one server), effectively simulating federated learning rounds.

## How It Works

1. The server initializes the global model.
2. Each client loads its local data subset and receives the current global model.
3. Clients perform local training and send updated weights to the server.
4. The server aggregates the received weights using federated averaging.
5. The updated global model is sent back to the clients.
6. Steps 2–5 repeat for a predefined number of federated rounds.
7. The final global model can be evaluated on test data.

## Getting Started

### Prerequisites

* Docker installed on your machine
* Docker Compose installed

### Running the Project

1. Clone the repository:

   ```bash
   git clone <repository-url>
   cd <repository-folder>
   ```

2. Start the federated learning simulation:

   ```bash
   docker-compose up --build
   ```

   This command builds and launches the three containers (two clients and one server) and starts the federated training workflow.

3. Monitor container logs to track training progress and weight updates.

4. Stop the simulation:

   ```bash
   docker-compose down
   ```

## Dataset

The **Smoking dataset** is used for classification and is partitioned across clients to simulate data heterogeneity in a federated learning setting.

## Technologies Used

* Python (model training and aggregation)
* Docker & Docker Compose (containerization and orchestration)
* Federated Learning concepts (FedAvg algorithm)
* Machine Learning framework (TensorFlow)

---
