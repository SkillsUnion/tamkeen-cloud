## Step-by-step: Build a CICD Pipeline for Serverless Applications with AWS SAM and CodePipeline

### Objective
Create a complete CICD pipeline using AWS SAM, CodeCommit, CodeBuild, and CodePipeline to deploy a Node.js serverless application automatically.

---

### Prerequisites
- AWS account with administrative access
- AWS CLI and AWS SAM CLI installed
- Docker installed (for SAM build)
- IAM roles configured for CodeBuild and CodePipeline
- An S3 bucket created for deployment artifacts

---

### Step-by-Step Instructions

#### Step 1: Initialize a Serverless Application
```bash
sam init --runtime nodejs18.x --name my-sam-app --app-template hello-world
cd my-sam-app
```
This creates the project directory and initializes a basic Lambda function and template.

#### Step 2: Create an S3 Bucket for Artifacts
```bash
aws s3 mb s3://<your-unique-bucket-name>
```
This bucket will store SAM build artifacts.

#### Step 3: Set Up a CodeCommit Repository
```bash
aws codecommit create-repository --repository-name my-sam-repo
```
Push your local application:
```bash
git init
aws codecommit credential-helper $'
' git config --global credential.helper '!aws codecommit credential-helper $@'
git remote add origin https://git-codecommit.<region>.amazonaws.com/v1/repos/my-sam-repo
git add .
git commit -m "Initial commit"
git push origin master
```

#### Step 4: Add `buildspec.yml`
Create a `buildspec.yml` file at the root of your project:
```yaml
version: 0.2
phases:
  install:
    runtime-versions:
      nodejs: 18
    commands:
      - npm install -g aws-sam-cli
  build:
    commands:
      - sam build
      - sam package --s3-bucket <your-unique-bucket-name> --output-template-file packaged.yaml
artifacts:
  files:
    - packaged.yaml
```

#### Step 5: Create a CodeBuild Project
```bash
aws codebuild create-project \
  --name sam-build-project \
  --source type=CODECOMMIT,location=https://git-codecommit.<region>.amazonaws.com/v1/repos/my-sam-repo \
  --artifacts type=NO_ARTIFACTS \
  --environment type=LINUX_CONTAINER,computeType=BUILD_GENERAL1_SMALL,image=aws/codebuild/standard:6.0 \
  --service-role <build-service-role-arn>
```

#### Step 6: Define and Deploy the CodePipeline
Use the AWS Console or SAM CLI:
```bash
sam pipeline init
sam pipeline bootstrap
sam deploy --guided
```
This will guide you through setting up the CICD pipeline.

#### Step 7: Make a Code Change and Observe Deployment
Make a change to your handler function and push to CodeCommit. CodePipeline will automatically detect the change, trigger the build, and deploy the updated application.

#### Step 8: Monitor the Deployment
Use CloudWatch or the SAM CLI:
```bash
sam logs -n HelloWorldFunction --stack-name my-sam-app --tail
```
Check logs and metrics in CloudWatch for runtime insights.

#### Step 9: Add Manual Approval (Optional)
Configure a manual approval action in the pipeline before promoting to production.

#### Step 10: Clean Up Resources
To avoid unnecessary charges, remove deployed resources:
```bash
aws cloudformation delete-stack --stack-name my-sam-app
aws s3 rb s3://<your-unique-bucket-name> --force
```

---

### Outcome
By completing this activity, you have:
- Initialized a serverless application using AWS SAM
- Set up a CICD pipeline using CodeCommit, CodeBuild, and CodePipeline
- Deployed a Lambda application automatically from a Git commit
- Gained experience in monitoring, logging, and managing deployments in AWS

This workflow can be further enhanced by adding stages such as canary deployments, integration testing, and post-deployment validations.

