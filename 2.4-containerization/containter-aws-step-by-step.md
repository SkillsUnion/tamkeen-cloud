# **Step-by-Step Guide: Docker, Docker Hub, ECR, and ECS**

## **1. Install Docker**

### **1.1 Install Docker on Windows & Mac**
1. Download **Docker Desktop** from [Docker's official website](https://www.docker.com/get-started).
2. Run the installer and follow the installation instructions.
3. Start Docker Desktop and ensure it is running.
4. Verify installation:
   ```bash
   docker --version
   ```

### **1.2 Install Docker on Linux (Ubuntu/Debian)**
1. Update your system:
   ```bash
   sudo apt update
   ```
2. Install Docker:
   ```bash
   sudo apt install docker.io -y
   ```
3. Start and enable Docker service:
   ```bash
   sudo systemctl start docker
   sudo systemctl enable docker
   ```
4. Verify installation:
   ```bash
   docker --version
   ```
5. Add your user to the Docker group (optional, avoids using `sudo`):
   ```bash
   sudo usermod -aG docker $USER
   ```
   Logout and log back in to apply changes.

---

## **2. Working with Docker Containers**

### **2.1 Running a Simple Container**
```bash
docker run hello-world
```

### **2.2 List Running Containers**
```bash
docker ps
```

### **2.3 Stop and Remove a Container**
```bash
docker stop <container_id>
docker rm <container_id>
```

---

## **3. Using Docker Hub**

### **3.1 Login to Docker Hub**
```bash
docker login
```

### **3.2 Pull an Image from Docker Hub**
```bash
docker pull nginx
```

### **3.3 Tag and Push an Image to Docker Hub**
```bash
docker tag my-app username/my-app:latest
docker push username/my-app:latest
```

---

## **4. Amazon ECR (Elastic Container Registry)**

### **4.1 Prerequisites**
- AWS Account
- AWS CLI installed (`aws configure`)

### **4.2 Create an ECR Repository**
```bash
aws ecr create-repository --repository-name my-ecr-repo
```

### **4.3 Authenticate Docker with ECR**
```bash
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com
```

### **4.4 Tag and Push Image to ECR**
```bash
docker tag my-app <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/my-ecr-repo:latest
docker push <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/my-ecr-repo:latest
```

---

## **5. Amazon ECS (Elastic Container Service)**

### **5.1 Create an ECS Cluster**
```bash
aws ecs create-cluster --cluster-name my-cluster
```

### **5.2 Create a Task Definition**
Create a `task-definition.json` file:
```json
{
  "family": "my-app-task",
  "containerDefinitions": [
    {
      "name": "my-app",
      "image": "<aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/my-ecr-repo:latest",
      "memory": 512,
      "cpu": 256,
      "essential": true,
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80
        }
      ]
    }
  ]
}
```
Register the task definition:
```bash
aws ecs register-task-definition --cli-input-json file://task-definition.json
```

### **5.3 Create an ECS Service**
```bash
aws ecs create-service --cluster my-cluster --service-name my-service \
  --task-definition my-app-task --desired-count 2 --launch-type FARGATE \
  --network-configuration "awsvpcConfiguration={subnets=[subnet-abc123],securityGroups=[sg-xyz456],assignPublicIp=ENABLED}"
```

### **5.4 View Running Tasks**
```bash
aws ecs list-tasks --cluster my-cluster
```

---

## **6. Monitoring and Scaling ECS**

### **6.1 View ECS Logs**
```bash
aws logs get-log-events --log-group-name /ecs/my-service --log-stream-name my-container-id
```

### **6.2 Scale ECS Service**
```bash
aws ecs update-service --cluster my-cluster --service my-service --desired-count 4
```

### **6.3 Update ECS Service with New Image**
```bash
aws ecs update-service --cluster my-cluster --service my-service --task-definition my-app-task
```

---

## **7. Clean Up AWS Resources**

### **7.1 Delete ECS Service**
```bash
aws ecs delete-service --cluster my-cluster --service my-service --force
```

### **7.2 Delete ECS Cluster**
```bash
aws ecs delete-cluster --cluster my-cluster
```

### **7.3 Delete ECR Repository**
```bash
aws ecr delete-repository --repository-name my-ecr-repo --force
```

---