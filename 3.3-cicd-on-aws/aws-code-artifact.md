# AWS CodeArtifact

![alt text](image-2.png)

## 1. Introduction
AWS CodeArtifact is a fully managed artifact repository service that helps organizations securely store, publish, and share software packages used in application development. It supports a wide range of package managers and formats including npm, PyPI, Maven, NuGet, RubyGems, Cargo, and more.

CodeArtifact reduces the operational overhead of maintaining self-hosted artifact repositories, automatically scaling to meet demand and integrating securely with AWS IAM, VPCs, and KMS for fine-grained access control and encryption.


{% include youtube.html id="-CA7NjSvSj0" %}

## 2. Key Features and Benefits
- **Fully Managed**: No servers to manage or scale.
- **Multi-Format Support**: Single repository can host multiple package formats.
- **Upstream Repositories**: Pull packages from public sources like npmjs.com, Maven Central, or PyPI.
- **Secure and Compliant**: Integrates with IAM, supports encryption at rest and in transit.
- **Pay-As-You-Go**: Billed by storage and requests.
- **VPC and Private Access**: Can be accessed securely from VPC environments.
- **CLI and Console Access**: Manage repositories via AWS CLI, SDKs, or Management Console.

## 3. Core Concepts
### Domain
A domain is a logical grouping of repositories in CodeArtifact. It is used to apply access policies and encryption settings. Each repository belongs to one domain.

### Repository
A repository holds packages and their versions. It can be connected to upstream public repositories or other CodeArtifact repositories.

### Package
A package is a bundle of software and metadata. CodeArtifact supports multiple formats including npm, PyPI, Maven, and NuGet.

### Package Version
A specific version of a package, e.g., `lodash@4.17.21`. Includes associated assets.

### Asset
An asset is a file such as a `.tgz`, `.whl`, or `.jar` that belongs to a package version.

### Upstream Repository
A linked repository that allows sharing and consumption of packages across domains or from external sources like npmjs.

### Authorization Token
Temporary token used by package managers to authenticate against a CodeArtifact repository. Generated using the AWS CLI.

## 4. Getting Started Steps
1. Create a **domain**.
2. Create one or more **repositories** in the domain.
3. Connect your repository to an upstream (e.g., public npm).
4. Authenticate using AWS CLI to retrieve a token.
5. Configure your package manager (e.g., npm, pip) to use CodeArtifact.
6. Publish or consume packages.

## 5. Example: Setup for npm
### Create Domain and Repositories
```bash
aws codeartifact create-domain --domain my-domain
aws codeartifact create-repository --domain my-domain --repository npm-store
aws codeartifact associate-external-connection \
  --domain my-domain --repository npm-store \
  --external-connection public:npmjs
```

### Configure Upstream
```bash
aws codeartifact create-repository \
  --domain my-domain \
  --repository my-repo

aws codeartifact update-repository \
  --domain my-domain --repository my-repo \
  --upstreams repositoryName=npm-store
```

### Authenticate
```bash
aws codeartifact login --tool npm --repository my-repo \
  --domain my-domain --domain-owner 111122223333
```

### Install Packages
```bash
npm install lodash
```

### Publish Packages
```bash
npm publish
```

## 6. Authentication and Access Control
CodeArtifact uses temporary authentication tokens issued via AWS CLI or SDK. These tokens are required to interact with the repository via package managers like npm or pip.

```bash
aws codeartifact get-authorization-token \
  --domain my-domain --domain-owner 111122223333
```

Use IAM policies to control who can publish, consume, and manage packages.

Example IAM permissions:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["codeartifact:*"],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": "sts:GetServiceBearerToken",
      "Resource": "*",
      "Condition": {
        "StringEquals": {
          "sts:AWSServiceName": "codeartifact.amazonaws.com"
        }
      }
    }
  ]
}
```

## 7. Working with Python
### Authenticate pip or twine
```bash
aws codeartifact login --tool pip --repository my-repo \
  --domain my-domain --domain-owner 111122223333
```

### Install packages
```bash
pip install requests
```

### Publish packages
```bash
twine upload --repository codeartifact dist/*
```

## 8. Monitoring and Logging
- **CloudTrail**: Logs all API actions.
- **CloudWatch**: View request logs, access patterns.
- **EventBridge**: Trigger actions based on package or repo events.

## 9. Best Practices
- Use separate domains for production vs non-production.
- Set retention policies for cleanup.
- Use upstream repositories to reduce external dependencies.
- Restrict access using fine-grained IAM policies.
- Enable encryption using customer-managed KMS keys if needed.

## 10. Summary
AWS CodeArtifact provides a secure, scalable, and highly available way to manage software dependencies. It supports industry-standard package formats and tools, integrates seamlessly with AWS services like CodeBuild and CodePipeline, and ensures control and visibility over internal and external software components. Whether managing open-source libraries or private packages, CodeArtifact simplifies artifact management across the software development lifecycle.