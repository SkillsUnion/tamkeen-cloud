# Capstone Project Brief
## Cloud Engineering Program
This capstone project is designed to help you apply and demonstrate the knowledge and skills you have acquired throughout the Cloud Engineering (AWS) program. It reflects real-world practices in cloud infrastructure deployment, automation, and operations using AWS services.

You may choose from two levels of difficulty—**Basic** or **Advanced**—based on your comfort level and experience. The project will span **two weeks**, during which instructors will be available to support you. There will be regular check-ins and a final presentation at the end of the project period.

You can choose to complete the project **individually** or in **groups**. Collaboration is encouraged through our learning platform or other communication tools to simulate teamwork in a professional cloud engineering environment.

> **Note**: This project is **optional and not graded**. However, completing it is highly recommended as it helps reinforce core concepts, strengthen your technical portfolio, and prepare you for real-world cloud engineering roles.

## Objectives
- Apply your cloud engineering skills to design and deploy a working AWS-based solution.
- Demonstrate proficiency with infrastructure-as-code, deployment pipelines, and cloud architecture design.
- Build a practical project to showcase in your professional portfolio.
<hr/>
## Project Tracks (Choose One)
### 1. Static Website Hosting with CI/CD

**Specifications:**
- Host a static website on Amazon S3
- Automate deployment using GitHub Actions or AWS CodePipeline
- Configure CloudFront for content delivery
- Optionally, set up a custom domain using Amazon Route 53

**Recommended Services:**
- Amazon S3, CloudFront
- GitHub Actions or AWS CodePipeline
- Amazon Route 53 (optional), IAM, CloudWatch
<hr/>
### 2. Containerized Application Deployment on ECS

**Specifications:**
- Containerize a simple application using Docker
- Push the container image to Amazon ECR
- Deploy the image using Amazon ECS with Fargate
- Automate build and deployment using CodePipeline
- 
**Recommended Services:**
- Docker, Amazon ECR, Amazon ECS (Fargate)
- AWS CodePipeline, IAM, CloudWatch Logs
- Source control via GitHub or AWS CodeCommit
<hr/>

### 3. Serverless API Deployment Using AWS SAM

**Specifications:**
- Build a serverless RESTful API using AWS Lambda, API Gateway, and DynamoDB
- Deploy infrastructure using AWS SAM CLI or Terraform
- Implement input validation, error handling, and logging
- Optionally, integrate authentication using Amazon Cognito

**Recommended Services:**
- AWS Lambda, API Gateway, DynamoDB
- AWS SAM / Terraform, CloudWatch
- IAM, Amazon Cognito (optional)
<hr/>
### 4. CI/CD Pipeline for Microservices Architecture

**Specifications:**
- Define and implement at least two services (e.g., user service and order service)
- Set up CI/CD pipelines using CodeCommit / GitHub, CodeBuild, and CodePipeline
- Deploy to ECS or Lambda
- Configure routing via API Gateway or Application Load Balancer
- Monitor logs and performance using CloudWatch

**Recommended Services:**
- CodeCommit / GitHub, CodeBuild, CodePipeline
- Amazon ECS / Lambda, API Gateway / ALB
- CloudWatch, IAM, Terraform / CloudFormation (optional)
<hr/>
## Submission Requirements
1. GitHub Repository Link – Include your source code, infrastructure configurations, and documentation.
2. Architecture Diagram – Provide a clear diagram (as an image or Markdown) explaining your solution.
3. Demonstration Evidence – Submit screenshots or a short video of the deployed system in action.
4. README File (optional but encouraged) with:
- Project overview and goals
- Step-by-step deployment guide
- Explanation of AWS services used

## Final Notes
You are encouraged to continue enhancing your project after the course concludes.
Where possible, utilize AWS Free Tier resources to minimize costs.
Refer to AWS documentation and course content to guide your implementation.
If you have questions or need support, please reach out to your instructors or use the discussion platforms provided.
