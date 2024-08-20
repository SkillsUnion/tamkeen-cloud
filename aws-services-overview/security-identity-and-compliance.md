# Security, Identity, and Compliance

## Amazon Cognito

### Overview
Amazon Cognito lets you add user sign-up, sign-in, and access control to your web and mobile apps quickly and easily. It supports scaling to millions of users and integrates with various identity providers like Apple, Facebook, Twitter, or Amazon, with SAML 2.0 identity solutions or your own identity system.

### Key Features
- Save data locally on users’ devices, enabling offline access.
- Synchronize data across users’ devices for a consistent app experience.
- Focus on app development while Amazon Cognito manages user management, authentication, and sync.

## Amazon Detective

### Overview
Amazon Detective simplifies security investigations by automatically collecting log data from AWS resources and using machine learning and analysis to visualize the relationships between resources over time.

### Key Features
- Analyzes trillions of events from data sources like VPC Flow Logs, AWS CloudTrail, and Amazon GuardDuty.
- Provides an interactive view for security investigations, helping you identify the root cause of security findings.

## Amazon GuardDuty

### Overview
Amazon GuardDuty is a threat detection service that continuously monitors for malicious activity and anomalous behavior across your AWS accounts, workloads, and data.

### Key Features
- Analyzes billions of events and uses threat intelligence feeds and machine learning to detect unauthorized activity.
- Delivers findings to the GuardDuty console, Amazon CloudWatch Events, and AWS Security Hub for easy integration and response.

## Amazon Inspector

### Overview
Amazon Inspector is an automated vulnerability management service that continuously scans AWS workloads for software vulnerabilities and network exposure.

### Key Features
- Scans Amazon EC2 instances and container images for known vulnerabilities.
- Provides contextualized risk scores to prioritize the most critical vulnerabilities.
- Integrated with AWS Systems Manager and Amazon Elastic Container Registry (ECR) for easier deployment.

## Amazon Macie

### Overview
Amazon Macie is a fully managed data security and privacy service that uses machine learning to discover sensitive data and monitor security across Amazon S3 environments.

### Key Features
- Detects sensitive data types like financial, health, and personally identifiable information (PII).
- Provides security evaluations of S3 buckets and alerts for potential risks.

## Amazon Security Lake

### Overview
Amazon Security Lake centralizes security data from AWS environments, SaaS providers, and on-premises sources into a purpose-built data lake in your AWS account.

### Key Features
- Automates the collection and management of security data.
- Converts ingested data into Apache Parquet format and the Open Cybersecurity Schema Framework (OCSF) for standardized analysis.

## Amazon Verified Permissions

### Overview
Amazon Verified Permissions is a scalable, fine-grained permissions management service that helps define and manage access control for custom applications.

### Key Features
- Uses the Cedar open-source policy language to define authorization models.
- Centralizes policy management for easier audits and compliance.

## AWS Artifact

### Overview
AWS Artifact is a central resource for compliance-related information, providing access to AWS security and compliance reports and agreements.

### Key Features
- Includes SOC reports, PCI reports, and compliance certifications.
- Provides access to agreements like the Business Associate Addendum (BAA) and Non-disclosure Agreement (NDA).

## AWS Audit Manager

### Overview
AWS Audit Manager helps you continuously audit your AWS usage to assess risk and compliance with industry standards and regulations.

### Key Features
- Automates evidence collection to reduce manual effort during audits.
- Provides prebuilt frameworks for common compliance standards like GDPR and PCI DSS.

## AWS Certificate Manager

### Overview
AWS Certificate Manager simplifies provisioning, managing, and deploying SSL/TLS certificates for AWS services and internal resources.

### Key Features
- Automatically renews certificates and handles deployment for services like Elastic Load Balancing and Amazon CloudFront.
- Allows the creation of private certificates for internal resources.

## AWS CloudHSM

### Overview
AWS CloudHSM provides a cloud-based hardware security module (HSM) for generating and managing your own encryption keys.

### Key Features
- FIPS 140-2 Level 3 validated HSMs.
- Fully managed service with automated scaling and high availability.

## AWS Directory Service

### Overview
AWS Directory Service for Microsoft Active Directory (AWS Managed Microsoft AD) provides managed Active Directory services in the AWS Cloud.

### Key Features
- Fully compatible with Microsoft Active Directory tools.
- Easily integrates with Amazon EC2, Amazon RDS, and AWS Enterprise IT applications.

## AWS Firewall Manager

### Overview
AWS Firewall Manager provides centralized security management and enforcement for firewall rules across multiple AWS accounts and applications.

### Key Features
- Automatically applies security policies to new applications and resources.
- Integrates with AWS Organizations for centralized policy management.

## AWS Identity and Access Management (IAM)

### Overview
AWS IAM helps you securely control access to AWS resources by managing permissions and roles for users and services.

### Key Features
- Granular access controls with permissions.
- Single sign-on (SSO) for managing multi-account access.

## AWS Key Management Service (KMS)

### Overview
AWS KMS helps you create and manage cryptographic keys and control their use across AWS services.

### Key Features
- FIPS 140-2 validated hardware security modules (HSMs).
- Integrated with AWS CloudTrail for logging key usage.

## AWS Network Firewall

### Overview
AWS Network Firewall is a managed service that provides network protection for Amazon VPCs with automatic scaling.

### Key Features
- Custom firewall rules and integrations with managed intelligence feeds.
- Features like intrusion prevention, web filtering, and stateful firewall policies.

## AWS Resource Access Manager (RAM)

### Overview
AWS RAM helps you securely share resources across AWS accounts without creating duplicates.

### Key Features
- Share resources like subnets, transit gateways, and more.
- Reduces operational overhead by managing shared resources in one place.

## AWS Secrets Manager

### Overview
AWS Secrets Manager helps manage and retrieve secrets like API keys and database credentials securely.

### Key Features
- Automates secret rotation and integrates with Amazon RDS, Redshift, and DocumentDB.
- Provides fine-grained access controls and audit trails.

## AWS Security Hub

### Overview
AWS Security Hub centralizes and automates security checks across your AWS accounts, aggregating findings from multiple services and partner products.

### Key Features
- Provides automated security best practice checks.
- Aggregates findings in a standardized format, improving overall security posture.

## AWS Shield

### Overview
AWS Shield is a managed Distributed Denial of Service (DDoS) protection service that safeguards web applications on AWS.

### Key Features
- AWS Shield Standard offers free protection against common DDoS attacks.
- AWS Shield Advanced provides enhanced protection, real-time visibility, and DDoS cost protection.

## AWS IAM Identity Center (SSO)

### Overview
AWS IAM Identity Center provides centralized management of SSO access to multiple AWS accounts and applications.

### Key Features
- Built-in integrations for popular business applications.
- Single sign-on access through a unified user portal.

## AWS WAF

### Overview
AWS WAF is a web application firewall that helps protect your web applications and APIs from common exploits.

### Key Features
- Managed Rules for addressing issues like OWASP Top 10 risks and bot traffic.
- Full-featured API for automation and management of security rules.

## AWS WAF Captcha

### Overview
AWS WAF Captcha helps block unwanted bot traffic by requiring users to complete challenges before accessing AWS WAF-protected resources.

### Key Features
- Configurable rules for applying CAPTCHA challenges based on specific traffic patterns.
- Includes an audio version and is designed to meet accessibility requirements.

