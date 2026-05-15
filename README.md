# 🚀 DevOps Hands-on Lab: Docker, Maven, Jenkins & CI/CD

Welcome to my DevOps practice repository.  
This repo is a collection of my hands-on tasks, notes, commands, and CI/CD practice work based on **Docker, Maven, Jenkins, Docker Compose, and GitHub Actions**.

The goal of this repository is not only to store commands, but to show my practical DevOps learning journey from basic container setup to automated CI/CD pipelines.

---

## 🎯 What This Repository Covers

This repository includes practical work on:

- Docker container creation and management
- Apache and NGINX web server containers
- Docker volumes and persistent storage
- Docker networking and bridge networks
- MySQL container setup
- Multi-container applications using Docker Compose
- Maven build automation for Java projects
- Maven Wrapper usage
- Dockerizing Java applications
- Jenkins CI/CD pipeline concepts
- GitHub Actions based CI/CD automation

---

## 🧰 Tech Stack Used

| Technology | Purpose |
|---|---|
| Docker | Containerization and application packaging |
| Dockerfile | Creating custom Docker images |
| Docker Volumes | Data persistence |
| Docker Network | Communication between containers |
| Docker Compose | Running multi-container applications |
| Apache | Web server container practice |
| NGINX | Custom web server image practice |
| MySQL | Database container practice |
| PostgreSQL | Database service in compose setup |
| Maven | Java build automation and dependency management |
| Maven Wrapper | Running Maven without local Maven installation |
| Jenkins | CI/CD automation server |
| GitHub Actions | Automated CI/CD workflows |
| GitHub | Version control and project hosting |

---

## 📅 15-Day DevOps Practice Journey

| Day | Task | What I Practiced |
|---|---|---|
| Day 01 | Apache Container Setup | Created Apache container, copied files using `docker cp`, and practiced `attach` vs `exec`. |
| Day 02 | Docker Named Volumes | Created named volumes and understood how container data persists. |
| Day 03 | Docker Questions + MySQL | Practiced Docker concepts and created a MySQL container. |
| Day 04 | Custom NGINX Image | Built a custom NGINX image using Dockerfile. |
| Day 05 | Docker Networking & Volumes | Practiced networking, volumes, and multi-container architecture. |
| Day 06 | Volume Persistence | Created volume, stored data, removed container, and verified data persistence. |
| Day 07 | Bridge Network | Created bridge network, connected containers, tested communication, and deleted resources. |
| Day 08 | Compose Multi-Container App | Built Frontend + Backend + PostgreSQL setup using Docker Compose. |
| Day 09 | Docker Compose Practice | Practiced compose commands like up, down, logs, ps, and build. |
| Day 10 | Maven Build with Compose | Used Docker Compose for Maven build in a containerized environment. |
| Day 11 | Maven + Docker | Built JAR with Maven, created Docker image, and ran Java app container. |
| Day 12 | Maven Wrapper | Practiced `mvnw` and Java JAR execution. |
| Day 13 | GitHub Actions + Docker | Automated Docker image build on code push. |
| Day 14 | Multi-Container CI/CD | Practiced CI/CD workflow using Docker Compose. |
| Day 15 | Java CI Pipeline | Created Java CI pipeline using Maven and GitHub Actions. |

---

## 🧠 Core Concepts Learned

### Docker
Docker is used to package applications with dependencies into lightweight containers.  
I practiced images, containers, volumes, networks, Dockerfile, and Docker Compose.

### Maven
Maven is a build automation and dependency management tool mainly used for Java projects.  
I practiced Maven lifecycle phases like `clean`, `compile`, `test`, `package`, and `install`.

### Jenkins
Jenkins is an automation server used for CI/CD pipelines.  
I learned Jenkins pipeline flow, Jenkinsfile basics, Maven integration, Docker integration, and webhook concepts.

### CI/CD
CI/CD helps automate build, test, package, and deployment processes.  
I practiced CI/CD using GitHub Actions and studied Jenkins pipeline workflow.

---

## 📂 Suggested Folder Structure

```text
devops-tasks/
│
├── day-01-apache-container/
│   ├── commands.txt
│   └── README.md
│
├── day-02-docker-volumes/
│   ├── commands.txt
│   └── README.md
│
├── day-03-mysql-container/
│   ├── commands.txt
│   └── README.md
│
├── day-04-nginx-dockerfile/
│   ├── Dockerfile
│   ├── index.html
│   └── README.md
│
├── day-08-docker-compose-app/
│   ├── docker-compose.yml
│   └── README.md
│
├── day-11-maven-docker/
│   ├── Dockerfile
│   ├── pom.xml
│   └── README.md
│
├── day-13-github-actions-docker/
│   └── .github/workflows/docker-build.yml
│
├── day-15-java-ci-maven/
│   └── .github/workflows/java-ci.yml
│
└── README.md
```

---

## 🐳 Docker Commands Practiced

```bash
docker --version
docker ps
docker ps -a
docker images
docker pull ubuntu
docker run -it ubuntu bash
docker run -dit --name mycontainer ubuntu
docker start <container_name>
docker stop <container_name>
docker rm <container_name>
docker rmi <image_name>
```

### Copy Files Between Host and Container

```bash
docker cp index.html <container_id>:/var/www/html/
docker cp <container_id>:/var/www/html/index.html .
```

### Enter Running Container

```bash
docker exec -it <container_id> bash
```

### Attach Container

```bash
docker attach <container_id>
```

> I learned that `docker exec` is safer for opening a new shell inside a running container, while `docker attach` connects to the main process.

---

## 📦 Docker Volume Practice

```bash
docker volume create myvolume
docker volume ls
docker run -dit --name vol-container -v myvolume:/data ubuntu
docker exec -it vol-container bash
```

Inside container:

