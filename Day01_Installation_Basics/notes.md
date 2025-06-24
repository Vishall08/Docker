## 📅 Day 01: Docker Installation, Concepts & Basic Commands

---

### 🧠 What I Learned

* ✅ Basics of compute paradigms:

  * **Bare Metal**: Physical servers without abstraction.
  * **Containerization**: Lightweight, OS-level virtualization using Docker.
  * **Virtualization**: Use of hypervisors to run multiple OS instances.
  * **Serverless**: Fully managed execution without server management.

* ✅ Installed Docker Engine on Ubuntu using `apt`.

* ✅ Started and verified Docker service status.

* ✅ Explored the Docker CLI: image handling, container lifecycle.

* ✅ Differentiated between foreground and detached mode.

---

### 🔧 Commands Practiced

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

# List Docker images
docker images
docker image ls
exit

# Re-enter root user to continue Docker commands
sudo su

# Search for nginx image on Docker Hub
docker search nginx

# Pull nginx image from Docker Hub
docker pull nginx

# Run nginx container in the foreground (blocks terminal)
docker run nginx

# Check running containers
docker ps

# Run nginx container in detached mode with a custom name
docker run -d --name mynginx nginx

# List all containers (including stopped ones)
docker ps -a
```
