# 📅 Day 05: Docker Hub & Amazon ECR (Elastic Container Registry)
---

## 🧠 What I Learned

✅ Created a Docker Hub account and public repository.

✅ Generated a personal access token with expiry for login.

✅ Tagged images and pushed them to Docker Hub.

✅ Logged in using token in CLI.

✅ Installed AWS CLI and configured credentials.

✅ Created a repository in ECR and prepared image for push.

## 🔧 Commands Practiced (Day 5)

```

# Docker Hub: Tag your image before pushing
docker tag appimg xyz/devops:v1.0

# Login to Docker Hub (username & token)
docker login -u xyz
# Password (token): asd;fjsfj

# Push image to Docker Hub
docker push xyz/devops:v1.0

# Remove image
docker rmi xyz/devops:v1.0

# Pull image back
docker pull xyz/devops:v1.0

docker image ls

```

## 🛠️ Create Docker Hub Token

Go to Docker Hub → Profile → Account Settings → Personal Access Token

Generate token with scope (read/write/delete), optional 30-day expiry

## 🔧 AWS ECR Steps

```
# Install AWS CLI
apt-get update
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
apt install unzip
unzip awscliv2.zip
./aws/install

# Verify installation
aws --version

# Configure AWS credentials
aws configure
# Enter: Access Key, Secret Key, Default Region, Output Format

# Tag Docker image for ECR
docker tag appimg <aws_account_id>.dkr.ecr.<region>.amazonaws.com/repo_name

# Login to ECR
eval $(aws ecr get-login-password --region <region> | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.<region>.amazonaws.com)

# Push to ECR
docker push <aws_account_id>.dkr.ecr.<region>.amazonaws.com/repo_name
```
