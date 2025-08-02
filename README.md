# Full Stack Docker Environment

This project uses Docker Compose to set up a complete development environment that includes a Spring Boot application and several backing services.

## Overview

The environment consists of the following services:

* **`spring-app`**: The main Spring Boot application.
* **`postgres-db`**: A PostgreSQL database for the Spring Boot application.
* **`keycloak`**: An identity and access management solution.
* **`keycloak-db`**: A dedicated PostgreSQL database for Keycloak.
* **`rabbitmq`**: A message broker for asynchronous communication.
* **`minio`**: An S3-compatible object storage server.

## Prerequisites

* [Docker](https://www.docker.com/get-started) must be installed and running on your machine.
* [Docker Compose](https://docs.docker.com/compose/install/) (usually included with Docker Desktop).

## Getting Started

1.  **Clone the repository** or make sure you have all the project files, including `docker compose.yml` and your Spring Boot application source code with its `Dockerfile`.
2.  **Open a terminal** in the root directory of the project.
3.  **Build and start all services** by running the following command:

    ```bash
    docker compose up --build
    ```

    * The `--build` flag will build the image for your `spring-app` the first time you run it.
    * If you just want to start the services without rebuilding, you can run `docker compose up`.

## Service Access Details

Once the containers are running, you can access each service at the following endpoints:

---

### 1. Your Spring Boot Application

* **URL**: `http://localhost:8081`
* **Description**: The main application. Check your code for available API endpoints (e.g., `http://localhost:8081/swagger-ui/index.html`).
* **Database Connection**: The app connects to the `postgres-db` container internally.

---

### 2. Keycloak (Identity Management)

* **Admin Console URL**: `http://localhost:8080`
* **Admin Username**: `admin`
* **Admin Password**: `admin`
* **Description**: Used for managing users, roles, and authentication.

---

### 3. RabbitMQ (Message Broker)

* **Management Dashboard URL**: `http://localhost:15672`
* **Default Username**: `guest`
* **Default Password**: `guest`
* **Description**: Used for managing queues, exchanges, and messages.

---

### 4. MinIO (Object Storage)

* **Web UI Console URL**: `http://localhost:9001`
* **Root User (Access Key)**: `minioadmin`
* **Root Password (Secret Key)**: `minioadmin`
* **Description**: An S3-compatible object storage for files, images, etc. The API is available on port `9000`.

---

### 5. PostgreSQL Databases

* **`postgres-db` (for Spring App)**:
    * **Host Port**: `5433`
    * **Description**: Not typically accessed directly from the host. Your Spring app connects to it internally on port `5432`.
* **`keycloak-db` (for Keycloak)**:
    * **Host Port**: Not exposed to the host machine.
    * **Description**: Used exclusively by the Keycloak service.

## Stopping the Environment

To stop all running containers, press `Ctrl + C` in the terminal where `docker compose` is running.

To stop and remove the containers completely, run:

```bash
docker compose down

To remove the database volumes as well (this will delete all your data), run:

docker compose down -v
