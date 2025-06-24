## 📅 Day 04: Advanced Image/Container Export, Save, Commit & Load

### 🧠 What I Learned

✅ Exported containers to .tar using both > and -o syntax.

✅ Saved Docker images to .tar files using docker save.

✅ Imported .tar files as images using docker import.

✅ Ran containers from imported images.

✅ Used docker commit to create an image from a container.

✅ Loaded images back using docker load.

✅ Practiced image and container cleanup.

### 🔧 Commands Practiced (Day 4)

```

# View running containers
docker container ls

# Export container to .tar file (two ways)
docker export <container-id> > myapp.tar
docker export <container-id> -o myapp.tar

# Save image to .tar file
docker save -o myapp1.tar myappimg1

# Run container from saved image
docker run -d -p 90:80 --name myapp myappimg1 /bin/bash

# Commit changes in container to new image
docker commit myapp appimg

# Save committed image to file
docker save -o myfile.tar appimg

# Remove unused image and container tar files
rm myapp1.tar myimg.tar nginx.tar
rm myapp.tar

# Import from tar to create image
docker import myapp.tar newapp

# Check image history
docker history newapp
docker history nginx

# Run container from imported image
docker run -d -it -p 8080:80 newapp bash

# Load image from .tar file
docker load -i myfile.tar

# Run container from loaded image
docker run -d -p 80:80 --name myapp appimg

# Clean up

# Stop all containers
docker container stop $(docker ps -aq)

# Prune stopped containers
docker container prune

# Remove all images
docker rmi $(docker images -q)
```

