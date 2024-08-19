# Step 1: Sign Up for an AWS Account

1. Open [https://portal.aws.amazon.com/billing/signup](https://portal.aws.amazon.com/billing/signup).
2. Choose **Create an AWS Account**.

3. Enter the account information and then choose **Continue**.

   It is essential that the account information is entered correctly, especially the email address. If the email address is entered incorrectly, access to the account may not be possible.

4. Choose either **Personal** or **Professional**.

   The difference between these options lies only in the information requested. Both account types offer the same features and functions.

5. Enter company or personal information.

6. Read and accept the [AWS Customer Agreement](https://aws.amazon.com/agreement/).

7. Choose **Create Account and Continue**.

   At this point, an email message will be sent to confirm that the AWS account is ready for use. The account can be accessed using the email address and password provided during sign-up. However, AWS services cannot be used until the account activation process is complete.

8. On the Payment Information page, enter the payment method details. If a different address from the one used during account creation is preferred, choose **Use a new address** and enter the desired billing address.

9. Choose **Verify and Add**.

10. To verify the phone number, select the appropriate country or region code from the list and enter a phone number where a call can be received within the next few minutes. Complete the CAPTCHA code and submit.

11. The AWS automated verification system will call and provide a PIN. Enter the PIN using the phone and then choose **Continue**.

12. Select an AWS Support plan.

    For details on available plans, see [Compare AWS Support Plans](https://aws.amazon.com/premiumsupport/plans/).

A confirmation page will appear, indicating that the account is being activated. Activation typically takes a few minutes but can take up to 24 hours. During this time, sign-in to the new AWS account is possible, although the **Complete Sign Up** button may still be visible, which can be ignored.

AWS sends a confirmation email when the account activation is complete. It is recommended to check the inbox and spam folder for this email. Once the message is received, full access to all AWS services is granted.

# Step 2: Sign in as the Root User

When an AWS account is first created, it begins with one sign-in identity that has complete access to all AWS services and resources within the account. This identity is known as the AWS account root user and is accessed by signing in with the email address and password used during account creation.

> **Important**  
> It is strongly recommended not to use the root user for everyday tasks. Safeguard the root user credentials and use them only for tasks that can be performed exclusively by the root user. For the complete list of tasks requiring root user credentials, see [Tasks that require root user credentials](https://docs.aws.amazon.com/IAM/latest/UserGuide/root-user-tasks.html) in the IAM User Guide.

## To Sign In as the Root User

1. Open the AWS Management Console at [https://console.aws.amazon.com/](https://console.aws.amazon.com/).
2. If this browser has not been used previously to sign in, the main sign-in page will appear. If the account owner is signing in, they should select **Root user**, enter the email address associated with the account, and choose **Next**.
3. A security check may be prompted. Complete it to proceed. If unable to complete the security check, try listening to the audio or refreshing the characters.
4. Enter the password and choose **Sign in**.


> **Note**  
> If the root user has been previously signed in using this browser, the email address for the AWS account might be remembered.  
> If the IAM user has been signed in previously using this browser, the IAM user sign-in page may appear instead. To return to the main sign-in page, choose **Sign in using root user email**.


# Step 3: Activate MFA for the AWS Account Root User

To enhance the security of root user credentials, it is recommended to follow the security best practice of activating multi-factor authentication (MFA) for the AWS account. Since the root user has access to perform sensitive operations within the account, adding this extra layer of authentication provides better protection.

Multiple types of MFA are available. For instructions on activating MFA for the root user, see [Enabling MFA devices for users in AWS](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable.html) in the IAM User Guide.
