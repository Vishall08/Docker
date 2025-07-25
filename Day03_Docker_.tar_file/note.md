## 📅 Day 03: Docker Container Backup & Restore with .tar
---

### 🧠 What I Learned

✅ Stopped individual and all containers.

✅ Created .tar backups of containers using docker export.

✅ Imported .tar files as Docker images using docker import.

✅ Used imported images to run new containers.

✅ Understood difference between container export and pushing to registries (Docker Hub, ECR).

### 🔧 Commands Practiced (Day 3)

```

# Stop a single container
docker container stop <container-id>

# Stop all containers
docker container stop $(docker ps -q)

# View all containers
docker ps -a

# Start a specific container
docker container start myapp1

# Remove all stopped containers
docker container prune

# Export a container to .tar file
docker export <container-id> > filename.tar

# Create image from .tar file
docker import filename.tar imagename

# Use the new image to create a container
docker run -d -p 80:80 --name tartcont imagename

# Another example with ubuntu
docker run -d ubuntu

# Example: export, import, and run custom container
docker export <container-id> > myapp.tar
docker import myapp.tar myappimg
docker run -d -p 90:80 --name myapp myappimg

```

### 🗂️ Concepts Mentioned

.tar file creation and import

Docker Hub

Amazon ECR (Elastic Container Registry)
