# **Advanced Docker Concepts**

### **1. Dockerfiles**

#### **1.1 Understanding Dockerfile Instructions**
A **Dockerfile** is a script that contains instructions for building a Docker image. Understanding each instruction is essential for creating optimized and secure images.

##### **Key Instructions:**

- `FROM` – Specifies the base image.
- `WORKDIR` – Sets the working directory inside the container.
- `COPY` / `ADD` – Copies files from the local system to the image.
- `RUN` – Executes commands during the image build process.
- `EXPOSE` – Declares ports the container will listen on.
- `CMD` – Specifies the default command executed when the container runs.
- `ENTRYPOINT` – Defines a fixed command for the container.
- `ENV` – Sets environment variables.
- `ARG` – Defines variables that can be passed at build-time.

##### **Optimizing Dockerfiles**

- Use **multi-stage builds** to reduce image size.
- Leverage **layer caching** by ordering instructions strategically.
- Minimize the number of layers to enhance performance.
- Use `.dockerignore` to exclude unnecessary files from the build context.
- Prefer official, lightweight base images (e.g., `alpine`, `debian-slim`).

##### **Example of an Optimized Dockerfile**

```dockerfile
# Multi-stage build example
FROM node:16-alpine AS builder
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=builder /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

---

### **2. Docker Networking**

#### **2.1 Understanding Docker Networking**
Docker provides various networking options to allow communication between containers and external systems.

##### **Types of Docker Networks:**

- **Bridge (default)** – Containers can communicate on the same host but are isolated from external networks.
- **Host** – The container shares the host network.
- **None** – The container runs without networking.
- **Overlay** – Enables multi-host networking (used in Docker Swarm).
- **Macvlan** – Assigns a MAC address to containers, making them appear as physical devices.

##### **Creating and Managing Networks**

**Creating a Custom Network:**

```bash
docker network create my-network
```

**Running Containers on a Custom Network:**

```bash
docker run -d --name container1 --network my-network nginx
```

**Inspecting a Network:**

```bash
docker network inspect my-network
```

**Removing a Network:**

```bash
docker network rm my-network
```

---

### **3. Docker Volumes and Storage**

#### **3.1 Introduction to Volumes**

Docker volumes provide persistent storage for containers.

##### **Types of Storage:**

- **Volumes** – Managed by Docker (`docker volume create`).
- **Bind Mounts** – Maps a host directory to the container.
- **Tmpfs Mounts** – Stored in memory for temporary data.

##### **Creating and Using Volumes**

**Creating a Volume:**

```bash
docker volume create my-volume
```

**Using a Volume in a Container:**

```bash
docker run -d -v my-volume:/data --name my-container nginx
```

**Inspecting Volumes:**

```bash
docker volume inspect my-volume
```

**Removing a Volume:**

```bash
docker volume rm my-volume
```

---

### **4. Docker Compose**

#### **4.1 What is Docker Compose?**

Docker Compose is a tool for defining and managing multi-container applications. It simplifies application deployment by allowing multiple services to be defined in a single YAML configuration file.

#### **4.2 Key Features of Docker Compose**

- **Service definition** – Define multiple services in a `docker-compose.yml` file.
- **Volume management** – Share persistent data between services.
- **Networking** – Automatically create a network for defined services.
- **Scaling** – Scale services up or down easily.
- **Environment variable management** – Define environment variables in `.env` files.

#### **4.3 Writing a `docker-compose.yml` File**

Example:

```yaml
version: "3.8"
services:
  web:
    image: nginx
    ports:
      - "8080:80"
    volumes:
      - web-data:/usr/share/nginx/html
    depends_on:
      - db
  db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: example
volumes:
  web-data:
```

#### **4.4 Running and Managing Multi-Container Applications**

**Starting Services:**

```bash
docker-compose up -d
```

**Viewing Logs:**

```bash
docker-compose logs -f
```

**Stopping Services:**

```bash
docker-compose down
```

**Scaling Services:**

```bash
docker-compose up --scale web=3 -d
```

**Restarting Services:**

```bash
docker-compose restart
```

**Checking Service Status:**

```bash
docker-compose ps
```

**Using Environment Variables in Compose:**

Create a `.env` file:
```env
MYSQL_ROOT_PASSWORD=securepassword
```
Modify `docker-compose.yml`:
```yaml
environment:
  MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
```

---

### **5. Docker Security Best Practices**

#### **5.1 Common Security Risks**

- Running containers as root.
- Using outdated, vulnerable images.
- Exposing unnecessary ports.
- Weak access control policies.

#### **5.2 Security Best Practices**

- Use **least privilege** by avoiding root access.
- Scan images with tools like `docker scan` or `Trivy`.
- Restrict container capabilities using `--cap-drop`.
- Enable user namespaces for process isolation.
- Use Docker Content Trust (DCT) for verified images.

---

