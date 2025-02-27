# **Amazon Elastic Container Registry (ECR)**

## **1. Overview of Amazon ECR**
Amazon Elastic Container Registry (ECR) is a fully managed Docker container registry that allows developers to store, manage, and deploy container images securely. It integrates seamlessly with Amazon Elastic Container Service (ECS), Amazon Elastic Kubernetes Service (EKS), and AWS Lambda.

### **Key Features of ECR**
- **Fully Managed** – No need to manage underlying infrastructure.
- **Private and Public Repositories** – Store container images securely with IAM-based access control.
- **Image Scanning** – Automatically scan images for security vulnerabilities.
- **Lifecycle Policies** – Automate image retention and cleanup.
- **High Availability** – Highly scalable and available across AWS regions.
- **Encryption & Security** – Supports AWS IAM, KMS encryption, and private networking with VPC endpoints.

---

## **2. Setting Up Amazon ECR**

### **2.1 Prerequisites**
- AWS Account
- AWS CLI installed and configured (`aws configure`)
- Docker installed

### **2.2 Creating an ECR Repository**
#### **Using AWS Console:**
1. Navigate to the **Amazon ECR** service in the AWS Management Console.
2. Click **Create Repository**.
3. Choose **Visibility Settings**:
   - **Private** (default, restricts access to IAM roles/users)
   - **Public** (publicly accessible repository)
4. Configure settings:
   - Add **Repository Name**
   - Enable **Tag Immutable** (optional)
   - Enable **Scan on Push** (recommended for security)
5. Click **Create Repository**.

#### **Using AWS CLI:**
```bash
aws ecr create-repository --repository-name my-ecr-repo
```

---

## **3. Authenticating Docker with ECR**
Amazon ECR requires authentication to push and pull images. Use the AWS CLI to obtain a temporary authentication token:

```bash
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com
```

Replace `<aws_account_id>` with your AWS account ID.

---

## **4. Pushing Docker Images to ECR**

### **4.1 Tagging an Image for ECR**
Once authenticated, tag the local Docker image with the ECR repository URL:
```bash
docker tag my-app:latest <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/my-ecr-repo:latest
```

### **4.2 Pushing the Image to ECR**
```bash
docker push <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/my-ecr-repo:latest
```

### **4.3 Verifying the Image in ECR**
Check if the image is successfully pushed:
```bash
aws ecr describe-images --repository-name my-ecr-repo
```

---

## **5. Pulling Docker Images from ECR**
To pull an image from ECR, first authenticate and then run:
```bash
docker pull <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/my-ecr-repo:latest
```

---

## **6. Managing Amazon ECR Repositories**

### **6.1 Listing ECR Repositories**
```bash
aws ecr describe-repositories
```

### **6.2 Deleting an ECR Repository**
To delete a repository and all its images:
```bash
aws ecr delete-repository --repository-name my-ecr-repo --force
```

---

## **7. Enabling Image Scanning in ECR**
ECR supports automated image scanning for vulnerabilities using Amazon Inspector.

### **7.1 Enabling Scan on Push**
```bash
aws ecr put-image-scanning-configuration --repository-name my-ecr-repo --image-scanning-configuration scanOnPush=true
```

### **7.2 Running Manual Image Scans**
```bash
aws ecr start-image-scan --repository-name my-ecr-repo --image-id imageTag=latest
```

### **7.3 Viewing Scan Results**
```bash
aws ecr describe-image-scan-findings --repository-name my-ecr-repo --image-id imageTag=latest
```

---

## **8. Using Lifecycle Policies in ECR**
Lifecycle policies help automatically delete old or untagged images to reduce storage costs.

### **8.1 Creating a Lifecycle Policy**
Create a JSON file `lifecycle-policy.json`:
```json
{
  "rules": [
    {
      "rulePriority": 1,
      "description": "Delete images older than 30 days",
      "selection": {
        "tagStatus": "untagged",
        "countType": "sinceImagePushed",
        "countUnit": "days",
        "countNumber": 30
      },
      "action": { "type": "expire" }
    }
  ]
}
```
Apply the policy to the repository:
```bash
aws ecr put-lifecycle-policy --repository-name my-ecr-repo --lifecycle-policy-text file://lifecycle-policy.json
```

### **8.2 Viewing Lifecycle Policies**
```bash
aws ecr get-lifecycle-policy --repository-name my-ecr-repo
```

### **8.3 Deleting a Lifecycle Policy**
```bash
aws ecr delete-lifecycle-policy --repository-name my-ecr-repo
```

---

## **9. Using Amazon ECR with ECS and EKS**
Amazon ECR integrates seamlessly with AWS container orchestration services.

### **9.1 Using ECR with Amazon ECS**
1. Create a task definition in ECS with the ECR image URL.
2. Configure ECS service to pull images from ECR.
3. Deploy the ECS service with auto-scaling.

### **9.2 Using ECR with Amazon EKS**
1. Create an EKS cluster.
2. Configure Kubernetes `Deployment.yaml` to use the ECR image.
3. Ensure EKS worker nodes have necessary IAM permissions to access ECR.

---

## **10. Best Practices for Amazon ECR**

### **10.1 Security Best Practices**
- Use **IAM policies** to restrict repository access.
- Enable **image scanning** to detect vulnerabilities.
- Encrypt images using **AWS KMS encryption**.
- Use **VPC endpoints** for private ECR access.

### **10.2 Cost Optimization Best Practices**
- Implement **lifecycle policies** to delete old images.
- Use **S3 storage tiering** for archived images.
- Monitor ECR usage with **AWS CloudWatch Metrics**.

---

## **Summary**
Amazon ECR provides a secure, scalable, and fully managed container registry service. This guide covered:
- Creating, managing, and securing ECR repositories.
- Pushing and pulling container images.
- Using automated image scanning and lifecycle policies.
- Integrating ECR with ECS and EKS.
- Implementing best practices for security and cost optimization.

