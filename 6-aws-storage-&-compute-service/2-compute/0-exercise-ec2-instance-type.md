# EC2 Step-by-Step

## 1. Launching an EC2 Instance

An EC2 instance can be launched using the AWS Management Console following the steps outlined below. This guide focuses on the essential steps to quickly launch an instance.

### Steps to Launch an Instance:

1. Open the [Amazon EC2 console](https://console.aws.amazon.com/ec2/).

2. In the navigation bar at the top, the current AWS Region is displayed (e.g., Ohio). The selected Region can be used, or optionally, a Region closer to the user can be selected.

3. From the EC2 console dashboard, in the **Launch instance** pane, select **Launch instance**.

4. Under **Name and tags**, enter a descriptive name for the instance under **Name**.

5. Under **Application and OS Images (Amazon Machine Image)**:
   - Select **Quick Start** and then choose the operating system (OS) for the instance. For a first Linux instance, **Amazon Linux** is recommended.
   - Choose an Amazon Machine Image (AMI) marked as **Free Tier eligible**.

6. Under **Instance type**, select **t2.micro**, which is eligible for the Free Tier. In Regions where **t2.micro** is not available, **t3.micro** is Free Tier eligible.

7. Under **Key pair (login)**, select an existing key pair or choose **Create new key pair** to create a first key pair.

   > **Warning:**  
   > Proceeding without a key pair is not recommended as it will prevent connection to the instance using the methods described in this tutorial.

8. Under **Network settings**, the default VPC is selected, along with the default subnet in an Availability Zone chosen automatically. A security group is also configured to allow connections from anywhere. For the first instance, it is recommended to use the default settings. Network settings can be updated as follows:
   - (Optional) To use a specific default subnet, select **Edit** and choose a subnet.
   - (Optional) To use a different VPC, select **Edit** and choose an existing VPC. If the VPC isn't configured for public internet access, connecting to the instance will not be possible.
   - (Optional) To restrict inbound connection traffic to a specific network, choose **Custom** instead of **Anywhere** and enter the CIDR block for the network.
   - (Optional) To use a different security group, select **Select existing security group** and choose an existing group. Ensure the security group allows SSH traffic for Linux instances or RDP traffic for Windows instances.

9. Under **Configure storage**, a root volume is configured but no data volumes are added. This is sufficient for testing purposes.

10. Review the instance configuration summary in the **Summary** panel, and when ready, select **Launch instance**.

11. If the launch is successful, select the instance ID from the success notification to open the **Instances** page and monitor the launch status.

12. Select the checkbox for the instance. The initial instance state will be **pending**. Once the instance starts, its state will change to **running**. Choose the **Status checks** tab. Once the instance passes its status checks, it is ready to receive connection requests.

## 2. Connecting to the Instance

The connection method depends on the operating system of the instance.

### Connecting to Linux Instances:

1. Open the [Amazon EC2 console](https://console.aws.amazon.com/ec2/).
2. In the navigation pane, choose **Instances**.
3. Select the instance and choose **Connect**.
4. On the **Connect to instance** page, select the **SSH client** tab.
5. (Optional) If a key pair was created during the instance launch and the private key (`.pem` file) was downloaded to a Linux or macOS computer, run the `chmod` command to set permissions for the private key.
6. Copy the provided SSH command. For example:
   ```bash
   ssh -i key-pair-name.pem ec2-user@ec2-198-51-100-1.us-east-2.compute.amazonaws.com
   ```
   Replace `key-pair-name.pem` with the private key file name, `ec2-user` with the appropriate username, and the string after the `@` symbol with the instance's public DNS name.
7. In a terminal window, run the SSH command. If the private key file is not in the current directory, specify the fully-qualified path to the key file in the command.
8. When prompted, verify the instance's fingerprint by comparing it with the instance's system log output. Enter `yes` to continue connecting.

### Connecting to Windows Instances:

To connect to a Windows instance via Remote Desktop Protocol (RDP), the initial administrator password must be retrieved and entered when connecting to the instance. It may take a few minutes after the instance launch before this password becomes available.

The default username for the Administrator account varies depending on the operating system (OS) language in the AMI. To identify the correct username, match the AMI's OS language with the corresponding username. For example:
- English OS: `Administrator`

If the OS language does not have a corresponding username, use `Administrator (Other)`. For more information, refer to the Microsoft TechNet Wiki on Localized Names for Administrator Accounts in Windows.

1. Open the [Amazon EC2 console](https://console.aws.amazon.com/ec2/).
2. In the navigation pane, select **Instances**.
3. Choose the instance, then select **Connect**.
4. On the **Connect to instance** page, select the **RDP client** tab.
5. For **Username**, select the default username for the Administrator account, matching the language of the OS in the AMI. If no specific language username exists, select `Administrator (Other)`.
6. Choose **Get password**.
7. On the **Get Windows password** page:
   - Choose **Upload private key file** and navigate to the private key (`.pem`) file specified when the instance was launched. Select the file and choose **Open**.
   - Choose **Decrypt password**. The default administrator password will appear under **Password**.

8. Copy the password and store it securely. This password is needed to connect to the instance.

#### Connecting to a Windows Instance Using an RDP Client

1. On the **Connect to instance** page, choose **Download remote desktop file**. After the download completes, choose **Cancel** to return to the Instances page.
2. Run `mstsc.exe` to open the RDP client on Windows.
3. Expand **Show options**, then choose **Open** and select the `.rdp` file from the Downloads folder.
4. By default, **Computer** is set to the public IPv4 DNS name of the instance, and **User name** is the administrator account. To connect using IPv6, replace the public IPv4 DNS name with the instance's IPv6 address. Review and modify the settings as needed.
5. Choose **Connect**. If a warning about the remote connection's unknown publisher appears, choose **Connect** to proceed.
6. Enter the previously saved password and choose **OK**.

   - Due to the nature of self-signed certificates, a warning about the security certificate may appear. To proceed:
     - **Windows:** Compare the certificate thumbprint with the value in the system log to verify the remote computer's identity. Choose **View certificate** and compare the **Thumbprint** in the **Details** tab with the `RDPCERTIFICATE-THUMBPRINT` in **Actions > Monitor and troubleshoot > Get system log**.
     - **Mac OS X:** Compare the certificate fingerprint with the value in the system log. Choose **Show Certificate**, expand **Details**, and choose **SHA1 Fingerprints**. Compare this value with `RDPCERTIFICATE-THUMBPRINT` in **Actions > Monitor and troubleshoot > Get system log**.

7. If the RDP connection is successful, the RDP client will display the Windows login screen, followed by the Windows desktop. If an error message appears, consult the troubleshooting guide for remote desktop connection issues. When finished, close the RDP client.

## 3. Cleaning Up the Instance

After completing the tutorial, it is important to clean up by terminating the instance. Terminating an instance deletes it, preventing any future connections.

### Steps to Terminate the Instance:

1. In the navigation pane, choose **Instances**. In the list of instances, select the instance.
2. Choose **Instance state**, then **Terminate instance**.
3. Confirm the termination when prompted.

After termination, the instance status changes to **shutting down** and then **terminated**. The terminated instance remains visible in the console for a short time before being automatically deleted.

> **Important:**  
> Terminating an instance stops any further charges for that instance or usage against Free Tier limits. If the instance is to be kept without incurring charges, it can be stopped instead of terminated. For more information, see <a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Stop_Start.html" target="_blank">Stop and start Amazon EC2 instances</a>.
