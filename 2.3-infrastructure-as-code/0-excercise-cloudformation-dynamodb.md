# **Creating a Simple AWS CloudFormation Stack for a DynamoDB Table**

This guide walks through **creating an Amazon DynamoDB table** using **AWS CloudFormation**. The CloudFormation template will define the table's attributes, primary key, and billing mode. The setup will be executed using both **AWS Management Console** and **AWS CLI**.

---

## **1. Prerequisites**
Before starting, ensure the following:
- **AWS Account**: You need an active AWS account.
- **AWS CLI Installed**: If using the CLI, install and configure the AWS CLI ([Installation Guide](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)).
- **IAM Permissions**: Ensure you have **CloudFormation** and **DynamoDB** permissions.
- **Basic Knowledge of DynamoDB**: Understanding **primary keys, attributes, and billing modes**.

---

## **2. Creating a CloudFormation Template**
A **CloudFormation template** defines the AWS resources to be created. Below is a simple **YAML-based** CloudFormation template to provision a **DynamoDB table**.

### **Step 1: Create a YAML File**
Save the following content as `dynamodb-template.yaml`:

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: "CloudFormation template to create a DynamoDB Table"

Resources:
  MyDynamoDBTable:
    Type: "AWS::DynamoDB::Table"
    Properties:
      TableName: "MyCloudFormationDynamoDBTable"
      AttributeDefinitions:
        - AttributeName: "ID"
          AttributeType: "S"
      KeySchema:
        - AttributeName: "ID"
          KeyType: "HASH"
      BillingMode: "PAY_PER_REQUEST"
      Tags:
        - Key: "Environment"
          Value: "Dev"

Outputs:
  TableName:
    Description: "DynamoDB Table Name"
    Value: !Ref MyDynamoDBTable
```

---

## **3. Deploying the CloudFormation Stack**
The CloudFormation stack will **create the DynamoDB table**.

### **Using AWS Management Console**
1. **Log in to AWS Console**.
2. Navigate to **CloudFormation** service.
3. Click **Create Stack** → **With New Resources**.
4. Select **Upload a template file**, then upload `dynamodb-template.yaml`.
5. Click **Next**.
6. **Specify Stack Name** (e.g., `MyDynamoDBStack`).
7. Click **Next**, leaving default settings.
8. **Review the configuration**, then click **Create Stack**.
9. Wait for the stack status to change to **CREATE_COMPLETE**.

---

### **Using AWS CLI**
1. Open a terminal and navigate to the location of your template file.
2. Run the following command to **create the stack**:

```sh
aws cloudformation create-stack --stack-name MyDynamoDBStack --template-body file://dynamodb-template.yaml
```

3. Check the stack creation progress:

```sh
aws cloudformation describe-stacks --stack-name MyDynamoDBStack
```

4. Once complete, verify the **DynamoDB table** using:

```sh
aws dynamodb list-tables
```

Expected output:
```sh
{
    "TableNames": [
        "MyCloudFormationDynamoDBTable"
    ]
}
```

---

## **4. Validating the Deployment**
- Navigate to **AWS Console** > **DynamoDB**.
- Click **Tables** and look for **MyCloudFormationDynamoDBTable**.
- Verify its **Primary Key (ID)** and **Billing Mode (PAY_PER_REQUEST)**.

If using CLI, run:
```sh
aws dynamodb describe-table --table-name MyCloudFormationDynamoDBTable
```

---

## **5. Deleting the Stack**
To **remove the resources** and avoid unnecessary costs:

### **Using AWS Console**
1. Navigate to **CloudFormation**.
2. Select **MyDynamoDBStack**.
3. Click **Delete** and confirm.

### **Using AWS CLI**
```sh
aws cloudformation delete-stack --stack-name MyDynamoDBStack
```

Check deletion status:
```sh
aws cloudformation describe-stacks --stack-name MyDynamoDBStack
```

---

## **6. Conclusion**
By following this guide, you have:
- Created a **DynamoDB table** using CloudFormation.  
- Used **AWS CLI** and **AWS Console** for deployment.  
- Verified the table creation and learned to delete CloudFormation stacks.

For further learning, visit the [AWS CloudFormation Documentation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html). 🚀