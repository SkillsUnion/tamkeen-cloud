# Terminology

<a href="https://docs.aws.amazon.com/general/latest/gr/glos-chap.html" target="_blank">Common terminology</a> is used by Amazon Web Services (AWS) to describe the sign-in process. It is recommended that these terms be understood.

## Administrator

Referred to as an AWS account administrator or IAM administrator. Typically, an individual responsible for overseeing an AWS account is involved. Settings for the AWS account are established and implemented by administrators. IAM or IAM Identity Center users are created, and access credentials along with a sign-in URL are provided by the administrator.

## Account

An AWS account contains both resources and identities that have access to those resources. The account owner’s email address and password are associated with the account.

## Credentials

Credentials, also known as access credentials or security credentials, are the information provided to AWS for signing in and gaining access to AWS resources. Credentials may include an email address, username, password, account ID or alias, verification code, and a multi-factor authentication (MFA) code. The system uses credentials to determine who is making a request and whether the access should be granted. Typically, the access key ID and the secret access key are used for this purpose.

More information regarding credentials can be found in the document <a href="https://docs.aws.amazon.com/IAM/latest/UserGuide/security-creds.html" target="_blank">Understanding and Getting Your AWS Credentials</a>.

## Corporate Credentials

Corporate credentials are used when accessing corporate networks and resources, and they can be configured by a corporate administrator to be used for accessing an AWS account.

## Profile

When signing up for an AWS Builder ID, a profile is created. This profile includes contact information and the ability to manage multi-factor authentication (MFA) devices and active sessions. Details about privacy and data handling can also be found within the profile.

## User

A user within an account makes API calls to AWS products. Each user has a unique name and a distinct set of security credentials. These credentials are not shared and are independent from those associated with the account itself.

## Root User Credentials

The root user credentials allow sign-in to the AWS Management Console as the root user.

## Verification Code

A verification code is used to confirm identity during the sign-in process using MFA. Codes can be sent via text message or email, depending on the setup.

---

# AWS Users and Credentials

AWS credentials are specified when interacting with AWS to verify identity and access rights. Authentication and authorization of requests are handled using these credentials.

For example, if access to a protected file within Amazon Simple Storage Service (Amazon S3) is needed, appropriate credentials must be provided. Access will be denied if credentials do not permit it. However, credentials are not required to download files from publicly shared S3 buckets.

## Root User

Also referred to as the account owner or account root user, complete access is granted to all AWS services and resources. Upon account creation, a single sign-in identity is established, which has full control over the account.

## IAM Identity Center User

IAM Identity Center users access the AWS access portal through a specific URL provided by the administrator. If an IAM Identity Center user is created, an invitation email is sent with the sign-in details. IAM Identity Center users cannot access the AWS Management Console directly.

More details on IAM Identity Center are available in the <a href="https://docs.aws.amazon.com/singlesignon/latest/userguide/what-is.html" target="_blank">What is IAM Identity Center?</a> document.

## Federated Identity

A federated identity allows sign-in using an external identity provider (IdP) like Login with Amazon, Facebook, Google, or other OpenID Connect (OIDC)-compatible IdPs. Web identity federation provides an authentication token that can be exchanged for temporary credentials in AWS.

Instructions for <a href="https://docs.aws.amazon.com/signin/latest/userguide/federated-identity-overview.html" target="_blank">signing in as a federated identity</a> are available.

## IAM User

IAM users are created entities with specific permissions within an AWS account. Credentials include a username and password for signing into the AWS Management Console. Step-by-step instructions can be found in the <a href="https://docs.aws.amazon.com/IAM/latest/UserGuide/id.html" target="_blank">IAM User Guide</a>.

## AWS Builder ID User

An AWS Builder ID user is intended for accessing specific AWS services or tools. The user profile allows information to be viewed and updated.
