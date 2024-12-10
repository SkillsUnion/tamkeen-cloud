# Programme Methodology

## Flipped Classroom

This program adopts a flipped-classroom model where we expects students to review lectures and course materials before class, and spend class time clarifying concepts and completing exercises with the guidance of a section leader.

# How to Unblock Yourself in Cloud Engineering

### General Tips

When working with Cloud Engineering tasks, especially on AWS, it's important to follow a structured approach to solve problems. Here are three steps to unblock yourself when encountering a roadblock:

1. **Trace the Error Message**: Start by tracing the error message. What is the root cause? If addressing one error leads to another, continue troubleshooting step by step until no more error messages appear. If no error message is provided, try adding more logging (e.g., using `console.log` in Lambda functions or CloudWatch logs in AWS services) to gather additional clues.
   
2. **Google the Error Message and Context**: If you have a specific error message, combine it with the context of the technology you're working with. For example, if you're facing issues with an EC2 instance not starting, search for "EC2 instance not starting AWS error." By skimming through relevant Google results, you can find potential solutions and dive deeper into promising answers.

3. **Ask for Help**: When you're stuck, ask for help. Share the context about the problem, what you've learned from debugging and Googling, and the error you're encountering. Ask your peers, mentors, or the section leader in your program's communication channel (e.g., Discord or Slack). Providing context will allow others to assist you more effectively.

### How to Use Google Effectively

As a Cloud Engineer, you'll often face issues related to AWS configurations, infrastructure setup, or integration of services. You will need to use Google to troubleshoot problems that aren't explicitly covered in your curriculum. Searching effectively is a key skill, as many Cloud Engineers spend a large portion of their time finding solutions through online resources.

When searching for solutions, combine error messages with relevant technologies to narrow down your search. For instance:

- "EC2 instance not starting AWS"
- "Error 403 S3 access denied"
- "Lambda function timeout AWS"

As you gain more experience, you will better identify the right resources and recognize patterns in the results. Focus on the most relevant information, and avoid unnecessary reading. Platforms like **Stack Overflow**, **AWS documentation**, and **forums** are great places to find solutions.

### How to Ask Questions for Help

When asking for help, always provide enough context. The more specific you are, the easier it is for others to help you. Here's a template for providing context with your technical questions:

1. **What is the error message?**
2. **What do you think is the problem?**
3. **What have you learned from debugging and Googling?**
4. **What is the relevant code or configuration causing the problem?**

Compare the following examples to see how context can help others assist you more effectively:

#### Question 1: No Context

> "My CloudFormation stack is failing. Please help!"

#### Question 2: Incomplete Context

> "My CloudFormation stack is failing. I get the error 'ResourceNotFound: AWS::S3::Bucket'. Please help!"

#### Question 3: Full Context

> "I'm encountering the error 'ResourceNotFound: AWS::S3::Bucket' in my CloudFormation stack on line 15. The stack attempts to create an S3 bucket, but it seems the bucket name conflicts with an existing resource. I’ve checked AWS documentation on naming constraints but can’t find a solution. Below is the relevant code for the resource definition."
>
> ```yaml
> Resources:
>   MyS3Bucket:
>     Type: 'AWS::S3::Bucket'
>     Properties:
>       BucketName: 'my-existing-bucket-name'
> ```
>
> Any suggestions on how to resolve this?

By including the error message, what you think the problem might be, your attempts to solve it, and the relevant code or configuration, you're giving others the information they need to help you solve the issue faster.

### Additional Tips for Debugging AWS Issues

- **Check CloudWatch Logs**: AWS services like Lambda, EC2, and API Gateway generate logs in CloudWatch. Check these logs for detailed error messages and timestamps to help pinpoint the issue.
  
- **Review IAM Permissions**: Many errors in AWS stem from incorrect IAM policies. Ensure that the correct roles and permissions are applied to your services.
  
- **Verify Resource Configuration**: Double-check configurations like security groups, VPC settings, and AWS networking to ensure proper communication between services (e.g., EC2 instances and RDS databases).


### **How to Document Your Errors in Cloud Engineering (AWS Focus)**

In Cloud Engineering, documenting errors effectively is crucial to debugging and resolving issues efficiently, especially when working with AWS services. This process helps both individuals and teams to quickly identify and resolve issues, minimizing downtime and improving collaboration.

### **AWS Infrastructure Errors**

When working with AWS infrastructure, errors often stem from misconfigured resources, permissions, or connectivity issues. Below is how to document such errors.

**Documenting AWS Service Errors**

AWS provides comprehensive logging through **CloudWatch Logs** for almost all services. Here’s how to document an error that occurs within AWS resources like EC2, RDS, or Lambda.

1. **Check CloudWatch Logs**: When an error occurs in any AWS service, such as a Lambda function failure or an EC2 instance not starting, the error will typically be logged in **CloudWatch Logs**.
   
