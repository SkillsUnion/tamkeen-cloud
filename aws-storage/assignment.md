# Assignment: Create an S3 Bucket and Upload an Object using the AWS CLI

## Objective:
The objective of this assignment is to provide hands-on experience with Amazon S3 using the AWS Command Line Interface (CLI). You will create a bucket, upload a file (object), and manage it using AWS CLI commands. By the end of this task, you should be familiar with basic S3 operations using the CLI.

## Prerequisites:
1. Ensure the AWS CLI is installed on your system. If not, follow the [AWS CLI Installation Guide](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html).
2. Configure your AWS CLI by running the command `aws configure` and entering your AWS credentials (access key, secret key, region, and output format).

## Task Overview:
You are required to create an S3 bucket and upload a file using the AWS CLI. Follow the steps below to complete the assignment.

### Step 1: Create a New S3 Bucket

1. Open your terminal or command prompt.
2. Run the following command to create a new bucket:
   ```bash
   aws s3 mb s3://my-unique-bucket-name-[your initials]
   ```
   Replace `my-unique-bucket-name-[your initials]` with a globally unique name for your bucket. 

### Step 2: Upload an Object to the S3 Bucket

1. Choose a file from your local system (e.g., `example.txt`) and upload it to your S3 bucket using the command:
   ```bash
   aws s3 cp /path/to/your/file.txt s3://my-unique-bucket-name-[your initials]/
   ```
   Replace `/path/to/your/file.txt` with the path to your file and ensure the bucket name matches the one you created.

### Step 3: List the Objects in Your Bucket

1. Verify that the object was successfully uploaded by listing the objects in your bucket:
   ```bash
   aws s3 ls s3://my-unique-bucket-name-[your initials]/
   ```

### Step 4: Make the Object Publicly Accessible (Optional)

1. If you want the object to be publicly accessible, run the following command:
   ```bash
   aws s3api put-object-acl --bucket my-unique-bucket-name-[your initials] --key file.txt --acl public-read
   ```
   Replace `file.txt` with your object’s key name.

2. Verify that you can access the file in a web browser using the URL:
   ```
   https://my-unique-bucket-name-[your initials].s3.amazonaws.com/file.txt
   ```

### Step 5: Clean Up Resources

1. After completing the assignment, delete the object from the bucket:
   ```bash
   aws s3 rm s3://my-unique-bucket-name-[your initials]/file.txt
   ```

2. Delete the bucket to avoid incurring costs:
   ```bash
   aws s3 rb s3://my-unique-bucket-name-[your initials] --force
   ```

## Submission Instructions:
1. Provide screenshots showing:
   - The command used to create the bucket.
   - The command used to upload the object.
   - The output from listing the objects in the bucket.
2. Include the bucket name and a brief description of the file you uploaded.
3. (Optional) If you made the file public, include the URL to the file.
