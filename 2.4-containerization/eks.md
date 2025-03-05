# **Amazon Elastic Kubernetes Service (EKS)**

## **1. Overview of Amazon EKS**
Amazon Elastic Kubernetes Service (EKS) is a fully managed Kubernetes service that simplifies deploying, managing, and scaling containerized applications using Kubernetes on AWS.

### **Key Features of EKS**
- **Fully Managed Kubernetes Control Plane** – AWS manages the Kubernetes master nodes.
- **Deep AWS Integration** – Works seamlessly with IAM, VPC, ALB, ECR, and other AWS services.
- **Security & Compliance** – Supports IAM roles, security groups, private networking, and encryption.
- **Auto-Scaling & Load Balancing** – Uses AWS ALB and Cluster Autoscaler for dynamic scaling.
- **Supports EC2 and Fargate** – Run workloads on EC2 worker nodes or serverless with Fargate.

---

{% include youtube.html id="E956xeOt050" %}

## **2. Setting Up Amazon EKS**

### **2.1 Prerequisites**
- An **AWS account** with admin permissions.
- **AWS CLI** installed and configured (`aws configure`).
- **kubectl** installed (`kubectl version`).
- **eksctl** installed (`eksctl version`).
- **AWS IAM role** with EKS permissions.

### **2.2 Creating an EKS Cluster**
#### **Using eksctl (Recommended)**
```bash
eksctl create cluster --name my-cluster --region us-east-1 --nodegroup-name my-nodes --node-type t3.medium --nodes 2
```

#### **Using AWS Console**
1. Navigate to **Amazon EKS** in the AWS Console.
2. Click **Create Cluster** and configure VPC, IAM roles, and networking settings.
3. Add worker nodes by creating a **Node Group**.
4. Wait for the cluster status to become **Active**.

### **2.3 Verifying the Cluster**
```bash
kubectl get nodes
```

---

## **3. Deploying Applications on Amazon EKS**

### **3.1 Creating a Deployment**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app
        image: <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/my-app:latest
        ports:
        - containerPort: 80
```
Apply the deployment:
```bash
kubectl apply -f deployment.yaml
```

### **3.2 Exposing the Application**
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-app-service
spec:
  selector:
    app: my-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
  type: LoadBalancer
```
Apply the service:
```bash
kubectl apply -f service.yaml
```

### **3.3 Checking Application Status**
```bash
kubectl get deployments
kubectl get services
```

---

## **4. Scaling and Updating Applications**

### **4.1 Scaling Applications**
```bash
kubectl scale deployment my-app --replicas=5
```

### **4.2 Updating Applications**
```bash
kubectl set image deployment/my-app my-app=nginx:1.19.0
```

### **4.3 Rolling Back Changes**
```bash
kubectl rollout undo deployment/my-app
```

---

## **5. Monitoring & Logging in Amazon EKS**

### **5.1 Enabling CloudWatch Logging**
```bash
eksctl utils update-cluster-logging --enable-types all --cluster my-cluster --region us-east-1
```

### **5.2 Viewing Kubernetes Logs**
```bash
kubectl logs -l app=my-app
```

### **5.3 Monitoring with Prometheus & Grafana**
1. Deploy Prometheus and Grafana using Helm:
```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install prometheus prometheus-community/kube-prometheus-stack
```

2. Access Grafana dashboard:
```bash
kubectl port-forward svc/prometheus-grafana 3000:80
```

---

## **6. Networking in Amazon EKS**

### **6.1 Kubernetes Ingress with AWS ALB**
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-app-ingress
  annotations:
    alb.ingress.kubernetes.io/scheme: internet-facing
spec:
  rules:
  - host: my-app.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: my-app-service
            port:
              number: 80
```
Apply the ingress:
```bash
kubectl apply -f ingress.yaml
```

---

## **7. Security Best Practices for Amazon EKS**

### **7.1 Restrict Access Using IAM Roles**
```bash
eksctl create iamidentitymapping --cluster my-cluster --arn arn:aws:iam::account-id:role/Admin --group system:masters
```

### **7.2 Enforce Network Policies**
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-web
spec:
  podSelector:
    matchLabels:
      app: my-app
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          app: backend
```
Apply the policy:
```bash
kubectl apply -f network-policy.yaml
```

### **7.3 Enable Secrets Management**
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  username: dXNlcg==  # base64 encoded
  password: cGFzc3dvcmQ=
```
Apply the secret:
```bash
kubectl apply -f secret.yaml
```

---

## **8. Cost Optimization Best Practices for Amazon EKS**

- Use **EC2 Spot Instances** for worker nodes.
- Enable **Cluster Autoscaler** for right-sizing resources.
- Implement **resource requests & limits** to optimize pod usage.
- Monitor costs with **AWS Cost Explorer & CloudWatch Metrics**.

---

## **9. Summary**
- Amazon EKS basics and setup.
- Deploying and managing workloads.
- Monitoring, logging, and security best practices.
- Cost optimization strategies.