```bash
cd /data
echo "Persistent Docker Data" > file.txt
exit
```

Remove and verify:

```bash
docker rm -f vol-container
docker run -dit --name new-container -v myvolume:/data ubuntu
docker exec -it new-container cat /data/file.txt
```

---

## 🌐 Docker Network Practice

```bash
docker network ls
docker network create mybridge
docker run -dit --name container1 --network mybridge ubuntu
docker run -dit --name container2 --network mybridge ubuntu
docker exec -it container1 bash
ping container2
docker network rm mybridge
```

---

## 🧱 Custom NGINX Dockerfile

```Dockerfile
FROM nginx:latest
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

Build and run:

```bash
docker build -t custom-nginx:v1 .
docker run -d -p 8080:80 --name nginx-container custom-nginx:v1
```

---

## 🗄️ MySQL Container Setup

```bash
docker run -d   --name mysql-container   -e MYSQL_ROOT_PASSWORD=root123   -e MYSQL_DATABASE=devopsdb   -e MYSQL_USER=devops   -e MYSQL_PASSWORD=devops123   mysql:latest
```

Login:

```bash
docker exec -it mysql-container bash
mysql -u root -p
```

---

## 🧩 Docker Compose Example

```yaml
services:
  frontend:
    image: nginx:latest
    ports:
      - "8080:80"

  backend:
    build: ./backend
    ports:
      - "5000:5000"

  database:
    image: postgres:latest
    environment:
      POSTGRES_USER: devops
      POSTGRES_PASSWORD: devops123
      POSTGRES_DB: devopsdb
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

Compose commands:

```bash
docker compose up -d
docker compose ps
docker compose logs
docker compose build
docker compose down
```

---

## ☕ Maven Build Automation

Maven helps in compiling, testing, packaging, and managing dependencies for Java projects.

### Maven Lifecycle

| Phase | Purpose |
|---|---|
| validate | Checks project correctness |
| compile | Compiles source code |
| test | Runs test cases |
| package | Creates JAR/WAR file |
| install | Stores package in local repository |
| deploy | Uploads package to remote repository |

### Maven Commands

```bash
mvn -version
mvn clean
mvn compile
mvn test
mvn package
mvn install
mvn clean package
mvn clean package -DskipTests
```

---

## 📦 Maven + Docker Integration

Build JAR:

```bash
mvn clean package
```

Dockerfile:

```Dockerfile
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY target/*.jar app.jar
EXPOSE 8080
CMD ["java", "-jar", "app.jar"]
```

Build and run:

```bash
docker build -t java-maven-app:v1 .
docker run -d -p 8080:8080 --name java-app java-maven-app:v1
```

---

## ▶️ Maven Wrapper Practice

Linux/macOS:

```bash
./mvnw clean package
./mvnw test
java -jar target/*.jar
```

Windows:

```bash
mvnw.cmd clean package
mvnw.cmd test
java -jar target/*.jar
```

---

## ⚙️ GitHub Actions: Java CI with Maven

```yaml
name: Java CI with Maven

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Set up JDK 17
        uses: actions/setup-java@v4
        with:
          java-version: '17'
          distribution: 'temurin'

      - name: Build with Maven
        run: mvn clean package

      - name: Run Tests
        run: mvn test
```

---

## 🐳 GitHub Actions: Docker Build CI

```yaml
name: Docker Build CI

on:
  push:
    branches:
      - main

jobs:
  docker-build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Build Docker Image
        run: docker build -t devops-app:latest .
```

---

## 🧱 Docker Compose CI Workflow

```yaml
name: Docker Compose CI

on:
  push:
    branches:
      - main

jobs:
  compose-build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Build Services
        run: docker compose build

      - name: Start Services
        run: docker compose up -d

      - name: Check Running Containers
        run: docker compose ps

      - name: Stop Services
        run: docker compose down
```

---

## 🧪 Jenkins CI/CD Pipeline Concept

Jenkins pipeline flow:

```text
Developer
   ↓
GitHub Repository
   ↓
Jenkins
   ↓
Maven Build
   ↓
Test
   ↓
Package JAR/WAR
   ↓
Deploy
```

### Basic Jenkins Pipeline

```groovy
pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/username/repository-name.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application'
            }
        }
    }
}
```

---

## 📌 Important Interview / Viva Points

- Docker image is a template; container is a running instance of an image.
- Docker volumes keep data safe even if the container is deleted.
- Docker networks allow containers to communicate with each other.
- Docker Compose manages multiple containers using a YAML file.
- Maven automates Java build, test, and packaging.
- `pom.xml` is the main Maven configuration file.
- Jenkins automates CI/CD pipelines.
- GitHub Actions can automatically run workflows on push or pull request.
- CI means Continuous Integration.
- CD means Continuous Delivery or Continuous Deployment.

---

## 🚀 How to Use This Repository

1. Clone the repository:

```bash
git clone https://github.com/<your-username>/<your-repo-name>.git
```

2. Go inside the repository:

```bash
cd <your-repo-name>
```

3. Open day-wise folders.

4. Read commands and practice tasks.

5. Run Docker, Maven, Jenkins, or GitHub Actions workflows as required.

---

## ✅ Final Outcome

After completing these practical tasks, I gained hands-on experience in:

- Running and managing containers
- Creating custom Docker images
- Managing persistent data using volumes
- Connecting containers using networks
- Running multi-container apps with Docker Compose
- Building Java projects with Maven
- Creating CI/CD workflows using GitHub Actions
- Understanding Jenkins CI/CD pipeline flow

This repository represents my practical DevOps learning journey and can be used for revision, interviews, viva preparation, and project demonstration.

---

## 👨‍💻 Author

**Utkarsh**

---

## 📌 Note

This repository is created for learning, revision, and hands-on DevOps practice.
