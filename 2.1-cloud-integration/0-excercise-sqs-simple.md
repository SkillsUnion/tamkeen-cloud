# **AWS SQS (Simple Queue Service)**

## **Prerequisites**
- An **AWS account** with necessary IAM permissions.
- AWS CLI installed and configured (`aws configure`).
- Basic understanding of **JSON/YAML** for AWS CloudFormation.

---

## **Step 1: Create an SQS Queue using AWS CloudFormation**
Instead of using the AWS SDK programmatically, we will define our **SQS queue declaratively** using AWS CloudFormation.

### **1.1 Define the CloudFormation Template**
Create a file named `sqs-template.yaml` and define the SQS queue:

```yaml
AWSTemplateFormatVersion: "2010-09-09"
Resources:
  MyStandardQueue:
    Type: "AWS::SQS::Queue"
    Properties:
      QueueName: "MyStandardQueue"

  MyFIFOQueue:
    Type: "AWS::SQS::Queue"
    Properties:
      QueueName: "MyFIFOQueue.fifo"
      FifoQueue: true
```

### **1.2 Deploy the CloudFormation Stack**
Run the following AWS CLI command to create the SQS queues:
```sh
aws cloudformation create-stack --stack-name SQSStack --template-body file://sqs-template.yaml
```

To check the status of the stack deployment:
```sh
aws cloudformation describe-stacks --stack-name SQSStack
```

---

## **Step 2: Send and Receive Messages using AWS CLI**
Once the SQS queues are created, messages can be sent and retrieved using the **AWS CLI**.

### **2.1 Retrieve the Queue URL**
```sh
aws sqs get-queue-url --queue-name MyStandardQueue
```

### **2.2 Send a Message to the Queue**
```sh
aws sqs send-message --queue-url <queue_url> --message-body '{"orderId": "12345", "status": "pending"}'
```

For FIFO queues, an additional **MessageGroupId** parameter is required:
```sh
aws sqs send-message --queue-url <queue_url> --message-body '{"orderId": "12345", "status": "pending"}' --message-group-id "group1"
```

### **2.3 Receive Messages from the Queue**
```sh
aws sqs receive-message --queue-url <queue_url> --max-number-of-messages 1
```

### **2.4 Delete a Processed Message**
Once a message is processed, it should be deleted:
```sh
aws sqs delete-message --queue-url <queue_url> --receipt-handle <receipt_handle>
```

---

## **Step 3: Clean Up Resources**
To remove the SQS queues and avoid unnecessary costs, delete the CloudFormation stack:
```sh
aws cloudformation delete-stack --stack-name SQSStack
```

---