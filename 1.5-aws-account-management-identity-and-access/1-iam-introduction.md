# AWS Identity and Access Management (IAM)

## **Learning Objectives**

By the end of this module, participants will be able to:

1. **Understand the role of AWS Identity and Access Management (IAM)** in managing authentication and authorization for AWS resources.  
2. **Create and manage IAM identities**, including users, groups, and roles, to securely control access to AWS accounts.  
3. **Implement effective access management practices**, including defining detailed permissions and enforcing the principle of least privilege.

---

## Overview

AWS Identity and Access Management (IAM) is a web service that helps securely control access to AWS resources. With IAM, you can manage permissions that determine which AWS resources users can access. IAM provides the necessary infrastructure to control authentication (who can sign in) and authorization (what permissions they have) for your AWS accounts.

## Identities

When you create an AWS account, you start with one sign-in identity called the **AWS account root user**. This root user has complete access to all AWS services and resources in the account and is accessed using the email address and password associated with the account. 

> **Recommendation:** Do not use the root user for everyday tasks. Safeguard the root user credentials and use them only for tasks that require root privileges, such as account closure or billing. For a full list of tasks requiring root user credentials, refer to the [IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html).

### Setting Up Additional Identities

Use IAM to create additional identities such as administrators, analysts, and developers. These identities are granted access based on the permissions needed to perform their specific roles. By creating IAM users and groups, you can manage access in a granular manner.

## Access Management

### Authentication

Once a user is set up in IAM, they authenticate with AWS using their sign-in credentials. Authentication matches the credentials to a **principal** (an IAM user, federated user, IAM role, or application) trusted by the AWS account.

### Authorization

After successful authentication, the user requests access to resources. AWS grants or denies access based on the policies associated with the principal. For instance, when signing in and navigating the AWS Management Console, a request is made to access a service. The service then checks the policies associated with the identity, determining what level of access is permitted.

Authorization requests can originate from:
- **Principals within your AWS account**: Users or applications you directly manage.
- **Principals from other trusted AWS accounts**: When you allow access from another AWS account.

### Actions and Permissions

Once authorized, a principal can perform operations such as:
- Launching new Amazon EC2 instances.
- Modifying IAM group memberships.
- Deleting Amazon S3 buckets.

By setting up detailed permissions and policies, you can enforce least privilege, ensuring users only have the permissions they need to accomplish their tasks.

For more details on IAM features and best practices, consult the [AWS IAM Documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/).