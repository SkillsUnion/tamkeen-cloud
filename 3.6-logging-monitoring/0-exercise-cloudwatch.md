## Hands-On Activity: Monitor with AWS CloudWatch (Logs, Metrics, and Alarms)

### Objective
Set up complete AWS CloudWatch monitoring—including Logs, Metrics, and Alarms—for a sample application. This step-by-step lab provides experience with CloudWatch core services and demonstrates how to visualize, analyze, and respond to system events in real time.

---

### Prerequisites
- AWS account with IAM permissions to use CloudWatch, EC2, Lambda, and SNS
- AWS CLI and AWS SAM CLI installed (for deployment and testing)
- Basic understanding of AWS services (EC2, Lambda)

---

### Scenario
You will deploy a simple Lambda application and EC2 instance that emits logs and custom metrics. Then you will:
- Stream logs to CloudWatch Logs
- Create and visualize custom metrics
- Set up alarms to detect performance anomalies

---

### Part 1: Enable and View Logs

#### Step 1: Deploy Lambda (or use existing function)
```bash
sam init --runtime nodejs18.x --name cloudwatch-demo --app-template hello-world
cd cloudwatch-demo
sam deploy --guided
```

#### Step 2: Generate Logs
Invoke your function:
```bash
aws lambda invoke --function-name HelloWorldFunction out.json
```

#### Step 3: View Logs in CloudWatch
- Go to the AWS Console > CloudWatch > Logs > Log Groups
- Search for `/aws/lambda/HelloWorldFunction`
- Review log streams and event details

---

### Part 2: Create and View Custom Metrics

#### Step 4: Emit a Custom Metric
```bash
aws cloudwatch put-metric-data \
  --namespace "CustomApp" \
  --metric-name "ProcessedRecords" \
  --value 25 \
  --unit Count \
  --dimensions Service=Ingestor
```

#### Step 5: Visualize Metric
- Go to CloudWatch > Metrics > CustomApp > Service: Ingestor
- Add metric to a new dashboard

#### Step 6: Add Metric Math (optional)
- In Metrics, create a formula: `Sum(ProcessedRecords) / Time`
- Use this to analyze throughput over time

---

### Part 3: Set Up Alarms and Notifications

#### Step 7: Create SNS Topic
```bash
aws sns create-topic --name cloudwatch-alerts
aws sns subscribe --topic-arn arn:aws:sns:... --protocol email --notification-endpoint your-email@example.com
```

#### Step 8: Create Alarm for CPU on EC2 Instance
```bash
aws cloudwatch put-metric-alarm \
  --alarm-name "HighCPU" \
  --metric-name CPUUtilization \
  --namespace AWS/EC2 \
  --statistic Average \
  --period 300 \
  --threshold 80 \
  --comparison-operator GreaterThanThreshold \
  --evaluation-periods 2 \
  --alarm-actions arn:aws:sns:...:cloudwatch-alerts
```

#### Step 9: Test and Monitor Alarm
- View in CloudWatch > Alarms
- Simulate CPU spike (or adjust threshold to test alarm)
- Confirm notification email is received

---

### Diagram: End-to-End CloudWatch Flow
```text
[Lambda / EC2 / App] → [Logs / Metrics] → [CloudWatch Console]
                                         ↘ [Dashboards / Math]
                                         ↘ [Alarms → SNS / Lambda / Auto Scaling]
```

---

### Cleanup
```bash
aws cloudformation delete-stack --stack-name cloudwatch-demo
aws sns delete-topic --topic-arn arn:aws:sns:...:cloudwatch-alerts
```

---

### Outcome
By completing this activity, you have:
- Enabled log monitoring for Lambda
- Published and visualized custom metrics
- Created alarms with automated notifications
- Built a foundation for full-stack observability using AWS CloudWatch