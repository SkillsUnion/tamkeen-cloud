# Tutorial: Running `aws-nuke`

## Introduction

`aws-nuke` is a powerful tool designed to clean up and delete all resources in an AWS account. This is particularly useful when you want to reset or terminate all resources in an account quickly, such as in non-production environments or for sandbox accounts. 

⚠️ **Caution:** `aws-nuke` is destructive. Ensure you have proper permissions and understand the impact before proceeding.

---

## Prerequisites

1. **AWS Credentials**: Ensure you have an IAM user or role with permissions to delete all resources.
2. **AWS CLI Installed**: Verify the AWS CLI is installed and configured:
   ```bash
   aws --version
   ```
3. **Go Installed**: `aws-nuke` requires Go. Download it from [Go's official site](https://go.dev/).
4. **Access to Git**: Required to clone the `aws-nuke` repository.

---

## Step 1: Install `aws-nuke`

1. Clone the `aws-nuke` repository:
   ```bash
   git clone https://github.com/rebuy-de/aws-nuke.git
   ```
2. Navigate into the project directory:
   ```bash
   cd aws-nuke
   ```
3. Build the binary using Go:
   ```bash
   go build -o aws-nuke .
   ```
4. Verify the installation:
   ```bash
   ./aws-nuke version
   ```

---

## Step 2: Configure AWS Credentials

`aws-nuke` uses the credentials configured in your AWS CLI. Ensure your AWS CLI profile is set up correctly:

1. Check your default profile:
   ```bash
   aws configure
   ```
2. Alternatively, specify a profile explicitly:
   ```bash
   export AWS_PROFILE=<your-profile-name>
   ```

---

## Step 3: Create the `aws-nuke` Config File

1. Create a YAML configuration file named `config.yaml`:
   ```yaml
   regions:
     - "us-east-1"
     - "us-west-1"
     - "eu-west-1"
   account-blacklist:
     - "000000000000" # Add AWS account IDs to exclude
   accounts:
     "123456789012": # Replace with your AWS account ID
       filters:
         IAMUser:
           - "Administrator"
   ```
2. Replace the placeholders with actual values:
   - **Account ID**: Your AWS account ID.
   - **Filters**: Specify resources you want to exclude from deletion.

---

## Step 4: Run `aws-nuke`

1. **Dry Run**: Always start with a dry run to see what will be deleted:
   ```bash
   ./aws-nuke -c config.yaml --profile <your-profile-name> --no-dry-run=false
   ```
   - This lists all resources without deleting anything.

2. **Execute Deletion**: After verifying the dry run, run the actual command:
   ```bash
   ./aws-nuke -c config.yaml --profile <your-profile-name> --no-dry-run
   ```
   - Confirm the deletion when prompted.

---

## Step 5: Monitor and Verify

- Monitor the progress of the deletion process in the terminal.
- Use the AWS Management Console or CLI to verify that resources have been deleted.

---

## Notes and Best Practices

1. **Whitelist Critical Resources**: Use the `filters` section in the config to protect critical resources.
2. **Limit Regions**: Specify only the regions you want to clean up.
3. **Double-Check Configurations**: Mistakes in the config file can lead to unintended deletions.
4. **Automate with CI/CD**: For sandbox accounts, automate `aws-nuke` execution but restrict it with safeguards.

---

## Conclusion

`aws-nuke` is an effective way to clean AWS accounts but requires careful configuration and execution. Always test in non-critical accounts and use dry runs to understand its impact before running the tool in production-like environments.

