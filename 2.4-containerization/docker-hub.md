# **Docker Hub**

## **1. What is Docker Hub?**
Docker Hub is a cloud-based registry service provided by Docker for storing, managing, and sharing container images. It allows developers to publish and distribute containerized applications easily.

### **Key Features of Docker Hub**
- **Public and Private Repositories** – Store container images either publicly or privately.
- **Automated Builds** – Automatically build images from a linked GitHub or Bitbucket repository.
- **Webhooks** – Trigger actions when an image is updated.
- **Official Images** – Verified images maintained by Docker and other vendors.
- **Teams and Organizations** – Manage user permissions for repositories.
- **Content Trust** – Verify the authenticity of images before pulling.

---

## **2. Creating a Docker Hub Account**
1. Go to [Docker Hub](https://hub.docker.com/).
2. Click **Sign Up** and create an account.
3. Verify your email and log in.

---

## **3. Logging Into Docker Hub from CLI**
To push or pull images, log in to Docker Hub using the command line:
```bash
docker login
```
Enter your **Docker ID** and **password** when prompted.

To log out:
```bash
docker logout
```

---

## **4. Working with Docker Images on Docker Hub**

### **4.1 Searching for Images**
To find an image on Docker Hub:
```bash
docker search nginx
```

### **4.2 Pulling an Image from Docker Hub**
To download an image from Docker Hub:
```bash
docker pull nginx
```
This pulls the latest `nginx` image. To pull a specific version:
```bash
docker pull nginx:1.21.6
```

### **4.3 Listing Downloaded Images**
```bash
docker images
```

### **4.4 Running an Image**
```bash
docker run -d -p 8080:80 nginx
```

---

## **5. Pushing Images to Docker Hub**

### **5.1 Creating a Repository**
1. Go to Docker Hub and log in.
2. Click **Repositories** > **Create Repository**.
3. Enter a **repository name** and choose **public** or **private** visibility.
4. Click **Create**.

### **5.2 Tagging an Image**
Before pushing an image, tag it with your Docker Hub username and repository name:
```bash
docker tag my-image username/my-repo:latest
```

### **5.3 Pushing an Image**
To push the image to Docker Hub:
```bash
docker push username/my-repo:latest
```

### **5.4 Viewing Pushed Images**
Navigate to Docker Hub and check the repository to see the uploaded image.

---

## **6. Managing Repositories**

### **6.1 Making a Repository Private or Public**
1. Go to the repository settings on Docker Hub.
2. Toggle the **Public/Private** switch.

### **6.2 Deleting a Repository**
1. Navigate to your repository.
2. Click **Settings** > **Delete Repository**.
3. Confirm deletion.

---

## **7. Automating Builds from GitHub/Bitbucket**

### **7.1 Linking a Repository**
1. Go to Docker Hub.
2. Click **Repositories** > **Create Repository**.
3. Select **Link to GitHub/Bitbucket**.
4. Authorize Docker Hub to access your repository.
5. Configure build settings and click **Create**.

### **7.2 Triggering an Automated Build**
Push a change to the linked GitHub/Bitbucket repository. Docker Hub will automatically build and update the image.

---

## **8. Using Webhooks in Docker Hub**
Webhooks notify external services when an image is updated.

### **8.1 Adding a Webhook**
1. Go to your repository.
2. Click **Settings** > **Webhooks**.
3. Enter the **Webhook URL**.
4. Click **Add Webhook**.

---

## **9. Docker Official Images and Verified Publishers**

### **9.1 What Are Official Images?**
Official images are maintained by Docker and provide a secure, verified source of commonly used applications (e.g., `nginx`, `mysql`).

### **9.2 Finding Official Images**
Search for images labeled **Official Image** on Docker Hub.

### **9.3 Using Verified Publisher Images**
Verified Publisher images come from trusted vendors and ensure security and compliance.

---

## **10. Enabling Docker Content Trust**
Docker Content Trust (DCT) ensures only signed images are pulled.

### **10.1 Enabling DCT**
```bash
export DOCKER_CONTENT_TRUST=1
```

### **10.2 Pulling Signed Images**
```bash
docker pull my-secure-image
```
If the image isn’t signed, it won’t be pulled.

---

## **11. Docker Hub Rate Limits**
Free-tier users have rate limits on image pulls.

### **11.1 Checking Your Rate Limit**
```bash
docker system info | grep "Rate Limit"
```

### **11.2 Avoiding Rate Limits**
- Authenticate with Docker Hub (`docker login`).
- Use a **paid Docker Hub subscription** for higher limits.
- Cache images in a local registry to reduce Hub pulls.

---

## **12. Deleting and Managing Docker Hub Images**

### **12.1 Deleting an Image from Docker Hub**
1. Navigate to the repository.
2. Select the image tag to delete.
3. Click **Delete Tag**.

### **12.2 Retagging an Image**
To rename an existing image tag:
```bash
docker tag old-image username/new-repo:new-tag
```

Push the newly tagged image:
```bash
docker push username/new-repo:new-tag
```

---

---

## **Summary**
Docker Hub is an essential tool for storing, managing, and distributing container images. This covered:
- Creating an account and logging in.
- Pulling, pushing, and managing images.
- Setting up automated builds and webhooks.
- Using official and verified images securely.
- Avoiding rate limits and optimizing performance.

