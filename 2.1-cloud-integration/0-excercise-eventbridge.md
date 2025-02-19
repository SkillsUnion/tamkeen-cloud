# **Step-by-Step Guide: Amazon EventBridge**

---

## **Objective**
This guide provides a **comprehensive walkthrough** to help set up and use **Amazon EventBridge** for building **event-driven applications**. The guide focuses on a **single, detailed hands-on activity** to demonstrate **event routing and processing** using EventBridge and AWS Lambda.

---

## **Prerequisites**
- An active **AWS account**.
- Permissions for **EventBridge, Lambda, EC2**, and **IAM** services.
- Basic knowledge of **AWS Management Console**.

---

## **Amazon EventBridge Overview**
Amazon EventBridge is a **serverless event bus service** that enables applications to **connect using events**. It simplifies building **event-driven architectures** by allowing AWS services, SaaS applications, and custom applications to seamlessly **exchange and process real-time event data**.

### **Key Features of EventBridge**
- **Event-Driven Architecture** – Supports event routing from AWS services, SaaS applications, and custom applications.
- **Serverless & Scalable** – Automatically scales to handle **millions of events per second**.
- **Event Filtering & Transformation** – Allows fine-grained event pattern matching and **input transformation**.
- **Security & Compliance** – Integrated with **IAM** and **encryption features**.
- **Schema Registry** – Helps manage **event schemas** for **simpler integrations**.

---

## **Hands-On Activity: Build an Event-Driven Application with EventBridge and Lambda**

### **Scenario**
Create an **event-driven architecture** where **Amazon EventBridge** triggers an **AWS Lambda function** when an **EC2 instance changes state to running**. The Lambda function will **log the event details** to **Amazon CloudWatch Logs**.

---

### **Activity Steps**

### **Step 1: Create an AWS Lambda Function**
1. Navigate to the **AWS Lambda** service in the **AWS Management Console**.
2. Click **Create function**.
3. **Choose a blueprint**: Select **Author from scratch**.
4. **Function name**: `EC2StateChangeLogger`.
5. **Runtime**: `Python 3.9` (or the latest version available).
6. **Role**: Choose **Create a new role with basic Lambda permissions**.
7. Click **Create function**.

#### **Lambda Function Code**
Replace the default code with the following:
```python
import json
import logging

logger = logging.getLogger()
logger.setLevel(logging.INFO)

def lambda_handler(event, context):
    logger.info("Received event: %s", json.dumps(event, indent=2))
    instance_id = event['detail']['instance-id']
    instance_state = event['detail']['state']
    logger.info(f"EC2 Instance {instance_id} is now {instance_state}")
    return {
        'statusCode': 200,
        'body': json.dumps('Event logged successfully!')
    }
```
8. **Click Deploy** to save changes.

---

### **Step 2: Create an EventBridge Rule**
1. Navigate to **Amazon EventBridge**.
2. Go to **Rules** and click **Create rule**.
3. **Name the rule**: `EC2InstanceStateChangeRule`.
4. **Event source**: Select **AWS services**.
5. **Service name**: `EC2`.
6. **Event type**: `EC2 Instance State-change Notification`.
7. **Event pattern**:
```json
{
  "source": ["aws.ec2"],
  "detail-type": ["EC2 Instance State-change Notification"],
  "detail": {
    "state": ["running"]
  }
}
```
8. **Select a target**: Choose **AWS Lambda function**.
9. **Select the function**: `EC2StateChangeLogger`.
10. Click **Create rule**.

---

### **Step 3: Test the Event Flow**
1. **Manually start an EC2 instance**:
   - Navigate to **EC2 service**.
   - **Launch a new instance** or **start an existing stopped instance**.
2. **Check the EventBridge rule**:
   - Navigate to **EventBridge → Rules → EC2InstanceStateChangeRule**.
   - Verify if the rule was triggered.

---

### **Step 4: Verify the Event Handling in CloudWatch**
1. Navigate to **Amazon CloudWatch**.
2. Select **Logs → Log Groups**.
3. Open the **Log Group** associated with `EC2StateChangeLogger`.
4. Review the **log entries**:
   - Check if the event details from the EC2 instance state change are logged.

**Expected Log Output**:
```json
{
  "source": "aws.ec2",
  "detail-type": "EC2 Instance State-change Notification",
  "detail": {
    "instance-id": "i-0123456789abcdef0",
    "state": "running"
  }
}
```

---

### **Step 5: Clean Up Resources**
1. **Disable or delete the EventBridge rule** to prevent unexpected charges.
2. **Delete the Lambda function** (`EC2StateChangeLogger`).
3. **Terminate the EC2 instance** if not needed.
4. **Delete any associated CloudWatch log groups**.

---

## **Summary**
By completing this activity, the following key concepts were demonstrated:
- **Event-Driven Architecture** using **Amazon EventBridge**.
- **Setting up event rules** to filter specific **EC2 state changes**.
- **Triggering a Lambda function** as an event target.
- **Monitoring event processing** through **CloudWatch Logs**.

EventBridge provides a **flexible and powerful event management framework**, allowing applications to **react to changes in real-time** while maintaining **loose coupling** and **scalability**.