# Prerequisites

Before the setup process is initiated, the account requirements should be reviewed, consideration should be given to whether multiple AWS accounts are needed, and an understanding of the requirements for setting up administrative access in IAM Identity Center is essential.

## AWS Account Requirements

To sign up for an AWS account, the following information must be provided:

- **Account Name**: The account name appears in several locations, such as invoices, the Billing and Cost Management dashboard, and the AWS Organizations console.

  It is recommended that an account naming standard be used so that the account name is easily recognized and distinguished from other accounts. For company accounts, a naming convention like `organization-purpose-environment` (e.g., `AnyCompany-audit-prod`) should be considered. For personal accounts, a naming convention such as `first name-last name-purpose` (e.g., `paulo-santos-testaccount`) is suggested.

- **Email Address**: This email address is used as the sign-in name for the account’s root user and is necessary for account recovery (e.g., resetting a password). It is important that messages sent to this email address can be received. Before certain tasks can be performed, verification that access to this email account is available may be required.

- **Phone Number**: This phone number may be required for account ownership confirmation, and it should be ensured that calls can be received at this number.

- **Multi-Factor Authentication (MFA) Device**: To enhance the security of AWS resources, multi-factor authentication (MFA) should be enabled for the root user account. In addition to regular sign-in credentials, secondary authentication is required when MFA is activated, providing an additional security layer. Further details regarding MFA can be found in the [IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html#id_credentials_mfa-what-is-mfa).

- **AWS Support Plan**: A support plan must be chosen during the account creation process. Information on the available plans can be found in the [Compare AWS Support Plans](https://aws.amazon.com/premiumsupport/plans/) documentation.


## AWS Organizations

### Management of AWS Accounts

An AWS account must be managed by AWS Organizations. If an organization has not been set up, there is no requirement to do so immediately. When IAM Identity Center is enabled, a choice will be provided to allow AWS to create an organization.

If AWS Organizations has already been set up, it is recommended to ensure that all features are enabled. For more information, see [Enabling all features in your organization](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_org_support-all-features.html) in the AWS Organizations User Guide.

To enable IAM Identity Center, signing in to the AWS Management Console using the credentials of the AWS Organizations management account is necessary. IAM Identity Center cannot be enabled while signed in with credentials from an AWS Organizations member account. For more information, see [Creating and managing an AWS Organization](http://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_org.html) in the AWS Organizations User Guide.

---

## IAM Roles

### Checking Quotas and Requesting Increases

If IAM roles have already been configured in an AWS account, it is advisable to check whether the account is approaching the quota for IAM roles. For more information, see [IAM Object Quotas](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_iam-quotas.html#reference_iam-quotas-entities).

If the quota is nearing its limit, a quota increase should be requested. Otherwise, issues might arise when provisioning permission sets in IAM Identity Center if accounts exceed the IAM role quota. For details on requesting a quota increase, see [Requesting a quota increase](https://docs.aws.amazon.com/servicequotas/latest/userguide/request-quota-increase.html) in the Service Quotas User Guide.

---

## Next-Generation Firewalls and Secure Web Gateways

### Adding Required Domains and URL Endpoints to Allow-Lists

If specific AWS domains or URL endpoints are filtered using a web content filtering solution like NGFWs or SWGs, the following domains or URL endpoints must be added to the web-content filtering solution’s allow-lists:

#### Specific DNS Domains
- `*.awsapps.com`
- `*.signin.aws`

#### Specific URL Endpoints
- `https://[yourdirectory].awsapps.com/start`
- `https://[yourdirectory].awsapps.com/login`
- `https://[yourregion].signin.aws/platform/login`

---

## Using Multiple AWS Accounts

### Importance of Isolation and Separation

AWS accounts serve as the primary security boundary in AWS. They provide a resource container that facilitates isolation, which is critical for establishing a secure, well-governed environment.

### Principles Supported by Separating Resources

Separating resources into distinct AWS accounts supports several key principles in cloud environments:

- **Security Control**: Different applications may have distinct security profiles that require unique control policies. For instance, auditing becomes easier when a single AWS account is pointed to that hosts all elements subject to PCI standards.
- **Isolation**: An AWS account acts as a unit of security protection. Potential risks and security threats should remain contained within an AWS account without affecting others.
- **Multiple Teams**: Different teams with varying responsibilities and resource needs can avoid interfering with one another by using separate AWS accounts.
- **Data Isolation**: Isolating data stores within an account helps limit access and manage sensitive information, aiding compliance with regulations such as GDPR.
- **Business Processes**: Different business units or products often require separate processes, which can be supported by having multiple AWS accounts.
- **Billing**: An account provides the only true method of separating costs at a billing level. Even with consolidated billing, separate line items are maintained by AWS account.
- **Quota Allocation**: AWS service quotas are enforced separately for each account, preventing workloads from consuming quotas designated for other accounts.

### Recommendations and Planning

The recommendations and procedures provided align with the AWS Well-Architected Framework, designed to help build a flexible, resilient, and scalable cloud infrastructure. Adherence to this guidance, even from the start, ensures scalability without compromising security.

Before creating multiple accounts, a management plan should be developed. It is recommended to use AWS Organizations, a free AWS service, to manage all accounts within an organization.

### AWS Control Tower

AWS also offers AWS Control Tower, which enhances automation in Organizations and integrates with other AWS services like AWS CloudTrail, AWS Config, Amazon CloudWatch, and AWS Service Catalog. These services may incur additional costs. For more information, see [AWS Control Tower Pricing](https://aws.amazon.com/controltower/pricing).
