## Docker + K8s + Jenkins Overview

### 🚢 Docker → Containerization

### ☸️ Kubernetes → Container Orchestration

### 🔁 Jenkins → Continuous Integration & Deployment (CI/CD)

---

## Application Architecture

### 1. Frontend (UI Layer)

Technologies: HTML, CSS, JS, Angular, ReactJS

### 2. Backend (Business Logic)

Technologies: Java, Python, .NET

### 3. Database (Storage)

Technologies: MySQL, SQL Server, MongoDB, Oracle

Application Stack Example: Java + Angular 16 + MySQL → hosted via Tomcat

To run this application, all dependencies (Java, MySQL, Angular, Tomcat) must be set up in all environments.

---

## Application Environments

| Environment | Purpose                               |
| ----------- | ------------------------------------- |
| DEV         | Developers integrate and test code    |
| SIT         | System Integration Testing by QA Team |
| UAT         | User Acceptance Testing by Client     |
| PILOT       | Pre-production testing                |
| PROD        | Live environment (used by end users)  |

---

## Why Docker?

As DevOps engineers, maintaining setup consistency across all environments is challenging:

* Version mismatches
* Manual setup errors

Docker solves this by packaging app code + all dependencies → **Container**

---

## Docker Essentials

### What is Docker?

* Open source containerization tool
* Makes apps portable
* Containers include app code + required dependencies

### Key Components

1. **Dockerfile** – Instructions to build the image
2. **Docker Image** – Built artifact (code + dependencies)
3. **Docker Registry (Hub)** – Stores Docker Images
4. **Docker Container** – Running instance of Docker Image

---

## Docker Architecture Diagram

```mermaid
graph TD
    Dockerfile -->|build| DockerImage
    DockerImage -->|run| Container1[Container (Windows VM)]
    DockerImage -->|run| Container2[Container (Mac VM)]
    DockerImage -->|run| Container3[Container (Linux VM)]
    DockerImage -->|push| DockerHub
```

---

## Dev vs SIT Environment Setup

Both DEV and SIT environments require:

* Tomcat Server
* Java 17
* Angular 16
* MySQL
* OS

Without Docker, these setups are manual and error-prone. Docker solves this via containers.

---

## Port Mapping

Example Command:

```bash
$ docker run -d -p 8484:8080 telusko/spring-boot-app
```

### Mapping

* **-p 8484:8080** → Maps Host\:Container ports

### Docker Port Diagram

```mermaid
graph TD
    HostMachine((Host Machine))
    subgraph Docker Engine [Docker Engine - Linux OS]
    GuestVM[Guest VM (Linux)]
    GuestVM --> C1[Docker Container 1: -p 8485:9090]
    GuestVM --> C2[Docker Container 2: -p 8585:80]
    end
    HostMachine --> DockerEngine
```

> 🔴 Note: Two containers cannot map to the same host port.

---

## Docker Installation on Linux VM

### Steps:

1. Launch EC2 Linux VM
2. Connect via SSH (e.g., Git Bash)
3. Run:

```bash
$ sudo yum update -y
$ sudo yum install docker -y
$ sudo usermod -aG docker ec2-user
$ docker -v
```

---

## Docker Commands Reference

```bash
$ docker images                    # List all docker images
$ docker ps                        # List running containers
$ docker ps -a                     # List all (running + stopped) containers
$ docker pull <image-name>        # Pull image from Docker Hub
$ docker run <image-id/name>      # Run a container
$ docker rmi <image-id/name>      # Remove image
$ docker rm <container-id>        # Remove container
$ docker stop <container-id>      # Stop container
$ docker start <container-id>     # Start stopped container
$ docker system prune -a          # Cleanup all unused data
$ docker logs <container-id>      # View container logs
$ docker run -d <image-id/name>   # Run container in detached mode
```

---

## Dockerfile

Dockerfile defines the blueprint for building docker images.

### Key Instructions:

* `FROM`: Base image
* `MAINTAINER`: Author info
* `RUN`: Commands to execute during build
* `CMD`: Default command to run
* `COPY`: Copy files
* `ADD`: Copy + extract files
* `WORKDIR`: Working directory
* `EXPOSE`: Expose container port
* `ENTRYPOINT`: Main command
* `USER`: Set user

---

Let me know if you’d like Kubernetes or Jenkins parts documented next!
