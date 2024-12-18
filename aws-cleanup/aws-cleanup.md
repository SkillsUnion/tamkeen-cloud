# AWS Clean-Up

## Overview

The **AWS Clean-Up** aims to guide users in identifying and removing unused or unnecessary AWS resources to minimize costs and maximize free tier benefits. Properly cleaning up resources ensures efficient usage of AWS services while preventing unexpected charges.

---

## Learning Objectives

By the end of this module, you will:

1. Understand the importance of regularly cleaning up AWS resources.
2. Learn to identify unused or underutilized resources.
3. Gain hands-on experience in cleaning up commonly used AWS services.
4. Implement strategies to maintain a cost-effective AWS environment.

---

## Importance of Cleaning Up AWS Resources

### Why Clean Up?

1. **Cost Savings**:
   - Unused resources can accumulate charges.
   - Cleaning up helps reduce unnecessary costs.

2. **Maximizing Free Tier**:
   - AWS Free Tier limits are exceeded if resources are left running.
   - Ensuring only active resources are used keeps you within Free Tier limits.

3. **Security and Compliance**:
   - Unmonitored resources can pose security risks.
   - Cleaning up improves the security posture of your AWS account.

---

## Common AWS Resources to Clean Up

### 1. **EC2 Instances**
   - Stop or terminate unused EC2 instances.
   - Check for running instances in all regions.
   - Remove associated resources:
     - Elastic IPs
     - Attached EBS volumes

### 2. **Elastic Load Balancers (ELBs)**
   - Delete unused ELBs.
   - Clean up associated resources like target groups and listeners.

### 3. **Amazon RDS Instances**
   - Delete unused RDS databases.
   - Ensure snapshots are no longer needed before deletion.

### 4. **S3 Buckets**
   - Delete empty buckets or remove unnecessary objects.
   - Verify that the buckets are not storing sensitive or critical data.

### 5. **IAM Users, Roles, and Policies**
   - Remove unused IAM users and roles.
   - Clean up custom policies no longer in use.

### 6. **VPCs and Networking Resources**
   - Delete unused VPCs, subnets, and route tables.
   - Remove unused Internet Gateways and NAT Gateways.

### 7. **Lambda Functions**
   - Delete unused or test Lambda functions.
   - Remove associated CloudWatch log groups.

### 8. **CloudFormation Stacks**
   - Identify and delete outdated CloudFormation stacks.
   - Ensure resources created by the stack are also removed.

### 9. **Elastic Beanstalk Environments**
   - Terminate environments no longer in use.
   - Delete associated S3 buckets and resources.

### 10. **CloudWatch Alarms and Logs**
   - Delete inactive or outdated alarms.
   - Remove old log groups to save costs.

---

## Step-by-Step Clean-Up Process

### 1. **Identify Unused Resources**
   - Use the AWS Management Console, CLI, or SDKs to list resources.
   - Utilize AWS Trusted Advisor for cost optimization recommendations.
   - Check the AWS Billing Dashboard for a breakdown of charges.

### 2. **Audit Resources**
   - Confirm resource usage with team members.
   - Review tags to identify the owner or purpose of a resource.

### 3. **Delete Resources**
   - Stop or delete unused resources from the console or CLI.
   - Verify deletion to ensure the resource is no longer active.

### 4. **Monitor for Future Clean-Up**
   - Set up CloudWatch alarms for resource usage thresholds.
   - Implement tagging policies to simplify tracking and clean-up.

---

## Best Practices for AWS Clean-Up

1. **Use Automation**:
   - Schedule resource audits using AWS Config or Lambda.
   - Automate clean-up for temporary environments using lifecycle policies.

2. **Tag Resources**:
   - Apply consistent tagging (e.g., `Owner`, `Purpose`, `Environment`).
   - Use tags to identify resources for periodic clean-up.

3. **Enable Billing Alerts**:
   - Set budget alerts to track unexpected cost spikes.

4. **Use AWS Organizations**:
   - Centralize account management for consistent clean-up across multiple accounts.

5. **Document Clean-Up Processes**:
   - Maintain records of clean-up activities for accountability.

---

## Tools for AWS Clean-Up

1. **AWS Trusted Advisor**:
   - Provides cost optimization and clean-up recommendations.
2. **AWS Config**:
   - Tracks resource configurations and changes for audit purposes.
3. **AWS CLI**:
   - Enables batch clean-up operations.
4. **AWS Billing Dashboard**:
   - Helps identify cost-intensive resources.
5. **AWS CloudFormation**:
   - Simplifies resource deletion by managing stacks.

---

## Summary

The AWS Clean-Up Module equips users with strategies to identify and remove unused resources, ensuring a cost-efficient AWS environment. Regular clean-up routines, combined with tagging and monitoring, significantly reduce unexpected expenses and maximize Free Tier benefits.

**Next Steps**:
1. Perform a detailed audit of your AWS account.
2. Start cleaning up resources based on the guidance provided.
3. Set up automation for ongoing clean-up processes.
