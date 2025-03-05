# **Working with Docker Images and Containers**

---

## **1. Understanding Docker Images and Containers**

### **1.1 What is a Docker Image?**
A **Docker image** is a read-only template that contains the application code, dependencies, and runtime environment. Images serve as the blueprint for creating containers.

{% include youtube.html id="_dfLOzuIg2o" %}

### **1.2 What is a Docker Container?**
A **Docker container** is a running instance of a Docker image. Containers are lightweight and portable, allowing applications to run in isolated environments.

### **1.3 Key Differences Between Images and Containers**
| Feature | Docker Image | Docker Container |
|---------|-------------|------------------|
| **State** | Static, read-only | Dynamic, running instance |
| **Purpose** | Blueprint for containers | Executing applications |
| **Persistence** | Cannot change at runtime | Can be modified but changes disappear on restart |

---

{% include youtube.html id="gAkwW2tuIqE" %}

## **2. Managing Docker Containers**

### **2.1 Running a Container**
To create and run a container from an image:
```bash
docker run -d --name my-container nginx
```
- `-d`: Runs the container in detached mode (in the background).
- `--name my-container`: Assigns a custom name to the container.
- `nginx`: The image used to create the container.

### **2.2 Listing Running Containers**
```bash
docker ps
```
This command shows all active containers.

To see all containers, including stopped ones:
```bash
docker ps -a
```

### **2.3 Stopping and Removing Containers**
```bash
docker stop my-container
```
```bash
docker rm my-container
```

### **2.4 Viewing Container Logs**
```bash
docker logs my-container
```

### **2.5 Accessing a Running Container**
To open an interactive shell inside a container:
```bash
docker exec -it my-container /bin/sh
```

---

## **3. Building Custom Docker Images**

### **3.1 Writing a Dockerfile**
A **Dockerfile** is a script containing instructions to create a custom image. Example:
```dockerfile
# Use a base image
FROM node:16-alpine

# Set working directory
WORKDIR /app

# Copy application files
COPY . .

# Install dependencies
RUN npm install

# Expose application port
EXPOSE 3000

# Command to run application
CMD ["node", "app.js"]
```

### **3.2 Building a Docker Image**
To create an image from a Dockerfile:
```bash
docker build -t my-node-app .
```
- `-t my-node-app`: Assigns a name to the image.
- `.`: Specifies the build context (current directory).

### **3.3 Listing Docker Images**
```bash
docker images
```

### **3.4 Removing an Image**
```bash
docker rmi my-node-app
```

---

## **4. Using Docker Volumes for Data Persistence**

### **4.1 What Are Docker Volumes?**
By default, data inside containers is lost when they are removed. **Volumes** provide persistent storage for containers.

### **4.2 Creating a Volume**
```bash
docker volume create my-volume
```

### **4.3 Using a Volume in a Container**
```bash
docker run -d -v my-volume:/data --name my-container nginx
```
- `-v my-volume:/data`: Mounts the volume to `/data` inside the container.

### **4.4 Listing Volumes**
```bash
docker volume ls
```

### **4.5 Removing a Volume**
```bash
docker volume rm my-volume
```

---

## **5. Networking in Docker**

### **5.1 Default Docker Networks**
Docker provides the following built-in networks:
- **bridge** (default): Containers can communicate on the same host.
- **host**: Containers share the host's network stack.
- **none**: Containers have no network connectivity.

### **5.2 Creating a Custom Network**
```bash
docker network create my-network
```

### **5.3 Connecting Containers to a Network**
```bash
docker run -d --name container1 --network my-network nginx
```
```bash
docker run -d --name container2 --network my-network alpine sleep 1000
```

### **5.4 Inspecting a Network**
```bash
docker network inspect my-network
```

### **5.5 Removing a Network**
```bash
docker network rm my-network
```

---

## **6. Summary**
- Docker images are blueprints for creating containers.
- Containers are running instances of images that execute applications.
- `docker run`, `docker ps`, `docker stop`, and `docker rm` are essential container management commands.
- Dockerfiles enable building custom images with application dependencies.
- Volumes ensure persistent data storage across container restarts.
- Docker networking allows containers to communicate securely within isolated environments.

---