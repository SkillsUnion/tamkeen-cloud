# **AWS SQS (Simple Queue Service)**

## **Prerequisites**
- An **AWS account** with necessary IAM permissions.
- AWS CLI installed and configured (`aws configure`).
- Node.js installed.

---

## **Step 1: Create an SQS Queue**
You can create an SQS queue using the AWS CLI or the AWS Console.

### **1.1 Using AWS CLI**
To create a **Standard Queue**:
```sh
aws sqs create-queue --queue-name MyStandardQueue
```

To create a **FIFO Queue**:
```sh
aws sqs create-queue --queue-name MyFIFOQueue.fifo --attributes FifoQueue=true
```

### **1.2 Retrieve Queue URL**
```sh
aws sqs get-queue-url --queue-name MyStandardQueue
```

### **1.3 Get Queue Attributes**
```sh
aws sqs get-queue-attributes --queue-url <queue_url> --attribute-names All
```

---

## **Step 2: Integrate SQS with Node.js**
Let's build a simple Node.js application that **sends and receives messages** from the SQS queue.

### **2.1 Install AWS SDK**
```sh
npm install aws-sdk dotenv
```

### **2.2 Configure AWS SDK**
Create a `.env` file:
```
AWS_REGION=us-east-1
AWS_ACCESS_KEY_ID=<your-access-key>
AWS_SECRET_ACCESS_KEY=<your-secret-key>
QUEUE_URL=<your-sqs-queue-url>
```

### **2.3 Send a Message to SQS**
Create `sendMessage.js`:
```javascript
require('dotenv').config();
const AWS = require('aws-sdk');

const sqs = new AWS.SQS({
    region: process.env.AWS_REGION,
    accessKeyId: process.env.AWS_ACCESS_KEY_ID,
    secretAccessKey: process.env.AWS_SECRET_ACCESS_KEY
});

const params = {
    QueueUrl: process.env.QUEUE_URL,
    MessageBody: JSON.stringify({ orderId: "12345", status: "pending" })
};

sqs.sendMessage(params, (err, data) => {
    if (err) {
        console.error("Error sending message:", err);
    } else {
        console.log("Message sent, ID:", data.MessageId);
    }
});
```
Run:
```sh
node sendMessage.js
```

---

### **2.4 Receive Messages from SQS**
Create `receiveMessage.js`:
```javascript
require('dotenv').config();
const AWS = require('aws-sdk');

const sqs = new AWS.SQS({
    region: process.env.AWS_REGION,
    accessKeyId: process.env.AWS_ACCESS_KEY_ID,
    secretAccessKey: process.env.AWS_SECRET_ACCESS_KEY
});

const params = {
    QueueUrl: process.env.QUEUE_URL,
    MaxNumberOfMessages: 1,
    WaitTimeSeconds: 10
};

sqs.receiveMessage(params, (err, data) => {
    if (err) {
        console.error("Error receiving message:", err);
    } else if (data.Messages) {
        console.log("Received message:", JSON.parse(data.Messages[0].Body));

        // Delete the message after processing
        const deleteParams = {
            QueueUrl: process.env.QUEUE_URL,
            ReceiptHandle: data.Messages[0].ReceiptHandle
        };

        sqs.deleteMessage(deleteParams, (err) => {
            if (err) {
                console.error("Error deleting message:", err);
            } else {
                console.log("Message deleted successfully.");
            }
        });
    } else {
        console.log("No messages received.");
    }
});
```
Run:
```sh
node receiveMessage.js
```

---

