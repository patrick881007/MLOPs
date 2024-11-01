# MLOps-01: Microservice-Based Workflow for ML Modeling with DevOps Principles

This project builds a robust machine learning workflow by integrating DevOps principles, Docker for containerization, and MLFlow for tracking and model management. The goal is to build, ship, and test this workflow rapidly, ensuring that each component is modular, scalable, and adaptable to different ML projects. The workflow includes a MinIO server for data storage, an MLFlow tracking server, and an NGINX proxy for secure access.

<p align="center">
  <img src="https://user-images.githubusercontent.com/90475308/186834245-0efa8c74-70de-4b83-a36e-34b1cf67fc64.png" alt="workflow" width="300" height="300">
</p>

## Table of Contents

1. [Project Overview](#project-overview)
2. [Process Flow](#process-flow)
3. [Architecture](#architecture)
4. [Components](#components)
5. [Data Source](#data-source)
6. [Getting Started](#getting-started)
7. [Accessing the Services](#accessing-the-services)

---

## Project Overview

In this project, we create a structured and efficient ML workflow adopting DevOps practices. By leveraging Docker for containerization and MLFlow for tracking experiments, this setup allows us to:

- Rapidly build, ship, and test models in a modular environment.
- Track and log ML experiments using MLFlow, storing metadata in MySQL and files in MinIO.
- Ensure security and ease of access using an NGINX proxy.

## Process Flow

This workflow enables end-to-end management of ML experiments, from data preprocessing and training to deployment. The following diagram shows the process flow:

<p align="center">
  <img src="https://user-images.githubusercontent.com/90475308/184595553-01c9ec73-d888-44aa-a469-5055b5deb4e1.png" alt="Process Flow" width="800" height="400">
</p>

## Architecture

The core of this workflow includes Docker containers orchestrated with `docker-compose` to run various services:
- **MLFlow Tracking Server**: For experiment logging and model versioning.
- **MinIO Server**: S3-compatible object storage for model artifacts.
- **MySQL Database**: Stores MLFlow metadata.
- **NGINX**: Manages access control with basic authentication.

<p align="center">
  <img src="https://user-images.githubusercontent.com/90475308/186097290-9fd5407f-3a1b-48c0-bf92-1bac3559828b.png" alt="MLFlow Tracking Server with Docker" width="800" height="500">
</p>

## Components

### 1. MLFlow Tracking Server

The MLFlow server allows us to track and visualize ML experiments. Data is stored in a MySQL database, and model artifacts are saved in a MinIO bucket. Access MLFlow at `http://127.0.0.1:5000`.

<p align="center">
  <img src="https://user-images.githubusercontent.com/90475308/186097218-39df0ff5-fb1a-46a6-a082-3995e4984a3f.png" alt="MLFlow Server" width="900" height="700">
</p>

### 2. MinIO

MinIO is an S3-compatible storage system used for storing model artifacts. This allows for easy management and access to large files, datasets, and model artifacts. Access MinIO at `http://127.0.0.1:9000`.

### 3. NGINX

NGINX acts as a reverse proxy for secure access to the MLFlow server and MinIO. Basic authentication is implemented to restrict access. Access NGINX at `http://127.0.0.1`.

## Data Source

For this project, use the credit card fraud detection dataset from Kaggle:

- **Dataset URL**: [Credit Card Fraud Detection](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud?resource=download)
- Download `creditcard.csv` and place it in the `mlflow` folder before starting the containers.

## Getting Started

To set up and run this project, follow these steps:

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/your-repo.git
   cd your-repo
    ```
2. Start the Docker containers:
    ```bash
    docker-compose -f docker-compose.yml up -d
    ```
3. Start training models:
    ```bash
    docker exec -it [container ID] /bin/bash
    python train.py
    ```

## Accessing the Services

- MLFlow Server: Accessible at http://127.0.0.1:5000
- MinIO Server: Accessible at http://127.0.0.1:9000
- NGINX Proxy: Accessible at http://127.0.0.1