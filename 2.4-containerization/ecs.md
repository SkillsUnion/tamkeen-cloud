# **Amazon Elastic Container Service (ECS)**

## **1. Overview of Amazon ECS**
Amazon Elastic Container Service (ECS) is a fully managed container orchestration service that allows users to run, manage, and scale containerized applications on AWS. ECS supports **EC2 launch type** (running containers on AWS-managed EC2 instances) and **AWS Fargate launch type** (serverless container deployment).

{% include youtube.html id="I9VAMGEjW-Q" %}

### **Key Features of ECS**
- **Fully Managed** – AWS manages the control plane, reducing operational overhead.
- **Flexible Deployment** – Supports both **EC2** and **Fargate** launch types.
- **Deep Integration with AWS Services** – Works with ECR, CloudWatch, IAM, ALB, and more.
- **Auto Scaling** – Automatically scales containers based on demand.
- **Networking and Security** – Integrates with AWS VPC, Security Groups, and IAM roles.
- **Load Balancing** – Works with ALB, NLB, and Cloud Map for service discovery.
- **Spot Instances Support** – Run ECS workloads on cheaper EC2 spot instances.

---

## **2. Setting Up Amazon ECS**

### **2.1 Prerequisites**
- An **AWS account** with administrator access.
- **AWS CLI** installed and configured (`aws configure`).
- **Docker** installed for building and pushing images.
- **Amazon ECR repository** created for storing container images (See [ECR Guide](#)).

### **2.2 Creating an ECS Cluster**
#### **Using AWS Console:**
1. Navigate to **Amazon ECS** in AWS Console.
2. Click **Clusters** > **Create Cluster**.
3. Select **Networking only (Fargate)** or **EC2 Linux + Networking** based on your use case.
4. Configure **Cluster Name**, Networking, and Logging.
5. Click **Create**.

#### **Using AWS CLI:**
```bash
aws ecs create-cluster --cluster-name my-cluster
```

---

## **3. Defining ECS Task Definitions**
A **Task Definition** is a blueprint that defines how a container should run in ECS.

### **3.1 Writing a Task Definition (JSON Format)**
Create a `task-definition.json` file:
```json
{
  "family": "my-app-task",
  "containerDefinitions": [
    {
      "name": "my-app",
      "image": "<aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/my-app:latest",
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

### **3.2 Registering the Task Definition**
```bash
aws ecs register-task-definition --cli-input-json file://task-definition.json
```

---

## **4. Deploying a Service on Amazon ECS**
An **ECS Service** manages the deployment and scaling of tasks across the cluster.

### **4.1 Creating an ECS Service**
#### **Using AWS Console:**
1. Navigate to **ECS > Services**.
2. Click **Create Service**.
3. Select **Launch Type** (Fargate or EC2).
4. Choose the **Task Definition**.
5. Configure **Desired Task Count**.
6. Set up **Networking (VPC, Subnets, Security Groups)**.
7. Enable **Load Balancing** (optional).
8. Click **Create Service**.

#### **Using AWS CLI:**
```bash
aws ecs create-service --cluster my-cluster --service-name my-service \
  --task-definition my-app-task --desired-count 2 --launch-type FARGATE \
  --network-configuration "awsvpcConfiguration={subnets=[subnet-abc123],securityGroups=[sg-xyz456],assignPublicIp=ENABLED}"
```

---

## **5. Scaling and Updating ECS Services**

### **5.1 Scaling an ECS Service**
To scale up a service manually:
```bash
aws ecs update-service --cluster my-cluster --service my-service --desired-count 4
```

To enable auto-scaling:
1. Navigate to **ECS > Services > Auto Scaling**.
2. Set **CPU or Memory Utilization Targets**.
3. Configure **Scaling Policies**.

### **5.2 Updating an ECS Service**
To deploy a new image version:
```bash
aws ecs update-service --cluster my-cluster --service my-service --task-definition my-app-task
```

---

## **6. Monitoring ECS Services**
ECS provides monitoring through **Amazon CloudWatch**.

### **6.1 Viewing ECS Logs**
To check container logs:
```bash
aws logs get-log-events --log-group-name /ecs/my-service --log-stream-name my-container-id
```

### **6.2 Viewing Running Tasks**
```bash
aws ecs list-tasks --cluster my-cluster
```

### **6.3 Describing a Running Task**
```bash
aws ecs describe-tasks --cluster my-cluster --tasks <task_id>
```

---

## **7. Deploying ECS with Load Balancers**

### **7.1 Using an Application Load Balancer (ALB)**
1. Create an **ALB** in **EC2 > Load Balancers**.
2. Attach **ECS target groups**.
3. Enable **path-based routing**.
4. Update the ECS Service to use the ALB.

### **7.2 Updating ECS Service to Use ALB**
```bash
aws ecs update-service --cluster my-cluster --service my-service \
  --load-balancer "targetGroupArn=arn:aws:elasticloadbalancing:region:account-id:targetgroup/my-target-group/abc123,containerName=my-app,containerPort=80"
```

---

## **8. Using IAM Roles for ECS**

### **8.1 Creating an IAM Role for ECS Tasks**
```bash
aws iam create-role --role-name ecsTaskExecutionRole \
  --assume-role-policy-document file://ecs-trust-policy.json
```

### **8.2 Attaching Permissions to ECS Role**
```bash
aws iam attach-role-policy --role-name ecsTaskExecutionRole \
  --policy-arn arn:aws:iam::aws:policy/service-role/AmazonECSTaskExecutionRolePolicy
```

---

## **9. Best Practices for Amazon ECS**

### **9.1 Security Best Practices**
- Use **IAM roles** to restrict access.
- Enable **AWS WAF** to protect APIs.
- Limit **container privileges** (avoid `--privileged` mode).
- Encrypt data using **AWS Secrets Manager**.

### **9.2 Cost Optimization Best Practices**
- Use **Fargate Spot** for lower pricing.
- Scale containers based on **demand**.
- Monitor costs using **AWS Cost Explorer**.

---