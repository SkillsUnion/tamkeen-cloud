# **Step-by-Step AWS Step Functions Tutorial with AWS Lambda**

## **1. Prerequisites**
Before starting, ensure you have the following:
- **AWS Account** – Sign up at [AWS Console](https://aws.amazon.com/)
- **AWS CLI Installed** – Verify installation:
  ```bash
  aws --version
  ```
- **AWS IAM Role with Step Functions and Lambda Permissions**
- **AWS SAM CLI Installed** (optional for local testing)

---

## **2. Overview of AWS Step Functions with Lambda**
AWS Step Functions help orchestrate AWS Lambda functions and other services using state machines. In this tutorial, we will:
1. Create a **Lambda function** to process an input.
2. Define a **Step Functions state machine** to call the Lambda function.
3. Deploy and execute the workflow.

---

## **3. Creating an AWS Lambda Function**
### **3.1 Writing the Lambda Function Code**
Create a file called `lambda_function.py`:
```python
import json

def lambda_handler(event, context):
    name = event.get("name", "User")
    message = f"Hello, {name}! This is a Step Function execution."
    return {
        "statusCode": 200,
        "body": json.dumps({"message": message})
    }
```

### **3.2 Deploying the Lambda Function Using AWS CLI**
1. Create a ZIP package:
   ```bash
   zip function.zip lambda_function.py
   ```
2. Create an IAM role with Lambda execution permissions:
   ```bash
   aws iam create-role --role-name LambdaStepFunctionRole \
       --assume-role-policy-document file://trust-policy.json
   ```
   Sample `trust-policy.json` file:
   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Effect": "Allow",
         "Principal": {"Service": "lambda.amazonaws.com"},
         "Action": "sts:AssumeRole"
       }
     ]
   }
   ```
3. Attach policies to the role:
   ```bash
   aws iam attach-role-policy --role-name LambdaStepFunctionRole \
       --policy-arn arn:aws:iam::aws:policy/service-role/AWSLambdaBasicExecutionRole
   ```
4. Deploy the Lambda function:
   ```bash
   aws lambda create-function --function-name StepFunctionLambda \
       --runtime python3.8 --role arn:aws:iam::123456789012:role/LambdaStepFunctionRole \
       --handler lambda_function.lambda_handler --zip-file fileb://function.zip
   ```

---

## **4. Creating a Step Functions State Machine**
### **4.1 Writing the State Machine Definition**
Create a file called `state_machine.json`:
```json
{
  "Comment": "Step Function with Lambda",
  "StartAt": "InvokeLambda",
  "States": {
    "InvokeLambda": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:us-east-1:123456789012:function:StepFunctionLambda",
      "End": true
    }
  }
}
```

### **4.2 Deploying the State Machine**
1. Create an IAM role for Step Functions:
   ```bash
   aws iam create-role --role-name StepFunctionExecutionRole \
       --assume-role-policy-document file://step-functions-trust-policy.json
   ```
   Sample `step-functions-trust-policy.json`:
   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Effect": "Allow",
         "Principal": {"Service": "states.amazonaws.com"},
         "Action": "sts:AssumeRole"
       }
     ]
   }
   ```
2. Attach policies to the role:
   ```bash
   aws iam attach-role-policy --role-name StepFunctionExecutionRole \
       --policy-arn arn:aws:iam::aws:policy/service-role/AWSLambdaRole
   ```
3. Create the Step Function:
   ```bash
   aws stepfunctions create-state-machine --name LambdaStateMachine \
       --definition file://state_machine.json \
       --role-arn arn:aws:iam::123456789012:role/StepFunctionExecutionRole
   ```

---

## **5. Executing the Step Function**
### **5.1 Manually Starting Execution**
```bash
aws stepfunctions start-execution \
  --state-machine-arn arn:aws:states:us-east-1:123456789012:stateMachine:LambdaStateMachine \
  --input '{"name": "Alice"}'
```

### **5.2 Checking Execution Status**
```bash
aws stepfunctions describe-execution --execution-arn <execution-arn>
```
Replace `<execution-arn>` with the ARN returned when starting the execution.

### **5.3 Viewing Execution Logs**
1. Navigate to **AWS CloudWatch Logs**.
2. Find logs under `/aws/lambda/StepFunctionLambda`.
3. Use AWS CLI:
   ```bash
   aws logs tail /aws/lambda/StepFunctionLambda --follow
   ```

---

## **6. Adding a Choice State for Conditional Logic**
Modify `state_machine.json` to include decision-making:
```json
{
  "Comment": "Step Function with Choice State",
  "StartAt": "CheckInput",
  "States": {
    "CheckInput": {
      "Type": "Choice",
      "Choices": [
        {
          "Variable": "$.name",
          "StringEquals": "Alice",
          "Next": "GreetAlice"
        }
      ],
      "Default": "GreetDefault"
    },
    "GreetAlice": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:us-east-1:123456789012:function:StepFunctionLambda",
      "End": true
    },
    "GreetDefault": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:us-east-1:123456789012:function:StepFunctionLambda",
      "End": true
    }
  }
}
```
Deploy the updated state machine:
```bash
aws stepfunctions update-state-machine --state-machine-arn arn:aws:states:us-east-1:123456789012:stateMachine:LambdaStateMachine \
  --definition file://state_machine.json
```

---