# **AWS SNS (Simple Notification Service)**

## **Prerequisites**
- An **AWS account** with necessary IAM permissions.
- AWS CLI installed and configured (`aws configure`).
- Node.js installed.

---

## **Step 1: Create an SNS Topic**
An SNS topic is a logical access point where publishers send messages, and subscribers receive them.

### **1.1 Using AWS CLI**
```sh
aws sns create-topic --name MySNSTopic
```
Response:
```json
{
    "TopicArn": "arn:aws:sns:us-east-1:123456789012:MySNSTopic"
}
```

### **1.2 Retrieve Topic ARN**
```sh
aws sns list-topics
```

---

## **Step 2: Subscribe to the SNS Topic**
### **2.1 Subscribe an Email**
```sh
aws sns subscribe --topic-arn arn:aws:sns:us-east-1:123456789012:MySNSTopic \
  --protocol email \
  --notification-endpoint your-email@example.com
```
👉 **Confirm the Subscription**: AWS will send a confirmation email. Open it and click the confirmation link.


## **Step 3: Publish Messages to SNS**
### **3.1 Publish a Message using AWS CLI**
```sh
aws sns publish --topic-arn arn:aws:sns:us-east-1:123456789012:MySNSTopic \
  --message "Hello, this is a test notification from AWS SNS!"
```

### **3.2 Publish Messages using Node.js**
Install AWS SDK:
```sh
npm install aws-sdk dotenv
```

Create `.env` file:
```
AWS_REGION=us-east-1
AWS_ACCESS_KEY_ID=<your-access-key>
AWS_SECRET_ACCESS_KEY=<your-secret-key>
TOPIC_ARN=arn:aws:sns:us-east-1:123456789012:MySNSTopic
```

Create `publishMessage.js`:
```javascript
require('dotenv').config();
const AWS = require('aws-sdk');

const sns = new AWS.SNS({
    region: process.env.AWS_REGION,
    accessKeyId: process.env.AWS_ACCESS_KEY_ID,
    secretAccessKey: process.env.AWS_SECRET_ACCESS_KEY
});

const params = {
    Message: "Hello from AWS SNS!",
    TopicArn: process.env.TOPIC_ARN
};

sns.publish(params, (err, data) => {
    if (err) {
        console.error("Error publishing message:", err);
    } else {
        console.log("Message sent successfully:", data.MessageId);
    }
});
```
Run:
```sh
node publishMessage.js
```
