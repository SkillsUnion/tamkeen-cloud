# **Kubernetes (K8s)**

## **1. Overview of Kubernetes**
Kubernetes (K8s) is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications.

### **Key Features of Kubernetes**
- **Automated Deployment & Scaling** – Manage applications with declarative configurations.
- **Service Discovery & Load Balancing** – Internal service discovery and traffic distribution.
- **Self-Healing** – Automatic container restarts, replacements, and rescheduling.
- **Storage Orchestration** – Manage persistent storage for containers.
- **Secret & Configuration Management** – Securely manage sensitive data.

---

## **2. Setting Up Kubernetes**

### **2.1 Prerequisites**
- Linux or MacOS machine (Windows requires WSL2)
- `kubectl` installed (`kubectl version`)
- Docker installed (`docker --version`)
- Minikube (for local Kubernetes cluster) installed (`minikube version`)

### **2.2 Installing Kubernetes Locally with Minikube**
1. Start a local Kubernetes cluster:
   ```bash
   minikube start --driver=docker
   ```
2. Verify cluster status:
   ```bash
   kubectl get nodes
   ```

### **2.3 Installing Kubernetes on Cloud Providers**
#### **Google Kubernetes Engine (GKE)**
```bash
gcloud container clusters create my-cluster --num-nodes=3
```
#### **Microsoft Azure Kubernetes Service (AKS)**
```bash
az aks create --resource-group my-resource-group --name my-cluster --node-count 3 --enable-addons monitoring --generate-ssh-keys
```

---

## **3. Deploying Applications on Kubernetes**

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
        image: nginx:latest
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

## **4. Managing Kubernetes Workloads**

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

## **5. Monitoring & Logging in Kubernetes**

### **5.1 Viewing Kubernetes Logs**
```bash
kubectl logs -l app=my-app
```

### **5.2 Monitoring with Prometheus & Grafana**
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

## **6. Kubernetes Networking**

### **6.1 Kubernetes Ingress for Routing**
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-app-ingress
  annotations:
    kubernetes.io/ingress.class: nginx
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

## **7. Security Best Practices for Kubernetes**

### **7.1 Restrict Access Using RBAC**
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: developer-binding
subjects:
- kind: User
  name: dev-user
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: developer-role
  apiGroup: rbac.authorization.k8s.io
```
Apply the role binding:
```bash
kubectl apply -f rbac.yaml
```

### **7.2 Enable Network Policies**
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

## **8. Summary**
This guide covered:
- Kubernetes basics and setup.
- Deploying and managing workloads.
- Networking, security, and monitoring best practices.
