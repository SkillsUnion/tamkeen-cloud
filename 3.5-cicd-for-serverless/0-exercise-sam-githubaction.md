## Activity: CICD Pipeline for Serverless Applications Using AWS SAM and GitHub Actions

### Objective
This activity guides you in setting up a complete CICD pipeline for deploying a serverless Node.js application using AWS SAM, GitHub, and GitHub Actions.

---

### Prerequisites
- AWS account with administrative permissions
- AWS CLI and AWS SAM CLI installed
- Docker installed (for local SAM builds)
- GitHub repository created for your project
- AWS credentials (Access Key ID and Secret Access Key) to be stored in GitHub Secrets
- An S3 bucket created for deployment artifacts

---

### Step-by-Step Instructions

#### Step 1: Initialize a SAM Application
```bash
sam init --runtime nodejs18.x --name sam-github-app --app-template hello-world
cd sam-github-app
```

#### Step 2: Create an S3 Bucket for Artifacts
```bash
aws s3 mb s3://<your-unique-s3-bucket>
```

#### Step 3: Push Code to GitHub
Initialize Git, commit the code, and push to a GitHub repository:
```bash
git init
git remote add origin https://github.com/<your-username>/<your-repo-name>.git
git add .
git commit -m "Initial commit"
git push -u origin main
```

#### Step 4: Add GitHub Secrets
In your GitHub repository:
- Go to **Settings > Secrets and variables > Actions > New repository secret**
- Add the following secrets:
  - `AWS_ACCESS_KEY_ID`
  - `AWS_SECRET_ACCESS_KEY`
  - `AWS_REGION` (e.g., `ap-southeast-1`)
  - `S3_BUCKET` (your artifact bucket name)

#### Step 5: Create GitHub Actions Workflow
Create the file `.github/workflows/deploy.yml`:
```yaml
name: Deploy SAM Application

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout source
        uses: actions/checkout@v3

      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Set up AWS credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ${{ secrets.AWS_REGION }}

      - name: Install AWS SAM CLI
        run: |
          pip install aws-sam-cli

      - name: Build with SAM
        run: sam build

      - name: Package with SAM
        run: sam package \
          --s3-bucket ${{ secrets.S3_BUCKET }} \
          --output-template-file packaged.yaml

      - name: Deploy with SAM
        run: sam deploy \
          --template-file packaged.yaml \
          --stack-name sam-github-stack \
          --capabilities CAPABILITY_IAM \
          --region ${{ secrets.AWS_REGION }}
```

#### Step 6: Test Your Pipeline
Make any code change, commit, and push to `main`. Monitor the **Actions** tab in GitHub to observe workflow execution and successful deployment.

#### Step 7: Verify Deployment
Check your AWS Lambda console or CloudFormation stack to confirm the application is deployed. You can also use:
```bash
aws cloudformation describe-stacks --stack-name sam-github-stack
```

#### Step 8: Clean Up (Optional)
```bash
aws cloudformation delete-stack --stack-name sam-github-stack
aws s3 rb s3://<your-unique-s3-bucket> --force
```

---

### Outcome
By completing this activity, you have:
- Initialized and pushed a serverless application to GitHub
- Created a secure GitHub Actions workflow to automate deployment using AWS SAM
- Successfully deployed a Lambda function using CICD

This setup can be extended with stages for testing, linting, and security scanning.

