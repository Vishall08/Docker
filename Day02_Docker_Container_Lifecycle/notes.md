## 📅 Day 02: Docker Container Lifecycle, Ports, Exec & Cleanup

---

### 🧠 What I Learned

✅ Inspected image history and understood image layers.

✅ Exposed container ports to host using -p flag.

✅ Used docker exec to interact inside running containers.

✅ Edited files inside containers using nano.

✅ Used curl to test internal server content.

✅ Stopped, started, and removed containers individually and in bulk.

✅ Learned docker container prune and force removal techniques.



### Commands Practiced (Day 2)
```
# Switch to root
sudo su

# List Docker images
docker image ls

# View image history
docker history <image-id-or-name>

# Run container with port mapping
docker run -d --name mycont -p 80:80 <image-id-or-name>
# Syntax: -p <host-port>:<container-port>

# Example: Run nginx with port mapping
docker run -d --name mycontainer -p 80:80 nginx

# Execute commands inside container
docker exec -it <container-id> ls
docker exec -it <container-id> ls /usr
docker exec -it <container-id> /bin/bash

# Navigate and edit inside container
cd /usr/share/nginx/html
apt update
apt install nano
nano home.html
curl localhost/home.html

# Stop a container
docker stop <container-id-or-name>
docker container stop <container-id-or-name>

# Stop multiple containers
docker stop <id1> <id2> <id3>
docker container stop <id1> <id2> <id3>

# Stop all running containers
docker stop $(docker ps -q)
docker container stop $(docker ps -q)

# Start all stopped containers
docker start $(docker ps -aq)
docker container start $(docker ps -aq)

# Remove a single container
docker rm <container-id>
docker container rm <container-id>

# Remove multiple containers
docker rm <id1> <id2>
docker container rm <id1> <id2>

# Remove all stopped containers
docker container prune

docker rm $(docker ps -aq)
docker rm -f $(docker ps -aq)
```
