# **Step-by-Step Guide: Deploying a Web Application with AWS Elastic Beanstalk**

## **Overview**
This guide will walk through deploying a simple web application using AWS Elastic Beanstalk with the **EB CLI** (Elastic Beanstalk Command Line Interface).

---

## **Prerequisites**

Before starting, ensure you have:

- An active AWS account
- [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html) installed and configured (`aws configure`)
- [EB CLI](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install.html) installed
- Python and `pip` installed (for installing EB CLI)
- A basic web app (e.g., Python Flask, Node.js)

---

## **Step 1: Install EB CLI**

If not already installed:

```bash
pip install awsebcli --upgrade --user
```

Ensure your PATH includes the user-level Python `bin` directory:

```bash
export PATH=~/.local/bin:$PATH
```

Verify installation:

```bash
eb --version
```

---

## **Step 2: Prepare a Simple App**

We'll use a basic **Flask** app as an example.

Create a directory:

```bash
mkdir beanstalk-demo && cd beanstalk-demo
```

Create `application.py`:

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello():
    return "Hello from Elastic Beanstalk!"
```

Create `requirements.txt`:

```
Flask==2.3.3
```

Create `Procfile` (no extension):

```
web: python application.py
```

This tells Elastic Beanstalk how to run your app.

---

## **Step 3: Initialize Elastic Beanstalk Project**

Initialize your EB project:

```bash
eb init
```

Follow the prompts:
- Select your AWS region
- Select or create an application name
- Choose platform (e.g., **Python**)
- Select default settings (yes to CodeCommit if prompted is optional)

---

## **Step 4: Create and Launch Environment**

Create and launch a new environment:

```bash
eb create beanstalk-env
```

- Choose **Web Server Environment**
- Accept defaults or customize (e.g., instance type, key pair, etc.)

This step will:
- Provision EC2, Load Balancer, Auto Scaling Group, and S3 bucket
- Deploy your app

Wait until the environment is ready.

---

## **Step 5: Open the Application**

Once deployed, open your app:

```bash
eb open
```

It will launch the URL of your Elastic Beanstalk environment in your browser.

You should see:

```
Hello from Elastic Beanstalk!
```

---

## **Step 6: View Logs (Optional)**

To retrieve logs:

```bash
eb logs
```

To tail logs in real-time:

```bash
eb logs --stream
```

---

## **Step 7: Monitor and Manage**

You can monitor:
- **Environment health**: `eb health`
- **Dashboard**: Go to AWS Console → Elastic Beanstalk → Your App

You can also:
- **Update the app**: Modify `application.py` and run `eb deploy`
- **Change settings**: Use `eb config`
- **Scale manually**: `eb scale <number-of-instances>`

---

## **Step 8: Clean Up Resources**

To avoid ongoing charges:

```bash
eb terminate beanstalk-env
```

Confirm when prompted.

---

## **Summary**

You’ve just:

- Installed the EB CLI
- Created and deployed a Python web app
- Launched it via Elastic Beanstalk
- Monitored and managed the environment