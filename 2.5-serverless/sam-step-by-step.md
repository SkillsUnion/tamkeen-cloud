# **Step-by-Step AWS SAM**

## **1. Prerequisites**
Before starting with AWS Serverless Application Model (AWS SAM), ensure you have:
- **AWS Account** – Sign up at [AWS Console](https://aws.amazon.com/).
- **AWS CLI Installed** – Verify installation with:
  ```bash
  aws --version
  ```
- **AWS SAM CLI Installed** – Verify installation with:
  ```bash
  sam --version
  ```
- **IAM Role with Lambda Execution Permissions**.
- **Docker Installed** (for local testing).

---

## **2. Initialize an AWS SAM Project**
AWS SAM provides prebuilt templates to scaffold applications.

### **2.1 Create a New SAM Application**
```bash
sam init
```
### **2.2 Choose Configuration**
- **Choose 1** for AWS Quick Start Templates.
- Select **runtime** (Python, Node.js, Java, Go, etc.).
- **Project Name:** `my-sam-app`
- Navigate to the project directory:
  ```bash
  cd my-sam-app
  ```

---

## **3. Understanding the AWS SAM Project Structure**
After initialization, the directory structure looks like this:
```
my-sam-app/
│── template.yaml  # SAM Template defining AWS resources
│── hello_world/   # Source code for the Lambda function
│   ├── app.py     # Main function handler
│   ├── requirements.txt  # Dependencies
│── events/        # Sample events for testing
│── tests/         # Unit tests
```

---

## **4. Writing an AWS Lambda Function**
### **4.1 Open `hello_world/app.py` and Add the Following Code:**
```python
import json

def lambda_handler(event, context):
    return {
        "statusCode": 200,
        "body": json.dumps({"message": "Hello, AWS SAM!"})
    }
```

### **4.2 Defining the Function in `template.yaml`**
Modify `template.yaml` to include:
```yaml
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31

Resources:
  HelloWorldFunction:
    Type: AWS::Serverless::Function
    Properties:
      Handler: hello_world.app.lambda_handler
      Runtime: python3.8
      CodeUri: hello_world/
      Events:
        HelloWorldAPI:
          Type: Api
          Properties:
            Path: /hello
            Method: GET
```

---

## **5. Building and Testing Locally**
### **5.1 Install Dependencies**
```bash
pip install -r hello_world/requirements.txt
```

### **5.2 Build the Project**
```bash
sam build
```
This processes dependencies and prepares the function for deployment.

### **5.3 Test the Function Locally**
```bash
sam local invoke "HelloWorldFunction"
```
Sample output:
```json
{
  "statusCode": 200,
  "body": "{\"message\": \"Hello, AWS SAM!\"}"
}
```

### **5.4 Test API Gateway Locally**
```bash
sam local start-api
```
Send a request:
```bash
curl http://127.0.0.1:3000/hello
```
Expected output:
```json
{"message": "Hello, AWS SAM!"}
```

---

## **6. Deploying the Application**
### **6.1 Configure AWS Credentials**
Ensure AWS credentials are configured before deployment:
```bash
aws configure
```

### **6.2 Deploy to AWS**
Run the guided deployment:
```bash
sam deploy --guided
```
Follow the prompts to:
- Define stack name (e.g., `sam-app`)
- Select AWS region
- Confirm deployment settings
- Save settings for future deployments

Once deployed, AWS provides an API Gateway URL. Test it using:
```bash
curl https://your-api-id.execute-api.region.amazonaws.com/Prod/hello
```

---

## **7. Managing AWS SAM Deployments**
### **7.1 View Deployed Stack**
```bash
aws cloudformation list-stacks
```

### **7.2 Update the Lambda Function**
Make changes to `hello_world/app.py`, then rebuild and deploy:
```bash
sam build
sam deploy
```

### **7.3 Delete the Stack**
```bash
aws cloudformation delete-stack --stack-name sam-app
```

---

## **8. Monitoring and Debugging AWS SAM Applications**
### **8.1 Checking Logs in CloudWatch**
```bash
aws logs tail /aws/lambda/HelloWorldFunction --follow
```

### **8.2 Enabling Tracing with AWS X-Ray**
Modify `template.yaml` to enable tracing:
```yaml
      Tracing: Active
```
Deploy changes:
```bash
sam deploy
```
View traces:
```bash
aws xray get-service-graph
```

---

## **9. Implementing CICD for AWS SAM**
### **9.1 Using AWS CodePipeline**
1. Store code in **GitHub** or **CodeCommit**.
2. Use **AWS CodeBuild** for building and packaging Lambda.
3. Deploy using **AWS CodeDeploy** with blue/green deployment strategies.

### **9.2 GitHub Actions Workflow for AWS SAM**
Example CICD pipeline:
```yaml
name: Deploy AWS SAM Application
on: [push]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v2
      - name: Install AWS SAM CLI
        run: pip install aws-sam-cli
      - name: Build and Deploy
        run: |
          sam build
          sam deploy --no-confirm-changeset --no-fail-on-empty-changeset
```

---

## **Summary**
- AWS SAM simplifies **serverless application development, testing, and deployment**.
- **SAM CLI** enables local execution and debugging of Lambda functions.
- **Infrastructure as Code (IaC)** using `template.yaml` automates resource provisioning.
- **CICD Pipelines** streamline deployment using AWS CodePipeline or GitHub Actions.
