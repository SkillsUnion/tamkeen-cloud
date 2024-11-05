# Create an Administrative User in IAM Identity Center

> **Note**  
> If multi-factor authentication (MFA) for the root user was not activated, please try to complete Activate MFA for your AWS account root user before proceeding.

After completing Set up a New AWS Account, follow these steps to set up AWS account access for an administrative user, which will be used for daily tasks.

## 1: Enable IAM Identity Center

To enable IAM Identity Center:

1. Sign in to the AWS Management Console as the account owner by choosing **Root user** and entering the AWS account email address. On the next page, enter the password.
2. Open the IAM Identity Center console.
3. Under **Enable IAM Identity Center**, choose **Enable**.
4. IAM Identity Center requires AWS Organizations. If an organization has not been set up, choose whether to have AWS create one by selecting **Create AWS organization**.

   AWS Organizations automatically sends a verification email to the email address associated with the management account. There might be a delay before the verification email is received. Be sure to verify the email address within 24 hours.

## 2: Choose Your Identity Source

The identity source in IAM Identity Center defines where users and groups are managed. One of the following can be chosen as the identity source:

- **IAM Identity Center Directory**: When IAM Identity Center is enabled for the first time, it is automatically configured with an IAM Identity Center directory as the default identity source, where users and groups are created and assigned access levels.
- **Active Directory**: This option is selected if users are managed in either an AWS Managed Microsoft AD directory or a self-managed directory in Active Directory (AD).
- **External Identity Provider (IdP)**: This option is chosen if users are managed in an external identity provider such as Okta or Azure Active Directory.

Once IAM Identity Center is enabled, the identity source must be chosen. The selected identity source determines where IAM Identity Center searches for users and groups that need single sign-on (SSO) access. After the identity source is chosen, a user is created or specified and administrative permissions are assigned.

## Synchronize an Administrative User into IAM Identity Center

After connecting a directory to IAM Identity Center, specify a user for administrative permissions, then synchronize that user into IAM Identity Center:

1. Open the IAM Identity Center console.
2. Choose **Settings**.
3. On the **Settings** page, select the **Identity source** tab, choose **Actions**, and then select **Manage Sync**.
4. On the **Manage Sync** page, choose the **Users** tab, and then select **Add users and groups**.
5. Under **User**, enter the exact username and choose **Add**.
6. Under **Added Users and Groups**, confirm the user to be granted administrative permissions, select the checkbox next to the username, and choose **Submit**.
7. On the **Manage Sync** page, the specified user should appear in the **Users in sync scope** list.
8. In the navigation pane, choose **Users**.
9. On the **Users** page, it might take some time for the specified user to appear. Refresh the user list by choosing the refresh icon.

At this point, the user does not yet have access to the management account. Administrative access will be set up by creating a permission set and assigning the user to it.

## Use the Default Directory and Create a User in IAM Identity Center

When IAM Identity Center is first enabled, it is configured with an IAM Identity Center directory as the default identity source. Follow these steps to create a user in IAM Identity Center:

1. Sign in to the AWS Management Console as the account owner by choosing **Root user** and entering the AWS account email address. On the next page, enter the password.
2. Open the IAM Identity Center console.
3. Follow the steps in <a href="https://docs.aws.amazon.com/singlesignon/latest/userguide/addusers.html" target="_blank">Add users</a> to create a user.

   When specifying user details, the default option to send an email with password setup instructions can be used, or a one-time password can be generated. Ensure the email address specified is accessible.

4. After adding the user, return to this procedure. If the default option to send password setup instructions via email was used:

   - An email with the subject "Invitation to join AWS Single Sign-On" will be received. Open the email and choose **Accept invitation**.
   - On the New user sign-up page, enter and confirm a password, then choose **Set new password**.

At this point, the user does not yet have access to the management account. Administrative access will be set up by creating a permission set and assigning the user to it.

## 3: Create an Administrative Permission Set

Permission sets in IAM Identity Center define the level of access users and groups have to an AWS account. Follow these steps to create a permission set with administrative permissions:

