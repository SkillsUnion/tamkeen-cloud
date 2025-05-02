## AWS CloudWatch Metrics

### Introduction
Amazon CloudWatch Metrics provide critical observability into the performance and health of your AWS infrastructure and applications. Metrics are the backbone of monitoring, allowing you to track changes over time, analyze trends, and respond to incidents. CloudWatch collects both default metrics from AWS services and custom metrics from your own applications, delivering high-resolution, real-time insights.


{% include youtube.html id="Yxl7e88cTAQ" %}

---

### What Are CloudWatch Metrics?

A metric represents a time-ordered set of data points. Each metric belongs to a **namespace** (e.g., `AWS/EC2`, `AWS/Lambda`) and is uniquely defined by a **name** and a set of **dimensions** (e.g., `InstanceId`, `FunctionName`). Metrics are stored for 15 months and can be retrieved using various statistics like `Average`, `Minimum`, `Maximum`, `Sum`, and `SampleCount`.

---

### Types of Metrics

1. **Default (Service) Metrics**
   - Automatically collected by AWS services like EC2, RDS, Lambda, S3, DynamoDB, and API Gateway.
   - Examples: `CPUUtilization`, `NetworkIn`, `Latency`, `Throttles`, `Invocations`, `Errors`.

2. **Custom Metrics**
   - Created by developers using the AWS CLI, SDKs, or CloudWatch Agent.
   - Useful for application-level indicators (e.g., queue depth, active users).
   - Support standard (1-minute) and high-resolution (1-second) data points.

3. **High-Resolution Metrics**
   - Enable granular observability with 1-second intervals.
   - Ideal for tracking latency-sensitive or high-frequency applications.

---

### How to Publish Custom Metrics

#### Using AWS CLI
```bash
aws cloudwatch put-metric-data \
  --namespace "MyApp" \
  --metric-name "ActiveUsers" \
  --value 120 \
  --dimensions AppVersion=1.0,Region=us-east-1
```

#### Using AWS SDK (Node.js Example)
```javascript
const AWS = require('aws-sdk');
const cw = new AWS.CloudWatch();
cw.putMetricData({
  Namespace: 'MyApp',
  MetricData: [{
    MetricName: 'ActiveUsers',
    Dimensions: [{ Name: 'Region', Value: 'us-east-1' }],
    Unit: 'Count',
    Value: 120
  }]
}).promise();
```

---

### Metric Math and Anomaly Detection

1. **Metric Math**
   - Perform calculations across multiple metrics.
   - Examples: Error rate = `Errors / Invocations * 100`, or combining EC2 CPU metrics.

2. **Anomaly Detection**
   - Uses machine learning to create a band of expected values.
   - Alarms can trigger when a metric breaches the anomaly band.

---

### Diagram: Metric Lifecycle

```text
[Data Source: AWS Service / App]
     ↓
[Metric Namespace + Dimensions]
     ↓
[CloudWatch Metrics Storage]
     ↓
[Alarms / Dashboards / Math / Anomaly Detection]
```

---

### Visualization and Dashboards

- Use CloudWatch Dashboards to create widgets (line, stacked, number, gauge).
- Group metrics by service, region, or environment.
- Use filters and legends for multi-metric comparisons.

---

### Alarms Based on Metrics

- Alarms trigger when a threshold is breached.
- Support `Static`, `Step`, or `Anomaly` thresholds.
- Integration with Amazon SNS, Lambda, or Auto Scaling.

#### Example: Alarm on CPUUtilization
```bash
aws cloudwatch put-metric-alarm \
  --alarm-name "HighCPU" \
  --metric-name "CPUUtilization" \
  --namespace "AWS/EC2" \
  --statistic "Average" \
  --period 300 \
  --threshold 80 \
  --comparison-operator "GreaterThanThreshold" \
  --evaluation-periods 2 \
  --alarm-actions arn:aws:sns:us-east-1:123456789012:NotifyMe
```

---

### Best Practices

- **Use High-Resolution Metrics** for short-lived or bursty applications.
- **Tag Resources and Metrics** for better organization and cost tracking.
- **Aggregate Across Dimensions** for service-level KPIs.
- **Export Key Metrics to Dashboards** and regularly review them.
- **Combine with Logs and Traces** for full observability.

---

### Limitations and Considerations

- CloudWatch has default quotas (e.g., 10 standard metrics per alarm).
- High-resolution metrics incur additional cost.
- Ensure metric names and namespaces follow naming conventions.

---

### Summary
CloudWatch Metrics form the foundation of AWS monitoring. Whether you're tracking EC2 performance, Lambda error rates, or custom application behavior, metrics provide the quantitative data you need for automation, alerting, and optimization. When combined with dashboards, metric math, and anomaly detection, CloudWatch Metrics enable proactive cloud operations.

> Explore more: [CloudWatch Metrics Documentation](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/working_with_metrics.html)