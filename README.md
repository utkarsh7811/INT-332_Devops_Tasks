DevOps Tasks – Docker, Maven, and CI/CD
This repository contains my 15-day DevOps practical learning journey.  
The main focus is on Docker containers, Docker volumes, Docker networking, Docker Compose, Maven build automation, and CI/CD using GitHub Actions.
---
📌 Repository Objective
The purpose of this repository is to document and practice important DevOps concepts through hands-on tasks.
By completing these tasks, I practiced:
Container creation and management
Apache and NGINX container setup
Docker volumes and persistent storage
Docker networking and bridge networks
Multi-container application setup
Docker Compose
Maven build automation
Maven Wrapper usage
Dockerizing Java applications
GitHub Actions CI/CD pipeline
Multi-container CI/CD workflow
---
🛠️ Tools and Technologies Used
Tool / Technology	Purpose
Docker	Containerization
Dockerfile	Custom image creation
Docker Volumes	Persistent storage
Docker Network	Container communication
Docker Compose	Multi-container application management
Apache HTTP Server	Web server container practice
NGINX	Custom web server image
MySQL	Database container practice
PostgreSQL	Database service in Docker Compose
Maven	Java build automation
Maven Wrapper	Running Maven without local Maven installation
GitHub Actions	CI/CD automation
GitHub	Version control and repository hosting
---
📅 15-Day DevOps Task Summary
Day	Topic Practiced	Description
Day 01	Apache Container Setup	Created Apache container, performed file manipulation, used `docker cp`, and practiced `docker attach` vs `docker exec`.
Day 02	Docker Named Volumes	Practiced named volumes and understood container data persistence.
Day 03	Docker Questions + MySQL	Practiced Docker questions and created a MySQL container setup.
Day 04	Custom NGINX Image	Built a custom NGINX Docker image using a Dockerfile.
Day 05	Networking, Volumes, Architecture	Practiced Docker networking, volumes, and multi-container architecture.
Day 06	Volume Persistence Practical	Created Docker volume, attached it to a container, stored data, removed container, and verified persistence.
Day 07	Bridge Network Practical	Created bridge network, connected containers, tested communication, and deleted network/containers.
Day 08	Docker Compose Multi-Container App	Created Frontend + Backend + PostgreSQL setup using Docker Compose.
Day 09	Docker Compose Practice	Practiced Docker Compose commands and service management.
Day 10	Maven Build with Docker Compose	Used Docker Compose for Maven build in a containerized build environment.
Day 11	Maven + Docker Integration	Built JAR using Maven, created Docker image, and ran Java app container.
Day 12	Maven Wrapper	Practiced `mvnw` and Java JAR execution.
Day 13	GitHub Actions with Docker	Created CI/CD workflow for automatic Docker image build on push.
Day 14	Multi-Container CI/CD	Practiced CI/CD workflow using Docker Compose.
Day 15	Java CI Pipeline	Created Java CI pipeline using Maven and GitHub Actions.
---
📂 Suggested Repository Structure
```text
devops-tasks/
│
├── day-01-apache-container/
│   ├── README.md
│   └── commands.txt
│
├── day-02-docker-volumes/
│   ├── README.md
│   └── commands.txt
│
├── day-03-mysql-container/
│   ├── README.md
│   └── commands.txt
│
├── day-04-nginx-dockerfile/
│   ├── Dockerfile
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
│   └── .github/
│       └── workflows/
│           └── docker-build.yml
│
├── day-15-java-ci-maven/
│   ├── pom.xml
│   └── .github/
│       └── workflows/
│           └── java-ci.yml
│
└── README.md
```
---
🐳 Important Docker Commands
Check Docker Version
```bash
docker --version
```
List Running Containers
```bash
docker ps
```
List All Containers
```bash
docker ps -a
```
List Docker Images
```bash
docker images
```
Pull Docker Image
```bash
docker pull ubuntu
```
Run Container
```bash
docker run -it ubuntu bash
```
Run Container in Detached Mode
```bash
docker run -dit --name mycontainer ubuntu
```
Stop Container
```bash
docker stop <container_name_or_id>
```
Start Container
```bash
docker start <container_name_or_id>
```
Remove Container
```bash
docker rm <container_name_or_id>
```
Remove Image
```bash
docker rmi <image_name>
```
---
📁 Docker File Copy Command
Copy File from Host to Container
```bash
docker cp index.html <container_id>:/var/www/html/
```
Copy File from Container to Host
```bash
docker cp <container_id>:/var/www/html/index.html .
```
---
🔗 docker attach vs docker exec
Command	Use
`docker attach`	Connects to the main running process of a container
`docker exec`	Runs a new command inside a running container
Example
```bash
docker attach <container_id>
```
```bash
docker exec -it <container_id> bash
```
> Best practice: Use `docker exec` for entering a running container because it does not disturb the main process.
---
📦 Docker Volumes
Docker volumes are used to store persistent data.
Create Volume
```bash
docker volume create myvolume
```
List Volumes
```bash
docker volume ls
```
Run Container with Volume
```bash
docker run -dit --name vol-container -v myvolume:/data ubuntu
```
Verify Data Persistence
```bash
docker exec -it vol-container bash
cd /data
echo "Hello Docker Volume" > file.txt
exit

docker rm -f vol-container

docker run -dit --name new-container -v myvolume:/data ubuntu
docker exec -it new-container cat /data/file.txt
```
---
🌐 Docker Networking
List Networks
```bash
docker network ls
```
Create Bridge Network
```bash
docker network create mybridge
```
Run Containers in Same Network
```bash
docker run -dit --name container1 --network mybridge ubuntu
docker run -dit --name container2 --network mybridge ubuntu
```
Test Container Connectivity
```bash
docker exec -it container1 bash
ping container2
```
Remove Network
```bash
docker network rm mybridge
```
---
🧱 Dockerfile Example for NGINX
```Dockerfile
FROM nginx:latest
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```
Build Image
```bash
docker build -t custom-nginx:v1 .
```
Run Container
```bash
docker run -d -p 8080:80 --name nginx-container custom-nginx:v1
```
Open in browser:
```text
http://localhost:8080
```
---
🗄️ MySQL Container Setup
```bash
docker run -d   --name mysql-container   -e MYSQL_ROOT_PASSWORD=root123   -e MYSQL_DATABASE=devopsdb   -e MYSQL_USER=devops   -e MYSQL_PASSWORD=devops123   mysql:latest
```
Enter MySQL Container
```bash
docker exec -it mysql-container bash
```
Login to MySQL
```bash
mysql -u root -p
```
---
🧩 Docker Compose
Docker Compose is used to manage multi-container applications using a `docker-compose.yml` file.
Basic Docker Compose Commands
```bash
docker compose up
docker compose up -d
docker compose down
docker compose ps
docker compose logs
docker compose build
```
---
🧪 Example Docker Compose File
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
---
☕ Maven Build Automation
Maven is used to build and manage Java projects.
Common Maven Commands
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
Maven Build Lifecycle
Phase	Purpose
validate	Checks project correctness
compile	Compiles source code
test	Runs test cases
package	Creates JAR/WAR file
install	Installs package in local repository
deploy	Deploys package to remote repository
---
📦 Maven + Docker Integration
Build JAR File
```bash
mvn clean package
```
Dockerfile for Java JAR
```Dockerfile
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY target/*.jar app.jar
EXPOSE 8080
CMD ["java", "-jar", "app.jar"]
```
Build Docker Image
```bash
docker build -t java-maven-app:v1 .
```
Run Docker Container
```bash
docker run -d -p 8080:8080 --name java-app java-maven-app:v1
```
---
▶️ Maven Wrapper
Maven Wrapper allows running Maven without installing Maven manually.
Commands
```bash
./mvnw clean package
./mvnw test
java -jar target/*.jar
```
For Windows:
```bash
mvnw.cmd clean package
mvnw.cmd test
java -jar target/*.jar
```
---
⚙️ GitHub Actions CI/CD with Docker
Create this file:
```text
.github/workflows/docker-build.yml
```
Docker Build Workflow
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
☕ Java CI Pipeline with Maven
Create this file:
```text
.github/workflows/java-ci.yml
```
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
🧱 Multi-Container CI/CD using Docker Compose
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
📘 Key Concepts Learned
Difference between Docker image and container
Difference between `docker attach` and `docker exec`
Container file copying using `docker cp`
Docker volume persistence
Docker bridge networking
Multi-container application architecture
Docker Compose service management
Writing Dockerfiles
Building custom Docker images
Running database containers
Maven build lifecycle
Maven Wrapper usage
Dockerizing Java applications
CI/CD workflow using GitHub Actions
---
🧠 Common Viva Questions
What is Docker?
Docker is a containerization platform used to package and run applications with all required dependencies.
What is a Docker image?
A Docker image is a read-only template used to create containers.
What is a Docker container?
A container is a running instance of a Docker image.
What is Docker Compose?
Docker Compose is a tool used to define and manage multi-container applications using a YAML file.
What is Docker volume?
A Docker volume is used to store persistent data outside the container lifecycle.
What is Maven?
Maven is a build automation and dependency management tool mainly used for Java projects.
What is CI/CD?
CI/CD means Continuous Integration and Continuous Delivery or Continuous Deployment.
What is GitHub Actions?
GitHub Actions is a CI/CD platform provided by GitHub to automate build, test, and deployment workflows.
---
🚀 How to Use This Repository
Clone the repository:
```bash
git clone https://github.com/<your-username>/<your-repo-name>.git
```
Go inside the repository:
```bash
cd <your-repo-name>
```
Open any day-wise folder.
Follow the commands and README files.
Run Docker or Maven commands as per the task.
---
✅ Final Outcome
After completing these 15 days of DevOps practice, I gained hands-on experience with Docker, Docker Compose, Maven, and GitHub Actions CI/CD pipelines.
This repository represents my practical DevOps learning journey and can be used for revision, interviews, viva preparation, and project demonstration.
---
🙋 Author
Utkarsh
---
📌 Note
This repository is created for DevOps learning and hands-on practice.
