## Dockerizing Java Web App

### Maven Project Setup

```bash
mvn archetype:generate -DgroupId=com.telusko -DartifactId=my-web-app \
-DarchetypeArtifactId=maven-archetype-webapp \
-DarchetypeVersion=1.4 -DinteractiveMode=false
```

```bash
cd my-web-app
mvn clean package
```

### Dockerfile

```Dockerfile
FROM tomcat:latest
MAINTAINER HaiderTelusko
EXPOSE 8080
COPY target/my-web-app.war /usr/local/tomcat/webapps/
```

### Build & Run

```bash
docker build -t java-web-app .
docker run -d -p 8080:8080 java-web-app
```

> 🔓 Enable port 8080 in security group, access via `<public-ip>:8080/my-web-app/`

---

## Dockerizing Spring Boot App

```bash
git clone https://github.com/Haider7214/SpringBootApp.git
cd SpringBootApp
mvn clean package
```

### Dockerfile

```Dockerfile
FROM openjdk:17
MAINTAINER LakshmiMadala
COPY target/jarfile /usr/app/
WORKDIR /usr/app
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "jarfileName"]
```

### Commands

```bash
docker build -t springbootapp .
docker run -d springbootapp
docker logs <container-id>
```

---

## Dockerizing Python Web App

Coming soon...

---

## Summary

* Architecture, tech stack, environments
* Docker need and architecture
* Dockerfile, image, registry, containers
* Dockerfile instructions
* Docker image pull, build, run
* Port mapping and detached mode
* Dockerizing Java, Spring Boot apps

---

## Docker Network

### Purpose

* Allows **container communication** via isolated network

### Default Docker Networks

* **bridge** – default for containers, assigns IP
* **host** – container shares host’s network
* **none** – no networking

### Advanced Networks

#### Overlay Network

* Used in Docker Swarm
* Multi-host secure communication

#### Macvlan Network

* Assigns **real LAN IP** to containers
* Useful for legacy systems

### Commands

```bash
docker network ls
# Create
$ docker network create telusko-network
# Inspect
$ docker network inspect telusko-network
# Remove
$ docker network rm telusko-network
```

### Usage

```bash
cd my-web-app
docker build -t my-web-app .
docker run -d -p 8080:8080 --network telusko-network my-web-app
```

---

## Docker Compose

Used for managing multi-container Docker apps.

### Features

* One YAML file to define services
* One command to manage containers

### Sections in Compose File

* **version** – Docker Compose version
* **services** – container definitions
* **networks** – custom networks
* **volumes** – storage setup

### Install Compose

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/v2.24.6/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

### docker-compose.yml

```yaml
version: "3"
services:
  application:
    image: springboot-app
    ports:
      - "8080:8080"
    networks:
      - telusko-net
    depends_on:
      - mysqldb
    volumes:
      - /data/springboot-app

  mysqldb:
    image: mysql:8.3
    networks:
      - telusko-net
    ports:
      - "3306:3306"
    environment:
      - MYSQL_ROOT_PASSWORD=root
      - MYSQL_DATABASE=sbms
    volumes:
      - /data/mysql

networks:
  telusko-net:
```

### Dockerfile (Spring Boot App)

```Dockerfile
FROM openjdk:17
MAINTAINER HaiderTelusko
EXPOSE 8080
COPY target/CrmWebbAPP.jar usr/app/
ENTRYPOINT ["java", "-jar", "/CrmWebbAPP.jar"]
```

### Docker Compose Commands

```bash
docker-compose up -d
docker-compose ps
docker-compose stop
docker-compose start
```
