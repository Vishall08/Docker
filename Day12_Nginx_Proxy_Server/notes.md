# 📅 Day 12: MySQL Init Script & Nginx as a Reverse Proxy

---

## 🧠 What I Learned

- Automating MySQL database and table creation using a shell script inside a container.
- Building a custom MySQL Docker image with environment variables using Dockerfile.
- Running multiple Nginx containers.
- Setting up Nginx as a reverse proxy server to balance traffic between containers.
- Editing configuration files inside Docker containers.
- Using a custom Docker bridge network to enable communication between containers.

---

## 🔧 Commands Practiced

### ✅ Part 1: MySQL Initialization with Script

#### 1️⃣ Create a shell script (`myfile.sh`) to initialize MySQL:

```bash
#!/bin/bash
mysql -u root -pPass@123 << EOF
create database insta;
use insta;
create table user(id int, name varchar(100));
insert into user values(101, "Fortune"), (102, "Cloud");
EOF
```
2️⃣ Create mysqlDockerfile:
```FROM mysql
MAINTAINER swati
LABEL version="1.0"
ENV MYSQL_ROOT_PASSWORD Pass@123
ENV MYSQL_DATABASE wordpressdb
EXPOSE 3306
CMD ["mysqld"]
```
3️⃣ Build and Run:
```
docker build -f mysqlDockerfile -t mydbimg .
docker run -d -p 3306 --name mydb mydbimg
docker exec -it mydb /bin/bash
mysql -u root -p
# Enter Password: Pass@123
```
✅ Part 2: Nginx as a Reverse Proxy Server
1️⃣ Run Backend Containers:
```
docker run -d --name cont1 nginx
docker run -d --name cont2 nginx
```
2️⃣ Modify index.html in cont1:
```
docker exec -it cont1 /bin/bash
cd /usr/share/nginx/html
rm index.html
echo "<h1>Hello from container 1</h1>" > index.html
exit
```
3️⃣ Modify index.html in cont2:
```
docker exec -it cont2 /bin/bash
cd /usr/share/nginx/html
rm index.html
echo "<h1>Hello from container 2</h1>" > index.html
exit
```
4️⃣ Start Proxy Container:
```
docker run -d --name proxy-server -p 80:80 nginx
```
5️⃣ Enter Proxy Container & Install nano:
```
docker exec -it proxy-server /bin/bash
apt update
apt install nano
```
6️⃣ Edit /etc/nginx/nginx.conf:
Add this under the http block:

```
http {
    upstream webserver {
        server cont1:80;
        server cont2:80;
    }
    ...
}
```
7️⃣ Edit /etc/nginx/conf.d/default.conf:
```
location / {
    proxy_pass http://webserver;
}
```
8️⃣ Reload Nginx:
```
service nginx reload
exit
```
9️⃣ Create Docker Network & Connect Containers:
```
docker network create mynetwork
docker network connect mynetwork cont1
docker network connect mynetwork cont2
docker network connect mynetwork proxy-server
```
🐛 Issues Faced
❌ Containers couldn't communicate → ✅ Fixed by connecting them to the same Docker network.

❌ Changes in nginx.conf didn’t apply → ✅ Fixed by running service nginx reload.

❌ Proxy returned 502 Bad Gateway → ✅ Fixed by ensuring correct container names and network links.

💡 Tips & Notes
Always use docker network to link containers that need to communicate.

Use upstream blocks in Nginx to implement simple round-robin load balancing.

Always reload Nginx after updating configuration.

Shell scripts (.sh) are a great way to initialize databases in Docker containers.

📚 Resources
📘 Docker MySQL Initialization

📘 Docker Networking Docs

📘 Nginx Reverse Proxy Setup
