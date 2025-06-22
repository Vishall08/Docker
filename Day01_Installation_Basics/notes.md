# 📅 Day 01: Docker Installation and Basic Commands

## 🧠 What I Learned

- Installed Docker on an Ubuntu system using `apt`.
- Understood how to start and check the Docker service.
- Verified Docker installation using the `hello-world` and `nginx` images.
- Learned the difference between foreground and detached container modes.
- Explored basic Docker CLI commands.

## 🔧 Commands Practiced

```bash
# Update package repository
sudo apt-get update

# Install Docker Engine
sudo apt-get install docker.io -y

# Start Docker service and check its status
sudo service docker start
sudo systemctl status docker.service

# Switch to root user
sudo su

# View Docker images
docker images
docker image ls

# Search for an image on Docker Hub
docker search nginx

# Pull an image from Docker Hub
docker pull nginx

# Run a container in the foreground (shows output directly)
docker run nginx

# Check running containers
docker ps

# Run a container in detached mode with a name
docker run -d --name mynginx nginx

# List running containers again
docker ps
