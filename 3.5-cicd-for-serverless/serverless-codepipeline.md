## AWS Serverless End-to-End Pipeline with CodePipeline


{% include youtube.html id="GEWrpZuBEkQ" %}

### Overview
This topic guides you through designing and implementing a complete end-to-end CICD pipeline for AWS serverless applications using AWS CodePipeline. It leverages AWS-native tools—CodeCommit, CodeBuild, CodeDeploy (via SAM), and CloudFormation—to fully automate deployments of Lambda-based applications.

The pipeline supports multiple environments (dev/staging/prod), handles infrastructure and application code changes, and enforces security and observability best practices. References include the *AWS CodePipeline User Guide (2025)* and *AWS Serverless Application Model Developer Guide (2025)*.

---

### Learning Objectives
By the end of this topic, you will:

1. Design a multi-stage CICD pipeline for serverless applications.
2. Automate infrastructure and code deployments using CodePipeline.
3. Use CodeBuild to package and test Lambda functions.
4. Deploy infrastructure as code using AWS SAM and CloudFormation.
5. Monitor and secure the CICD workflow using CloudWatch and IAM best practices.

---

### Architecture Diagram
```text
[CodeCommit] 
    ↓
[CodePipeline - Source Stage] 
    ↓
[CodeBuild - Build & Package Stage] 
    ↓
[S3 - Store Packaged Artifacts] 
    ↓
[CloudFormation via CodePipeline - Deploy Stage] 
    ↓
[Lambda/API Gateway/DynamoDB]
```

---

### Key Components and Their Roles
| Stage             | AWS Service        | Description                                                        |
|------------------|--------------------|--------------------------------------------------------------------|
| Source Control    | CodeCommit         | Hosts source code and templates. Triggers builds via webhook.     |
| Build & Package   | CodeBuild + SAM CLI| Automates building, testing, and packaging Lambda artifacts.       |
| Artifact Store    | Amazon S3          | Stores built templates and Lambda deployment packages.            |
| Deployment        | CodePipeline + SAM | Executes CloudFormation stacks for deployment.                    |
| Monitoring        | CloudWatch, X-Ray  | Tracks logs, metrics, and traces for deployed services.           |
| Security          | IAM, SecretsMgr    | Manages access and secrets securely throughout the pipeline.      |

CodePipeline supports **parallel** and **queued** execution modes, enabling flexible pipeline scheduling and avoiding race conditions in deployments【18†source】.

---

### Step-by-Step Pipeline Setup

#### Step 1: Prepare the Application Repository
Create a project structure containing:
- A `template.yaml` file defining the infrastructure (using AWS SAM syntax).
- A `buildspec.yml` for CodeBuild to run builds.
- Application code in a folder (e.g., `src/`).

**Sample buildspec.yml:**
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
      - sam package --output-template-file packaged.yaml --s3-bucket $ARTIFACT_BUCKET
artifacts:
  files:
    - packaged.yaml
```

#### Step 2: Bootstrap with SAM
Use the SAM CLI to prepare your CICD environment:
```bash
sam pipeline bootstrap --region ap-southeast-1 \
  --stack-name serverless-ci-resources \
  --pipeline-user-arn arn:aws:iam::123456789012:user/pipeline-user
```

#### Step 3: Initialize the Pipeline
Run:
```bash
sam pipeline init
```
This creates starter pipeline templates that can be modified or deployed via the AWS CLI or Management Console.

---

### Implementing Pipeline Stages

- **Source Stage** pulls code from CodeCommit, GitHub, or Bitbucket.
- **Build Stage** triggers CodeBuild to run `sam build` and `sam package`.
- **Deploy Stage** runs CloudFormation via CodePipeline, using `packaged.yaml`.
- **Approval Stage** (optional) for manual promotion to production.

Each stage can output and consume **artifacts**, with dependency flow managed by CodePipeline’s execution model【18†source】.

---

### Deployment and Promotion Strategies
- **Canary Deployments:** Gradual rollout with `AutoPublishAlias` and weighted routing.
- **Blue/Green Deployments:** Deploy alongside old version and shift traffic.
- **Manual Approvals:** Insert human checkpoints before production rollout.

CodePipeline integrates with Amazon SNS for sending notifications on pipeline transitions or approvals【18†source】.

---

### Monitoring and Observability
- **CloudWatch Logs:** Logs for Lambda, CodeBuild, and API Gateway.
- **AWS X-Ray:** Distributed tracing to visualize request flow.
- **sam logs:** Quick CLI access to function logs.

Create alarms and dashboards to track metrics like error rate, latency, and invocation count.

---

### Security Considerations
- **Scoped IAM Roles:** Assign least-privilege roles to each service.
- **Secrets Handling:** Store secrets in AWS Secrets Manager or SSM Parameter Store.
- **Audit Logging:** Enable AWS CloudTrail to log actions across the pipeline【18†source】.

---

### Using AWS SAM Templates
AWS SAM simplifies defining resources. Example below provisions a function, API, and DynamoDB table with 23 lines of code:
```yaml
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
Resources:
  getAllItemsFunction:
    Type: AWS::Serverless::Function
    Properties:
      Handler: src/get-all-items.getAllItemsHandler
      Runtime: nodejs20.x
      Events:
        Api:
          Type: HttpApi
          Properties:
            Path: /
            Method: GET
  SampleTable:
    Type: AWS::Serverless::SimpleTable
```
SAM transforms this into over 200 lines of CloudFormation syntax during deployment【19†source】.

---

### Conclusion
An AWS-native CICD pipeline using CodePipeline provides repeatable, secure, and scalable serverless deployments. Combined with AWS SAM and other serverless tools, developers can ship production-ready features faster and with greater confidence.

> Learn more from the [AWS Serverless Patterns Workshop](https://catalog.workshops.aws/serverless-patterns) and [AWS SAM Docs](https://docs.aws.amazon.com/serverless-application-model/).