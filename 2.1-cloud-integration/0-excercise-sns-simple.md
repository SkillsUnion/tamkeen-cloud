# **AWS SNS (Simple Notification Service)**

## **Prerequisites**
- An **AWS account** with necessary IAM permissions.
- AWS CLI installed and configured (`aws configure`).
- Basic understanding of **JSON/YAML** for AWS CloudFormation.

---

## **Step 1: Create an SNS Topic using AWS CloudFormation**
Instead of manually creating an SNS topic, we define it declaratively using **AWS CloudFormation**.

### **1.1 Define the CloudFormation Template**
Create a file named `sns-template.yaml` and define the SNS topic:

```yaml
AWSTemplateFormatVersion: "2010-09-09"
Resources:
  MySNSTopic:
    Type: "AWS::SNS::Topic"
    Properties:
      DisplayName: "My SNS Topic"
      TopicName: "MySNSTopic"
```

### **1.2 Deploy the CloudFormation Stack**
Run the following AWS CLI command to create the SNS topic:
```sh
aws cloudformation create-stack --stack-name SNSTopicStack --template-body file://sns-template.yaml
```

To check the status of the stack deployment:
```sh
aws cloudformation describe-stacks --stack-name SNSTopicStack
```

---

## **Step 2: Subscribe to the SNS Topic using AWS CLI**
Once the SNS topic is created, we subscribe an **email endpoint** to receive notifications.

### **2.1 Retrieve the SNS Topic ARN**
```sh
aws sns list-topics
```

### **2.2 Subscribe an Email Address**
```sh
aws sns subscribe --topic-arn <topic_arn> \
  --protocol email \
  --notification-endpoint your-email@example.com
```
👉 **Confirm the Subscription**:  
AWS will send a confirmation email. Open it and **click the confirmation link**.

---

## **Step 3: Publish Messages to SNS**
After subscription is confirmed, messages can be published using the **AWS CLI**.

### **3.1 Publish a Message**
```sh
aws sns publish --topic-arn <topic_arn> --message "Hello, this is a test notification from AWS SNS!"
```

---

## **Step 4: Clean Up Resources**
To remove the SNS topic and avoid unnecessary costs, delete the CloudFormation stack:
```sh
aws cloudformation delete-stack --stack-name SNSTopicStack
```

---