2. **Review the Error Message**: Read the error message to understand where the issue is originating. CloudWatch Logs provide detailed information, including error codes and service-specific messages.

Example:
```
‘ConnectionRefusedError: Unable to connect to RDS instance at 'db-instance-name'.’
```
This error typically indicates that there is an issue with your security group settings or the RDS instance is not running.

**Documenting AWS Service Errors**:
- Capture **CloudWatch Logs** that show the error details.
- Include the **AWS Resource** involved (e.g., EC2 instance ID, RDS instance endpoint).
- Provide the **error message** or code that AWS has logged.
- If applicable, share any **configuration files** (e.g., CloudFormation templates, security group settings).

---

### **IAM and Permissions Errors**

AWS Identity and Access Management (IAM) issues are common and can lead to access-related errors in various services like S3, EC2, or Lambda.

**Example IAM Error**

If an EC2 instance or Lambda function does not have sufficient permissions to access a resource, you might see an error like:
```
‘AccessDeniedException: User does not have permission to perform action on resource.’
```

This error is indicative of an **IAM permission** issue.

**Documenting IAM Errors**:
- **Capture the error message** from CloudWatch or the AWS Console that indicates an access issue.
- **Include the IAM role** or user involved and any relevant **permissions** or policies.
- **Screenshot or provide configuration details** of the IAM policy or role settings that are causing the issue.
- **Log the AWS service** that is failing (e.g., EC2, Lambda, S3) and the resource the service is attempting to access.

---

### **Networking and Connectivity Issues**

Many issues in Cloud Engineering are related to **networking**—for instance, issues with VPC, subnets, or security groups can prevent communication between services.

**Example VPC Error**

A common error might look like:
```
‘TimeoutError: Unable to connect to the database instance due to security group misconfiguration.’
```

This indicates that the **security group** or **VPC settings** are incorrectly configured, preventing resources from communicating.

**Documenting Networking Errors**:
- **Identify the services** involved (e.g., EC2, RDS, Lambda).
- **Capture the error message** that indicates connectivity failure (e.g., timeout, access denial).
- **Screenshot or provide CloudFormation** or **VPC configurations** (subnet settings, route tables, security groups).
- **Ensure the proper ports** are open in security groups for the services to communicate.

---

### **Database Errors in AWS (RDS, DynamoDB, etc.)**

Issues related to databases like **RDS**, **DynamoDB**, or **Aurora** can also occur due to misconfigurations or access problems.

**Example RDS Error**

An RDS error might look like:
```
‘DatabaseInstanceNotFound: The specified RDS instance does not exist or is not available.’
```

This can happen if the instance is incorrectly named or the connection string is misconfigured.

**Documenting Database Errors**:
- **Capture the error message** from CloudWatch or the AWS Console that indicates the issue.
- **Provide the RDS instance ID** or **DynamoDB table name** involved in the error.
- **Include connection string** or configuration details that may be incorrect (e.g., incorrect endpoint or credentials).
- **Check VPC/subnet settings** if the issue is connectivity-related.

---

### **Lambda Errors**

AWS Lambda functions can fail for a variety of reasons, such as permission issues, missing environment variables, or timeout errors.

**Example Lambda Error**

An error in Lambda might look like:
```
‘Task timed out after 60.00 seconds.’
```

This indicates that the function’s execution time exceeded the defined timeout.

**Documenting Lambda Errors**:
- **Capture the error message** from CloudWatch Logs related to the Lambda function.
- **Provide the function name** and **execution logs**.
- Include **configuration details**, such as **timeout settings**, **IAM roles**, or **environment variables**.

---

### **General Debugging Checklist for Cloud Engineering (AWS)**

When debugging errors in AWS, follow this checklist to ensure thorough documentation and troubleshooting:

- [ ] **Check CloudWatch Logs**: For detailed error logs across all services (EC2, Lambda, RDS, etc.).
- [ ] **Identify IAM Permission Issues**: Review IAM roles and policies that might cause access issues.
- [ ] **Verify Resource Configurations**: Ensure EC2 instances, RDS, S3 buckets, etc., are properly configured and accessible.
- [ ] **Check Security Group Settings**: Ensure correct security group settings, VPC configurations, and subnet routing.
- [ ] **Examine CloudFormation or Terraform Scripts**: Ensure infrastructure as code is correctly set up.
- [ ] **Check AWS Service Limits**: Verify that you are within AWS service limits (e.g., Lambda execution time, EC2 storage).
- [ ] **Check Environment Variables**: Ensure all necessary environment variables are set correctly for your application (e.g., AWS access keys, database URLs).
- [ ] **Check Network Setup**: Ensure that VPC, subnets, and routing are set up properly for service communication.
- [ ] **Reproduce the Error in Isolation**: Try to reproduce the issue in a controlled environment to isolate the cause.
- [ ] **Provide Detailed Error Information**: Share error messages, CloudWatch logs, and configuration files to assist others in troubleshooting.