# Visual Diagrams and CI/CD Flow Examples

To visualize the end-to-end delivery process using AWS CodePipeline, consider the following common architectural flow:

### **Diagram: Basic CodePipeline CI/CD Flow**

```
+-----------+       +------------+       +------------+       +-------------+       +------------+
| Source    |  -->  | Build      |  -->  | Test       |  -->  | Deploy       |  -->  | Production |
| (GitHub)  |       | (CodeBuild)|       | (Lambda)   |       | (CodeDeploy) |       | (EC2/ECS)  |
+-----------+       +------------+       +------------+       +-------------+       +------------+
```

Each component is an action within its corresponding stage in the CodePipeline. Artifacts flow from left to right, supporting audit, rollback, and traceability.

### **Use Case Example: Deploying a Node.js App**
This example walks through deploying a Node.js application with CodePipeline, using CodeCommit, CodeBuild, and CodeDeploy.

1. **Source Stage**
   - Code is pushed to AWS CodeCommit.
   - CodePipeline is triggered by the push event.

2. **Build Stage**
   - AWS CodeBuild compiles the Node.js application.
   - Output artifacts are stored in an S3 bucket.

3. **Deploy Stage**
   - AWS CodeDeploy performs a blue/green deployment to an Auto Scaling group of EC2 instances.

### **Buildspec Example (buildspec.yml)**
```yaml
version: 0.2
phases:
  install:
    runtime-versions:
      nodejs: 14
    commands:
      - npm install
  build:
    commands:
      - npm run build
artifacts:
  files:
    - '**/*'
```

### **AppSpec Example (appspec.yml)**
```yaml
version: 0.0
os: linux
files:
  - source: /
    destination: /home/ec2-user/app
hooks:
  AfterInstall:
    - location: scripts/restart.sh
      timeout: 60
      runas: ec2-user
```