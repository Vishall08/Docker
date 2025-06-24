# 📘 Day 14: Running WordPress Using Dockerfile + Docker Compose
---

## 🧩 Goal:
To deploy a WordPress website connected to a MySQL database, using:

A custom Dockerfile to build the MySQL image

docker-compose.yml to orchestrate the WordPress and MySQL services

### 🔧 1. Dockerfile (for MySQL container)
```
FROM mysql

ENV MYSQL_ROOT_PASSWORD Pass@123
ENV MYSQL_DATABASE mydb

EXPOSE 3306

CMD ["mysqld"]
```
### 🔍 Explanation:
FROM mysql: Uses the official MySQL image as a base.

ENV MYSQL_ROOT_PASSWORD Pass@123: Sets the root password for MySQL.

ENV MYSQL_DATABASE mydb: Creates a database named mydb at startup.

EXPOSE 3306: Opens MySQL’s default port (useful for documentation and linking).

CMD ["mysqld"]: Starts the MySQL server when the container runs.

✅ This custom Dockerfile lets you configure MySQL with your own settings.

### 📦 2. docker-compose.yml File
```
services:
  mydb:
    build:
      context: .
      dockerfile: Dockerfile

  mycont:
    image: wordpress
    environment:
      WORDPRESS_DB_HOST: mydb
      WORDPRESS_DB_USER: root
      WORDPRESS_DB_PASSWORD: Pass@123
      WORDPRESS_DB_NAME: mydb
    ports:
      - 80:80
    depends_on:
      - mydb
```

### 🔍 Explanation:
services: Defines multiple containers:

▶️ mydb (MySQL Service)
build: Builds the image using the custom Dockerfile in the current directory (context: .).

dockerfile: Dockerfile: Specifies the file to use for building.

▶️ mycont (WordPress Service)
image: wordpress: Uses the official WordPress image.

environment: Sets necessary variables for WordPress to connect to MySQL.

ports: - 80:80: Maps port 80 on the host to 80 in the container (for web access).

depends_on: Ensures the MySQL container (mydb) starts before WordPress.

🔗 WordPress will connect to MySQL using the service name mydb as the hostname (Docker handles networking between services).

### 💻 3. Docker Commands You Used
```
nano Dockerfile           # Edit or create the Dockerfile
nano docker-compose.yml   # Edit or create the docker-compose file

docker images             # View list of available Docker images
docker rmi mysql          # Remove existing MySQL image to force rebuild
docker ps -a              # List all containers (running or not)

docker-compose up -d      # Run all services in detached mode (in background)

docker image ls           # Alias of `docker images`
docker container ls       # Alias of `docker ps`
```

### 🔍 Purpose of Each Command:
docker rmi mysql: Ensures Docker rebuilds the image from Dockerfile instead of using a cached image.

docker-compose up -d: Builds and starts both services in background mode.

docker ps -a / docker container ls: Helps verify if containers are running properly.

docker images / docker image ls: Shows which images are available (including the one built from your Dockerfile).

### 🌐 Final Result
Once the containers are up:

Access your WordPress site via your browser at http://localhost (or your EC2/public IP if on cloud).

On first visit, WordPress will guide you through setting up the website using the database details provided.

| Concept                   | Description                                                      |
| ------------------------- | ---------------------------------------------------------------- |
| **Custom Dockerfile**     | To build a pre-configured MySQL image.                           |
| **Docker Compose**        | Manages multi-container apps like WordPress + MySQL.             |
| **Networking**            | Docker Compose enables inter-container communication by default. |
| **Environment Variables** | Used to pass configuration settings into containers.             |
| **Service Dependency**    | `depends_on` ensures DB starts before the app.                   |


### ✅ Real-World Use Case
This setup mimics how production-grade applications like CMSs (e.g., WordPress) rely on:

Multiple services

Orchestration (Compose, Kubernetes)

Custom configurations

It’s a foundation for deploying CMS platforms, LAMP stacks, or even microservices using containers.


