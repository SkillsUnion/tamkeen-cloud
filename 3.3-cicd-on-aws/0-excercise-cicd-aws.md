# CICD Pipeline Activity: Node.js App with CodePipeline, CodeBuild, and CodeDeploy

## Objective
Build and deploy a Node.js application using a fully automated CICD pipeline with AWS services: CodeCommit, CodeBuild, CodeDeploy, and CodePipeline.

## Prerequisites
- AWS CLI configured
- S3 bucket for storing artifacts
- IAM roles for CodePipeline, CodeBuild, and CodeDeploy
- EC2 instance with CodeDeploy agent installed
- Sample Node.js application with `appspec.yml` and `buildspec.yml`

## Step-by-Step Guide

### Step 1: Create S3 Bucket
```bash
aws s3 mb s3://my-nodejs-artifacts-bucket
```

### Step 2: Create CodeCommit Repository
```bash
aws codecommit create-repository \
  --repository-name nodejs-ci-app \
  --repository-description "Node.js CICD App"
```
Push your Node.js app:
```bash
git remote add origin https://git-codecommit.<region>.amazonaws.com/v1/repos/nodejs-ci-app
git push -u origin main
```

### Step 3: Prepare EC2 for Deployment
- Launch EC2 with Amazon Linux 2
- Install CodeDeploy agent:
```bash
sudo yum update -y
sudo yum install ruby wget -y
cd /home/ec2-user
wget https://aws-codedeploy-<region>.s3.amazonaws.com/latest/install
chmod +x ./install
sudo ./install auto
sudo service codedeploy-agent start
```
- Tag EC2: `Key=Name, Value=NodejsDeployTarget`
- Attach IAM role with `AmazonEC2RoleforAWSCodeDeploy`

### Step 4: Create AppSpec File
`appspec.yml` in your app root:
```yaml
version: 0.0
os: linux
files:
  - source: /
    destination: /home/ec2-user/app
hooks:
  AfterInstall:
    - location: scripts/start.sh
      timeout: 300
      runas: ec2-user
```
`scripts/start.sh`:
```bash
#!/bin/bash
cd /home/ec2-user/app
npm install
node index.js &
```

### Step 5: Define Buildspec for CodeBuild
`buildspec.yml`:
```yaml
version: 0.2
phases:
  install:
    runtime-versions:
      nodejs: 16
  build:
    commands:
      - echo "Zipping build output"
      - zip -r build-output.zip .
artifacts:
  files:
    - build-output.zip
```

### Step 6: Create CodeBuild Project
```bash
aws codebuild create-project \
  --name nodejs-codebuild-project \
  --source type=CODECOMMIT,location=nodejs-ci-app \
  --artifacts type=S3,location=my-nodejs-artifacts-bucket \
  --environment type=LINUX_CONTAINER,image=aws/codebuild/standard:7.0,computeType=BUILD_GENERAL1_SMALL \
  --service-role arn:aws:iam::<account>:role/codebuild-role
```

### Step 7: Create CodeDeploy App & Group
```bash
aws deploy create-application --application-name NodejsApp

aws deploy create-deployment-group \
  --application-name NodejsApp \
  --deployment-group-name NodejsDeploymentGroup \
  --deployment-config-name CodeDeployDefault.OneAtATime \
  --ec2-tag-filters Key=Name,Value=NodejsDeployTarget,Type=KEY_AND_VALUE \
  --service-role-arn arn:aws:iam::<account>:role/codedeploy-role
```

### Step 8: Define CodePipeline
Create `pipeline.json` and run:
```bash
aws codepipeline create-pipeline --cli-input-json file://pipeline.json
```

Sample `pipeline.json`:
```json
{
  "pipeline": {
    "name": "NodejsCICDPipeline",
    "roleArn": "arn:aws:iam::<account>:role/codepipeline-role",
    "artifactStore": {
      "type": "S3",
      "location": "my-nodejs-artifacts-bucket"
    },
    "stages": [
      {
        "name": "Source",
        "actions": [
          {
            "name": "SourceAction",
            "actionTypeId": {
              "category": "Source",
              "owner": "AWS",
              "provider": "CodeCommit",
              "version": "1"
            },
            "outputArtifacts": [
              {"name": "SourceOutput"}
            ],
            "configuration": {
              "RepositoryName": "nodejs-ci-app",
              "BranchName": "main"
            },
            "runOrder": 1
          }
        ]
      },
      {
        "name": "Build",
        "actions": [
          {
            "name": "BuildAction",
            "actionTypeId": {
              "category": "Build",
              "owner": "AWS",
              "provider": "CodeBuild",
              "version": "1"
            },
            "inputArtifacts": [
              {"name": "SourceOutput"}
            ],
            "outputArtifacts": [
              {"name": "BuildOutput"}
            ],
            "configuration": {
              "ProjectName": "nodejs-codebuild-project"
            },
            "runOrder": 1
          }
        ]
      },
      {
        "name": "Deploy",
        "actions": [
          {
            "name": "DeployAction",
            "actionTypeId": {
              "category": "Deploy",
              "owner": "AWS",
              "provider": "CodeDeploy",
              "version": "1"
            },
            "inputArtifacts": [
              {"name": "BuildOutput"}
            ],
            "configuration": {
              "ApplicationName": "NodejsApp",
              "DeploymentGroupName": "NodejsDeploymentGroup"
            },
            "runOrder": 1
          }
        ]
      }
    ],
    "version": 1
  }
}
```

### Step 9: Trigger and Test
Push code to CodeCommit and watch the pipeline execute:
- Source → Build → Deploy
- Verify the app is running on the EC2 instance.

---

## Sample Node.js Application

Here is a minimal structure for a Node.js app that works with this pipeline:

**project structure**
```
nodejs-ci-app/
├── appspec.yml
├── buildspec.yml
├── index.js
├── package.json
└── scripts/
    └── start.sh
```

**index.js**
```javascript
const http = require('http');

const hostname = '0.0.0.0';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello from CodePipeline CICD!\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

**package.json**
```json
{
  "name": "nodejs-ci-app",
  "version": "1.0.0",
  "description": "Simple Node.js app for CICD",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "author": "AWS Learner",
  "license": "MIT"
}
```