# Assignment: Static Website on Amazon S3

## Objective:
The objective of this assignment is to give hands-on experience in setting up and configuring a static website on Amazon S3. By the end of this assignment, you should be able to create an S3 bucket, configure it for static website hosting, manage public access settings, and upload your web content.

## Task Overview:
You are required to follow the steps below to configure a static website on Amazon S3. This assignment will guide you through the process of creating an S3 bucket, enabling static website hosting, setting permissions, and testing your website.

## Assignment Steps:

### 1: Create a Bucket

1. Sign in to the [AWS Management Console](https://console.aws.amazon.com/s3/).
2. In the S3 console, click on **Create bucket**.
3. Enter a bucket name (e.g., `example.com`).
4. Choose a Region that is geographically close to you for reduced latency.
5. Accept the default settings and click **Create**.

### 2: Enable Static Website Hosting

1. In the S3 console, select the bucket you created.
2. Go to **Properties**.
3. Under **Static website hosting**, click **Edit**.
4. Select **Use this bucket to host a website**.
5. Enter `index.html` as the **Index document** name.
6. Optionally, enter `404.html` as the **Error document** name.
7. Click **Save changes**.

### 3: Edit Block Public Access Settings

1. In the S3 console, select your bucket and go to **Permissions**.
2. Under **Block public access (bucket settings)**, click **Edit**.
3. Uncheck **Block all public access** and confirm by clicking **Save changes**.

> **Note:** Disabling Block Public Access allows anyone on the internet to access your bucket. Proceed only if you understand the risks.

### 4: Add a Bucket Policy to Make Your Bucket Publicly Accessible

1. In the S3 console, under **Permissions**, go to **Bucket Policy** and click **Edit**.
2. Copy and paste the following bucket policy:
    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "PublicReadGetObject",
                "Effect": "Allow",
                "Principal": "*",
                "Action": "s3:GetObject",
                "Resource": "arn:aws:s3:::Bucket-Name/*"
            }
        ]
    }
    ```
3. Replace `Bucket-Name` with your bucket name.
4. Click **Save changes**.

### 5: Configure an Index Document

1. Create an `index.html` file with the following content:
    ```html
    <html>
    <head>
        <title>My Website Home Page</title>
    </head>
    <body>
      <h1>Welcome to my website</h1>
      <p>Now hosted on Amazon S3!</p>
    </body>
    </html>
    ```
2. Upload the `index.html` file to your S3 bucket using the **Upload** option in the S3 console.

### 6: Configure an Error Document

1. Create a `404.html` file with your custom error message.
2. Upload the `404.html` file to your S3 bucket.

### 7: Test Your Website Endpoint

1. In the S3 console, go to **Properties** for your bucket.
2. Under **Static website hosting**, copy the **Endpoint** URL and open it in your web browser.
3. Verify that your website is displayed.

### 8: Clean Up (Optional)

If this setup was for learning purposes only, delete the S3 bucket and its contents to avoid incurring charges. You can do this by selecting the bucket and choosing the **Delete bucket** option.

## Submission Instructions:

1. Provide screenshots showing:
   - The created bucket and its settings.
   - The uploaded index.html and 404.html files.
   - The website endpoint displaying your hosted content.
   
2. Write a brief summary of your experience setting up the static website.

3. (Optional) If you wish, share the public URL of your hosted website.
