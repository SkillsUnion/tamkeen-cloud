# Creating IAM Users & Groups

This guide provides a step-by-step walkthrough for creating IAM users and groups, assigning permissions, and adding users to groups in the AWS Management Console.

## Prerequisites

- An AWS account with administrative access.
- Familiarity with the AWS Management Console.

## 1. Accessing the IAM Dashboard

1. Sign in to the [AWS Management Console](https://aws.amazon.com/console/) using an account with administrative privileges.
2. In the AWS Management Console, use the **Find Services** search box and enter "IAM".
3. Select **IAM** from the search results to open the IAM dashboard.

## 2. Creating an IAM User Group

1. In the left navigation pane, select **User groups**.
2. Click on the **Create group** button.
3. Provide a name for the user group (e.g., "Developers").
4. Attach the required policies to define the permissions for the group:
   - For this hands-on, select the **AdministratorAccess** policy (Note: In a production environment, follow the principle of least privilege and assign more specific permissions).
5. Click **Create group**.

## 3. Creating IAM Users

1. In the left navigation pane, select **Users**.
2. Click on the **Add users** button.
3. Enter a username for the new user (e.g., "JohnDoe").
4. Select the **AWS Management Console access** option if the user needs access to the console.
   - Set a custom password or allow the user to create one at first sign-in.
5. Optionally, enable **Require password reset** if you want the user to change their password upon first sign-in.
6. Click **Next: Permissions**.

## 4. Adding the User to a Group

1. On the **Set permissions** page, select **Add user to group**.
2. Choose the user group created in Step 2 (e.g., "Developers").
3. Click **Next: Tags**.

## 5. Adding Tags (Optional)

1. You can add tags (e.g., department, role) to the user for better organization and management.
2. Click **Next: Review**.

## 6. Reviewing and Creating the User

1. Review the user details and permissions.
2. Click **Create user**.
3. You will see a success message, and you can optionally download the user’s sign-in credentials (especially if the user is set to create their password at first sign-in).

## 7. Verifying the User Setup

1. Return to the **Users** section in the IAM dashboard.
2. Click on the username (e.g., "JohnDoe") to view the user details and verify that they have the correct group membership and permissions.

## 8. Testing User Sign-In

1. Share the AWS Management Console sign-in URL with the user, which can be found on the IAM dashboard.
2. The user should sign in using their username and password to verify they have the expected access.


You have now successfully created an IAM user group, added a user to the group, and granted permissions by associating the group with a policy.