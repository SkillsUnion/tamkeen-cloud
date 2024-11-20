## Assignment: Create a Custom VPC with A Components in AWS

### Objective
The purpose of this assignment is to create a Virtual Private Cloud (VPC) in AWS with detailed configurations, including subnets, route tables, and security settings. You will also launch an EC2 instance within your newly created VPC.

---

### Instructions

#### 1. **Create a VPC**
- **Name of VPC:** `<your-name>-custom-vpc` (e.g., `john-custom-vpc`)
- **CIDR Range:** Select an appropriate range, such as `10.0.0.0/16`.

---

#### 2. **Create Subnets**
Create the following subnets within your VPC:

1. **Public Subnet 1**
   - **Name:** `<your-name>-custom-public-subnet-az1`
   - **CIDR Range:** Assign a valid CIDR block, such as `10.0.1.0/24`.
   - **Availability Zone:** Choose one, such as `us-east-1a`.

2. **Public Subnet 2**
   - **Name:** `<your-name>-custom-public-subnet-az2`
   - **CIDR Range:** Assign a valid CIDR block, such as `10.0.2.0/24`.
   - **Availability Zone:** Choose another, such as `us-east-1b`.

3. **Private Subnet 1**
   - **Name:** `<your-name>-custom-private-subnet-az1`
   - **CIDR Range:** Assign a valid CIDR block, such as `10.0.3.0/24`.
   - **Availability Zone:** Use the same as Public Subnet 1 (e.g., `us-east-1a`).

4. **Private Subnet 2**
   - **Name:** `<your-name>-custom-private-subnet-az2`
   - **CIDR Range:** Assign a valid CIDR block, such as `10.0.4.0/24`.
   - **Availability Zone:** Use the same as Public Subnet 2 (e.g., `us-east-1b`).

---

#### 3. **Create an Internet Gateway**
- **Name of Internet Gateway:** `<your-name>-custom-igw`
- Attach the Internet Gateway to your newly created VPC.

---

#### 4. **Set Up Route Tables**
Create the following route tables and associate them with the appropriate subnets:

1. **Public Route Table**
   - **Name:** `<your-name>-custom-public-rtb`
   - Add a route for `0.0.0.0/0` with the Internet Gateway as the target.
   - Associate this route table with both public subnets.

2. **Private Route Table 1**
   - **Name:** `<your-name>-custom-private-rtb-az1`
   - Associate this route table with Private Subnet 1.

3. **Private Route Table 2**
   - **Name:** `<your-name>-custom-private-rtb-az2`
   - Associate this route table with Private Subnet 2.

---

#### 5. **Create a Security Group**
- **Name of Security Group:** `<your-name>-custom-sg-allow-ssh-http-https`
- **Ingress Rules:**
  - Allow **HTTP** (port 80) from anywhere.
  - Allow **HTTPS** (port 443) from anywhere.
  - Allow **SSH** (port 22) from anywhere.
- **Egress Rules:**
  - Allow all protocols to any destination.

---

#### 6. **Launch an EC2 Instance**
- **AMI:** Use the Amazon Linux 2023 AMI.
- **Public IP:** Enable Public IP assignment for the instance.
- **VPC:** Use your newly created VPC.
- **Subnet:** Choose one of your public subnets (e.g., `<your-name>-custom-public-subnet-az1`).
- **Key Pair:** Use an existing key pair that you own.
- **Security Group:** Select the security group created in step 5.
- **Instance Type:** Use `t2.micro`.
- **Name of EC2 Instance:** `<your-name>-custom-ec2`

---

### Submission Requirements
After completing the assignment:
1. Provide screenshots of the configurations for each component:
   - VPC
   - Subnets
   - Internet Gateway
   - Route Tables
   - Security Group
   - EC2 Instance
2. Share the public IP of your EC2 instance and confirm that you can SSH into the instance.
