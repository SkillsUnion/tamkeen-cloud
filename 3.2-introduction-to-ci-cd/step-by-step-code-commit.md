# Hands-On: Working with AWS CodeCommit (Step-by-Step)

## **Objective**
Learn how to:
- Create a Git repository in AWS CodeCommit
- Clone the repository locally
- Commit and push changes
- View updates in the AWS Console

---

## ** Prerequisites**
Before starting, ensure the following:

- An **AWS account**
- **IAM user** with CodeCommit access and Git credentials
- **AWS CLI** installed and configured:  
  ```bash
  aws configure
  ```
- **Git installed**  
  [Install Git](https://git-scm.com/downloads)

---

## **Step 1: Set Up IAM User for Git Access**

1. Sign in to the [AWS IAM Console](https://console.aws.amazon.com/iam/)
2. Create or choose an **IAM user**
3. Attach the policy:  
   `AWSCodeCommitFullAccess` (for learning purposes)
4. Under **Security Credentials**, generate **HTTPS Git credentials for AWS CodeCommit**
5. Save the **username** and **password** provided – you’ll need them for Git operations.

---

## **Step 2: Create a Repository in AWS CodeCommit**

1. Go to the [AWS CodeCommit Console](https://console.aws.amazon.com/codecommit/)
2. Click **Create repository**
3. Enter:
   - **Repository name**: `my-first-codecommit-repo`
   - (Optional) **Description**: e.g., “Demo for AWS CodeCommit”
4. Click **Create**

---

## **Step 3: Clone the Repository Locally**

1. Copy the **HTTPS URL** of the repo (it will look like this):  
   `https://git-codecommit.<region>.amazonaws.com/v1/repos/my-first-codecommit-repo`

2. In your terminal:
   ```bash
   git clone https://git-codecommit.<region>.amazonaws.com/v1/repos/my-first-codecommit-repo
   cd my-first-codecommit-repo
   ```

3. When prompted, enter your **Git credentials** (from Step 1)

---

## **Step 4: Add Files and Push to CodeCommit**

1. Create a file:
   ```bash
   echo "# My First CodeCommit Repo" > README.md
   ```

2. Stage the file:
   ```bash
   git add README.md
   ```

3. Commit:
   ```bash
   git commit -m "Initial commit with README"
   ```

4. Push to AWS CodeCommit:
   ```bash
   git push origin main
   ```

   > **Note**: If `main` branch doesn't exist, rename your current branch:
   ```bash
   git branch -M main
   ```

---

## **Step 5: Verify Changes in AWS Console**

1. Go to your CodeCommit repository in the AWS Console
2. Open the **Code tab**
3. Confirm that `README.md` is now listed with the commit message.

---

## **🧹 (Optional) Step 6: Clean Up**

If you're done experimenting:
- Delete the repository from AWS Console
- Remove the local folder:
  ```bash
  cd ..
  rm -rf my-first-codecommit-repo
  ```

---

## You’ve Learned:

- How to configure Git access for AWS CodeCommit  
- How to create, clone, and work with repositories  
- How to push and view changes using Git and the AWS Console

---