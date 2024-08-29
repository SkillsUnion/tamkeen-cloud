# Assignment: Creating IAM Users & Groups

## Objective:
The purpose of this assignment is to familiarize yourself with managing IAM users and groups in the AWS Management Console. By the end of this task, you should be able to create IAM user groups, add users to groups, and assign permissions using IAM policies.

## Prerequisites:
- Access to an AWS account with administrative privileges.
- Basic familiarity with the AWS Management Console.

## Task Overview:
You are required to create an IAM user group, create a new IAM user, add the user to the group, and assign the necessary permissions. Follow the steps below to complete the assignment.

### Step 1: Access the IAM Dashboard

1. Sign in to the [AWS Management Console](https://aws.amazon.com/console/) using an administrative account.
2. In the AWS Management Console, use the **Find Services** search bar to search for "IAM".
3. Select **IAM** from the search results to open the IAM dashboard.

### Step 2: Create an IAM User Group

1. In the IAM dashboard, go to the left navigation pane and select **User groups**.
2. Click **Create group**.
3. Enter a name for the user group (e.g., "Developers").
4. Attach the **AdministratorAccess** policy (Note: In a real-world scenario, use the principle of least privilege and attach more specific permissions).
5. Click **Create group**.

### Step 3: Create an IAM User

1. In the left navigation pane, select **Users**.
2. Click **Add users**.
3. Enter a username (e.g., "JohnDoe").
4. Select **AWS Management Console access** if the user needs console access.
   - Set a custom password or allow the user to create one upon first sign-in.
5. (Optional) Enable **Require password reset** if you want the user to change their password on first sign-in.
6. Click **Next: Permissions**.

### Step 4: Add the User to the Group

1. On the **Set permissions** page, select **Add user to group**.
2. Choose the user group you created in Step 2 (e.g., "Developers").
3. Click **Next: Tags**.

### Step 5: Add Tags (Optional)

1. (Optional) Add tags for better organization and management (e.g., department, role).
2. Click **Next: Review**.

### Step 6: Review and Create the User

1. Review the user’s details and permissions.
2. Click **Create user**.
3. You will see a success message, and you can optionally download the user’s sign-in credentials, especially if the user is set to create their password upon first sign-in.

### Step 7: Verify the User Setup

1. Return to the **Users** section in the IAM dashboard.
2. Click on the username (e.g., "JohnDoe") to view the user details.
3. Verify that the user is added to the correct group and has the expected permissions.

### Step 8: Test User Sign-In

1. Share the AWS Management Console sign-in URL with the user, which can be found on the IAM dashboard.
2. The user should sign in using their username and password to verify they have the expected access.

## Submission Instructions:

1. Provide screenshots of the following:
   - The created user group and its attached policy.
   - The user creation steps, including group assignment.
   - The IAM dashboard showing the user’s details and group membership.

2. Write a brief summary of your experience setting up IAM users and groups, highlighting any challenges encountered.

3. (Optional) Include a step on how you would secure the IAM user with multi-factor authentication (MFA).