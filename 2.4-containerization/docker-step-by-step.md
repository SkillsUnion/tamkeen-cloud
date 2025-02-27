# **Step-by-Step Docker**

## **1. Install Docker**

### **1.1 Install Docker on Windows & Mac**
1. Download **Docker Desktop** from [Docker's official website](https://www.docker.com/get-started).
2. Run the installer and follow the installation instructions.
3. After installation, open Docker Desktop and ensure it is running.
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

## **2. Run Your First Container**

### **2.1 Pull and Run a Container**
```bash
docker run hello-world
```
- This command downloads and runs a simple container that prints a message.

### **2.2 List Running Containers**
```bash
docker ps
```
- Shows currently running containers.

### **2.3 List All Containers (Including Stopped Ones)**
```bash
docker ps -a
```

### **2.4 Stop a Running Container**
```bash
docker stop <container_id>
```

### **2.5 Remove a Container**
```bash
docker rm <container_id>
```

---

## **3. Working with Docker Images**

### **3.1 Search for an Image**
```bash
docker search nginx
```

### **3.2 Pull an Image from Docker Hub**
```bash
docker pull nginx
```

### **3.3 List Downloaded Images**
```bash
docker images
```

### **3.4 Remove an Image**
```bash
docker rmi nginx
```

---

## **4. Build a Custom Docker Image**

### **4.1 Create a Simple Web Server Dockerfile**
Create a new directory and `Dockerfile`:
```bash
mkdir myapp && cd myapp
nano Dockerfile
```
Add the following content:
```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

### **4.2 Create an `index.html` File**
```bash
echo "<h1>Welcome to My Dockerized Web App</h1>" > index.html
```

### **4.3 Build the Docker Image**
```bash
docker build -t my-nginx-app .
```

### **4.4 Run the Custom Image**
```bash
docker run -d -p 8080:80 my-nginx-app
```

### **4.5 Access the Web Application**
Open `http://localhost:8080` in a web browser.

---

## **5. Docker Volumes (Persistent Storage)**

### **5.1 Create a Docker Volume**
```bash
docker volume create my-volume
```

### **5.2 Use the Volume in a Container**
```bash
docker run -d -v my-volume:/data --name my-container nginx
```

### **5.3 List Docker Volumes**
```bash
docker volume ls
```

### **5.4 Inspect a Volume**
```bash
docker volume inspect my-volume
```

### **5.5 Remove a Volume**
```bash
docker volume rm my-volume
```

---

## **6. Networking in Docker**

### **6.1 List Available Networks**
```bash
docker network ls
```

### **6.2 Create a Custom Network**
```bash
docker network create my-network
```

### **6.3 Connect a Container to a Network**
```bash
docker run -d --name container1 --network my-network nginx
```

### **6.4 Inspect a Network**
```bash
docker network inspect my-network
```

### **6.5 Remove a Network**
```bash
docker network rm my-network
```

---

## **7. Docker Compose (Multi-Container Applications)**

### **7.1 Create a `docker-compose.yml` File**
```yaml
version: "3.8"
services:
  web:
    image: nginx
    ports:
      - "8080:80"
  db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: example
```

### **7.2 Start Services**
```bash
docker-compose up -d
```

### **7.3 View Running Services**
```bash
docker-compose ps
```

### **7.4 Stop and Remove Services**
```bash
docker-compose down
```

---

## **8. Docker Security Best Practices**

### **8.1 Avoid Running Containers as Root**
```dockerfile
USER nginx
```

### **8.2 Scan Images for Vulnerabilities**
```bash
docker scan my-nginx-app
```

### **8.3 Restrict Container Capabilities**
```bash
docker run --cap-drop=ALL --security-opt no-new-privileges my-nginx-app
```

---

## **9. Clean Up Docker Resources**

### **9.1 Remove Unused Containers**
```bash
docker container prune
```

### **9.2 Remove Unused Images**
```bash
docker image prune
```

### **9.3 Remove Unused Volumes**
```bash
docker volume prune
```

### **9.4 Remove All Unused Resources**
```bash
docker system prune -a
```