1. Sign in to the AWS Management Console as the account owner by choosing **Root user** and entering the AWS account email address. On the next page, enter the password.
2. Open the IAM Identity Center console.
3. In the IAM Identity Center navigation pane, under **Multi-account permissions**, choose **Permission sets**.
4. Choose **Create permission set**.
5. For **1: Select permission set type**, keep the default settings and choose **Next**. The default settings grant full access to AWS services and resources using the `AdministratorAccess` predefined permission set.
6. For **2: Specify permission set details**, keep the default settings and choose **Next**. The default session duration is set to one hour.
7. For **3: Review and create**, do the following:

   - Review the permission set type and confirm that it is `AdministratorAccess`.
   - Review the AWS managed policy and confirm that it is `AdministratorAccess`.
   - Choose **Create**.

## 4: Set up AWS Account Access for an Administrative User

To set up AWS account access for an administrative user in IAM Identity Center, assign the user to the `AdministratorAccess` permission set:

1. Sign in to the AWS Management Console as the account owner by choosing **Root user** and entering the AWS account email address. On the next page, enter the password.
2. Open the IAM Identity Center console.
3. In the navigation pane, under **Multi-account permissions**, choose **AWS accounts**.
4. On the AWS accounts page, select the checkbox next to the AWS account for which administrative access is being assigned. If multiple accounts are in the organization, select the checkbox next to the management account.
5. Choose **Assign users or groups**.
6. For **1: Select users and groups**, on the **Assign users and groups to "AWS-account-name"** page:

   - On the **Users** tab, select the user to be granted administrative permissions. Use the search box to filter results if needed.
   - Confirm the correct user is selected, then choose **Next**.

7. For **2: Select permission sets**, on the **Assign permission sets to "AWS-account-name"** page, under **Permission sets**, select the `AdministratorAccess` permission set.
8. Choose **Next**.
9. For **3: Review and Submit**, on the **Review and submit assignments to "AWS-account-name"** page:

   - Review the selected user and permission set.
   - Confirm the correct user is assigned to the `AdministratorAccess` permission set, then choose **Submit**.

If either of the following applies, follow the steps in <a href="https://docs.aws.amazon.com/singlesignon/latest/userguide/mfa-enable-how-to.html" target="_blank">Enable MFA</a> to enable MFA for IAM Identity Center:

- The default Identity Center directory is being used as the identity source.
- An AWS Managed Microsoft AD directory or self-managed directory in Active Directory is being used, and RADIUS MFA is not enabled with AWS Directory Service.

When account access is set up for the administrative user, IAM Identity Center creates a corresponding IAM role in the relevant AWS account, with the policies specified in the permission set attached to the role.

## 5: Sign in to the AWS Access Portal with Administrative Credentials

Complete these steps to confirm that sign-in to the AWS access portal is possible using the administrative user credentials and access to the AWS account is granted:

1. Sign in to the AWS Management Console as the account owner by choosing **Root user** and entering the AWS account email address. On the next page, enter the password.
2. Open the AWS IAM Identity Center console at <a href="https://console.aws.amazon.com/singlesignon/" target="_blank">https://console.aws.amazon.com/singlesignon/</a>.
3. In the navigation pane, choose **Dashboard**.
4. On the Dashboard page, under **Settings summary**, copy the AWS access portal URL.
5. Open a separate browser, paste the copied AWS access portal URL, and press **Enter**.
6. Sign in using one of the following:

   - If Active Directory or an external identity provider (IdP) is being used as the identity source, sign in using the credentials of the assigned user.
   - If the default IAM Identity Center directory is being used as the identity source, sign in using the username and password specified during user creation.

7. After signing in, an AWS account icon should appear in the portal.
8. Select the AWS account icon to view the account name, account ID, and associated email address.
9. Choose the account name to display the `AdministratorAccess` permission set, then select the **Management Console** link next to `AdministratorAccess`.

When signed in, the assigned permission set will be displayed as an available role in the AWS access portal. Since the user was assigned to the `AdministratorAccess` permission set, the role will appear in the AWS access portal as: `AdministratorAccess/username`.

10. If redirected to the AWS Management Console, the setup of administrative access to the AWS account was successful.

11. Switch to the browser used to sign into the AWS Management Console and sign out from the AWS account root user.

To allow other users to access accounts and applications, and to administer IAM Identity Center, create and assign permission sets only through IAM Identity Center.
