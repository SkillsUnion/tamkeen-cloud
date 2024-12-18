# Tutorial: Running `aws-nuke` with GitHub Actions

## Introduction

`aws-nuke` is a powerful tool designed to clean up and delete all resources in an AWS account. It is especially useful for quickly resetting or terminating resources in **non-production environments** or **sandbox accounts**.

⚠️ **Caution:** `aws-nuke` is **destructive**. Always test with a dry run and understand the consequences before execution.

---

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Installing `aws-nuke`](#step-1-install-aws-nuke)
3. [Configuring AWS Credentials](#step-2-configure-aws-credentials)
4. [Creating the Config File](#step-3-create-the-aws-nuke-config-file)
5. [Running `aws-nuke`](#step-4-run-aws-nuke)
6. [Integration with GitHub Actions](#step-6-integrate-with-github-actions)
7. [Notes and Best Practices](#notes-and-best-practices)
8. [Conclusion](#conclusion)

---

## Prerequisites

1. **AWS Credentials**: IAM user or role with permissions to delete resources.
2. **AWS CLI Installed**: Verify with:
   ```bash
   aws --version
   ```
3. **Go Installed**: Download from [Go's official site](https://go.dev/).
4. **Access to Git**: To clone repositories.
5. **GitHub Secrets** (for GitHub Actions): Store `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` securely.

---

## Step 1: Install `aws-nuke`

1. Clone the `aws-nuke` repository:
   ```bash
   git clone https://github.com/rebuy-de/aws-nuke.git
   ```
2. Navigate to the project directory:
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

`aws-nuke` uses the AWS credentials configured via the CLI.

1. Configure credentials using the default profile:
   ```bash
   aws configure
   ```
2. Or explicitly specify a profile:
   ```bash
   export AWS_PROFILE=<your-profile-name>
   ```

---

## Step 3: Create the `aws-nuke` Config File

Create a YAML configuration file named `config.yaml`:

```yaml
regions:
  - "us-east-1"
  - "us-west-1"
  - "eu-west-1"
account-blacklist:
  - "000000000000" # AWS accounts to exclude
accounts:
  "123456789012": # Replace with your AWS account ID
    filters:
      IAMUser:
        - "Administrator"
```

Replace placeholders:
- **Account ID**: Your AWS account ID.
- **Filters**: Resources to exclude.

---

## Step 4: Run `aws-nuke`

1. **Dry Run**: Validate the resources to be deleted:
   ```bash
   ./aws-nuke -c config.yaml --profile <your-profile-name> --no-dry-run=false
   ```

2. **Execute Deletion**: Confirm resources and execute:
   ```bash
   ./aws-nuke -c config.yaml --profile <your-profile-name> --no-dry-run
   ```

---

## Step 5: Monitor and Verify

- Monitor the deletion in the terminal.
- Verify deletions in the AWS Console or using CLI.

---

## Step 6: Integrate with GitHub Actions

You can automate `aws-nuke` execution on a schedule using **GitHub Actions**.

### GitHub Actions Workflow

Create a GitHub Actions workflow file at `.github/workflows/aws-nuke.yml`:

```yaml
name: Run aws-nuke

on:
  schedule:
    - cron: '0 15 * * *' # 3 PM UTC (11 PM SGT)
  workflow_dispatch: # Manual trigger

jobs:
  aws_nuke_job:
    runs-on: ubuntu-latest
    container:
      image: delfrinando/aws-nuke:latest
      options: --user root

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v3

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v1
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ap-southeast-1

      - name: Verify `aws-nuke` Installation
        run: /usr/local/bin/aws-nuke --version

      - name: Run `aws-nuke`
        run: |
          /usr/local/bin/aws-nuke -c ${GITHUB_WORKSPACE}/nuke/config/config.yaml \
          --force --no-dry-run --force-sleep 3
```

### Key Points:
1. **Schedule**: Adjust the `cron` expression for your timing (e.g., `0 15 * * *` runs daily at 3 PM UTC).
2. **Manual Trigger**: Added `workflow_dispatch` for on-demand execution.
3. **Secrets**: Store `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` in GitHub Secrets.

---

## Notes and Best Practices

1. **Use Dry Runs**: Always perform a dry run before running in live accounts.
2. **Whitelist Critical Resources**: Use the `filters` section to exclude essential resources.
3. **Restrict Automation**: Add safeguards to prevent accidental deletions.
4. **Version Control Config**: Store the `config.yaml` in version control for auditability.

---

## Conclusion

`aws-nuke` is a robust tool for cleaning AWS accounts efficiently. By integrating it with GitHub Actions, you can automate cleanup tasks for sandbox or non-production environments on a defined schedule.

Always validate configurations and ensure proper safeguards are in place to avoid unintended deletions.