# Federated Learning–Based Smoker Classification System

## Overview
This project implements a Federated Learning system to train a machine learning model for smoker classification while preserving data privacy. Instead of pooling sensitive data in a central server, the training is distributed across multiple clients, each having their own local dataset. Model updates (weights) are shared and aggregated centrally, enabling collaborative training without exposing raw data.

## Key Features
- **Privacy-Preserving Federated Learning**: Local training on clients’ private data with only model weight updates communicated to the server.
- **Smoker Classification Model**: A classification model trained on the Smoking dataset.
- **Dockerized Simulation**: The system simulates a real federated environment using Docker containers.
- **Multi-Client Setup**: Two client containers simulate independent data holders.
- **Central Server Container**: Aggregates client model weights and updates the global model.
- **Docker Compose Workflow**: Orchestrates synchronization between clients and server for seamless federated training rounds.

## Project Structure:
/                           # Project root
├── client1/                # Client 1 code and local data subset
├── client2/                # Client 2 code and local data subset
├── server/                 # Central server code and global model
├── Smoking/                # Smoking dataset used for classification
├── docker-compose.yml      # Orchestration of containers and workflow synchronization
└── README.md               # This file


## Components Description

### Clients (client1 & client2)
Each client trains the local model on its subset of the Smoking dataset and sends the updated model weights to the server.

### Server
The server aggregates received weights from all clients using federated averaging and updates the global model. Then, it distributes the updated global model back to the clients for the next training round.

### Docker Compose
Used to launch and synchronize the three containers (2 clients + 1 server) to simulate federated rounds effectively.

## How It Works
1. The server initializes the global model.
2. Each client loads its local data subset and receives the current global model.
3. Clients perform local training and send updated weights to the server.
4. The server performs federated averaging of the weights from all clients.
5. The updated global model is sent back to clients.
6. Steps 2-5 repeat for a predefined number of federated rounds.
7. The final global model can be evaluated on test data.

## Getting Started

### Prerequisites
- Docker installed on your machine
- Docker Compose installed

### Running the Project
1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd <repository-folder>

2-Start the federated learning simulation using Docker Compose:
docker-compose up --build

This will build and launch the 3 containers (2 clients + 1 server) and start the federated training workflow.
3-Monitor logs from each container to track training progress and weight updates.
4-To stop the simulation

docker-compose down

Dataset
The Smoking dataset is used for classification. It is partitioned across clients to simulate data heterogeneity in federated learning.
Technologies Used

Python (for model training and aggregation)
Docker & Docker Compose (for containerization and orchestration)
Federated Learning concepts (e.g., FedAvg algorithm)
Machine Learning framework (e.g., TensorFlow, PyTorch - specify if known)
