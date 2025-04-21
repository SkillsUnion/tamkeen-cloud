# Hands-On Activity: Building and Pushing Container Images to AWS

## Objective
This activity walks you through building a Docker image for a simple Node.js application and pushing it to Amazon Elastic Container Registry (ECR) using the AWS CLI.

By the end of this activity, you will have:
- Created an ECR repository
- Built and tagged a Docker image
- Pushed the image to ECR
- Verified that the image is available for deployment
- Automated the entire process using AWS CodeBuild and CodePipeline

---

## Prerequisites
- AWS CLI configured with necessary IAM permissions
- Docker installed locally (for initial build)
- IAM roles for CodeBuild and CodePipeline
- An S3 bucket for storing artifacts
- A Node.js app with a Dockerfile and buildspec.yml

---

## Part 1: Manual Build and Push to ECR

### Step 1: Create an Amazon ECR Repository
```bash
aws ecr create-repository \
  --repository-name my-node-app \
  --region <your-region>
```

### Step 2: Authenticate Docker with ECR
```bash
aws ecr get-login-password \
  --region <your-region> \
  | docker login --username AWS --password-stdin <account_id>.dkr.ecr.<region>.amazonaws.com
```

### Step 3: Prepare a Sample App
```bash
git clone https://github.com/aws-samples/aws-nodejs-sample
cd aws-nodejs-sample
```

### Step 4: Dockerfile
```Dockerfile
FROM node:16
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
CMD ["node", "index.js"]
```

### Step 5: Build and Tag the Image
```bash
docker build -t my-node-app .
docker tag my-node-app:latest <account_id>.dkr.ecr.<region>.amazonaws.com/my-node-app:latest
```

### Step 6: Push to ECR
```bash
docker push <account_id>.dkr.ecr.<region>.amazonaws.com/my-node-app:latest
```

### Step 7: Confirm Upload
```bash
aws ecr describe-images --repository-name my-node-app
```

---