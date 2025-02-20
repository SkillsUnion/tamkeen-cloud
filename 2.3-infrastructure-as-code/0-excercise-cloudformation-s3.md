# **Creating a S3 Bucket with AWS CloudFormation Stack**

This guide provides a step-by-step tutorial on how to create a **simple AWS CloudFormation stack** that provisions an **Amazon S3 bucket**. The CloudFormation template will be written in YAML format and executed using the **AWS Management Console** and **AWS CLI**.

---

## **1. Prerequisites**
Before starting, ensure the following:
- **AWS Account**: You need an active AWS account.
- **AWS CLI Installed**: If using the CLI, install and configure the AWS CLI ([Installation Guide](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)).
- **IAM Permissions**: Ensure you have **CloudFormation** and **S3** permissions.

---

## **2. Creating a CloudFormation Template**
The CloudFormation template defines the AWS resources to be created. Below is a simple **YAML-based** CloudFormation template for an S3 bucket.

### **Step 1: Create a YAML File**
Save the following content as `s3-template.yaml`:

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: "CloudFormation template to create an S3 bucket"

Resources:
  MyS3Bucket:
    Type: "AWS::S3::Bucket"
    Properties:
      BucketName: "my-cloudformation-demo-bucket"
      
Outputs:
  BucketName:
    Description: "Name of the created S3 bucket"
    Value: !Ref MyS3Bucket
```

---

## **3. Deploying the CloudFormation Stack**

### **Using AWS Management Console**
1. **Log in to AWS Console**.
2. Navigate to **CloudFormation** service.
3. Click **Create Stack** → **With New Resources**.
4. Select **Upload a template file**, then upload `s3-template.yaml`.
5. Click **Next**.
6. **Specify Stack Name** (e.g., `MyS3Stack`).
7. Click **Next** and leave default settings.
8. **Review the configuration**, then click **Create Stack**.
9. Wait for the stack status to change to **CREATE_COMPLETE**.

---

### **Using AWS CLI**
1. Open a terminal and navigate to the location of your template file.
2. Run the following command to create the stack:

```sh
aws cloudformation create-stack --stack-name MyS3Stack --template-body file://s3-template.yaml
```

3. Check the stack creation progress:

```sh
aws cloudformation describe-stacks --stack-name MyS3Stack
```

4. Once complete, view the created S3 bucket:

```sh
aws s3 ls
```

---

## **4. Validating the Deployment**
- Navigate to **Amazon S3** in the AWS Console.
- Look for the **newly created bucket** under the **S3 Buckets** list.
- If using CLI, verify the bucket:

```sh
aws s3 ls | grep my-cloudformation-demo-bucket
```

---

## **5. Deleting the Stack**
To remove the resources and avoid unnecessary costs:

### **Using AWS Console**
1. Navigate to **CloudFormation**.
2. Select **MyS3Stack**.
3. Click **Delete** and confirm.

### **Using AWS CLI**
```sh
aws cloudformation delete-stack --stack-name MyS3Stack
```

Check deletion status:
```sh
aws cloudformation describe-stacks --stack-name MyS3Stack
```

---

## **6. Conclusion**
You have successfully created and deleted an AWS CloudFormation stack. This tutorial introduced **infrastructure as code (IaC)** principles by provisioning an **Amazon S3 bucket** using CloudFormation.

For more advanced use cases, consider adding:
- **IAM Policies** for bucket permissions.
- **Versioning and Logging** in S3 properties.
- **More AWS Resources** (EC2, RDS, Lambda, etc.).

For more details, visit the [AWS CloudFormation Documentation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html).