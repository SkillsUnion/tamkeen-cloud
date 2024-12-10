# Programme Methodology

## Flipped Classroom

This program adopts a flipped-classroom model where we expects students to review lectures and course materials before class, and spend class time clarifying concepts and completing exercises with the guidance of a section leader.

## How to unblock yourself

### General tips

This program recommends the following 3 steps to unblock ourselves when blocked on a problem.

1. Trace the error message. What could be causing this error message? If we address that and there is another error message, keep addressing until there are no more error messages. If you do not see an error message, find where it is and/or find a way to give yourself more clues, e.g. with `console.log` statements.
2. Google the error message and context, e.g. "PropTypes not defined React". Skim through Google results and dig deeper in results that seem more promising.
3. Ask your peers and section leader in your section Disco channel, sharing context about the problem and what you've learnt from Steps 1 and 2 above. Context will allow them to help you. We mostly uses mainstream technologies and our problems will not be overly difficult.

### How to use Google

Students will need to use Google as a resource to solve problems not explained in our curriculum. We will do our best to document the most common mistakes, but it would be impossible to document all. Professional SWEs spend most time finding answers on Google, and googling effectively may be your most important takeaway from program.

When searching on Google, generally search for a combination of your error message and relevant technology name. For example, "Uncaught TypeError: Cannot read properties of null JavaScript" (JavaScript is the technology in this example). This will allow Google to share results for the specific error we are seeing for the specific technology.

With experience you will know when you are on the right track. Often it takes multiple permutations of Google search keywords to find the answer we are looking for. The goal when reading documentation, Stack Overflow or forum answers is to find relevant information as quickly as possible without reading more than necessary.

### How to ask questions to get help

Always provide context with questions. Helpful context for technical questions can include:

1. What is the error message?
2. What do you think is the problem?
3. What have you learnt from debugging and googling?
4. What is the relevant code causing the problem?

Compare the following 3 questions. Notice how it becomes much easier to help someone the more context we have about their problem.

#### Question 1: No context

> "My code is not working. Please help!"

#### Question 2: Incomplete context

> "My code is not working. I'm getting the error "Uncaught TypeError: Cannot read properties of null (reading 'rank')". Please help!"

#### Question 3: Full context

> "I'm getting the error 'Uncaught TypeError: Cannot read properties of null (reading 'rank')' on line 3. On line 3 I'm accessing a property of object `card` from my card deck. Googling tells me that `card` must be `null`, but I am not sure why. I've attached the relevant code below. Any suggestions?"
>
> ```javascript
> const cardDeck = [null];
> const card = cardDeck[0];
> console.log(card.rank);
> ```


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