# **Step-by-Step Activity: Working with Relational Databases on Amazon RDS using Terminal**

---

## **Objective:**
Set up a **Relational Database Management System (RDBMS)** on **Amazon RDS**, create a **MySQL database**, and perform **CRUD (Create, Read, Update, Delete)** operations using the **terminal**.

---

## **Prerequisites:**
1. An **active AWS account**.
2. **IAM permissions** to access **Amazon RDS**, **VPC**, and **EC2**.
3. **MySQL client** installed on your **local terminal**.
4. **Basic understanding** of **SQL** and **relational databases**.

---

## **1. Create a VPC for the Database**

### **Step 1:** Navigate to the **VPC Dashboard**
- Open the **AWS Management Console**.
- Search for and select **VPC**.

### **Step 2:** Create a **New VPC**
- Click on **Create VPC**.
- Choose **VPC only** and configure:
  - **Name tag:** `my-rds-vpc`
  - **IPv4 CIDR block:** `10.0.0.0/16`
  - **Tenancy:** **Default**
- Click **Create VPC**.

### **Step 3:** Create **Subnets**
- Go to **Subnets** > **Create subnet**.
- Add two subnets:
  - **Public Subnet:** Name: `my-public-subnet`, AZ: `us-east-1a`, CIDR: `10.0.1.0/24`.
  - **Private Subnet:** Name: `my-private-subnet`, AZ: `us-east-1b`, CIDR: `10.0.2.0/24`.

### **Step 4:** Create an **Internet Gateway (IGW)**
- Go to **Internet Gateways** > **Create internet gateway**.
  - Name: `my-rds-igw`
- Attach the **IGW** to `my-rds-vpc`.

### **Step 5:** Configure **Route Tables**
- Go to **Route Tables** > **Create route table**.
  - Name: `my-public-rt`, VPC: `my-rds-vpc`
- Add a **route** to allow internet access:
  - **Destination:** `0.0.0.0/0`, **Target:** `my-rds-igw`
- **Associate** `my-public-subnet` with `my-public-rt`.

---

## **2. Create a Security Group for RDS**

### **Step 1:** Navigate to **EC2 Dashboard**
- Open **Security Groups** > **Create security group**.
  - Name: `my-rds-sg`, VPC: `my-rds-vpc`

### **Step 2:** Configure **Inbound Rules**
- Add the following rules:
  - **MySQL/Aurora:** Port **3306**, Source: **Your IP** (`MyIP`).
  - **SSH:** Port **22**, Source: **Your IP**.
  - **HTTP:** Port **80**, Source: **0.0.0.0/0** (Optional).

### **Step 3:** Configure **Outbound Rules**
- Allow **All traffic**, **Destination:** `0.0.0.0/0`.

---

## **3. Launch a MySQL Database Instance on Amazon RDS**

### **Step 1:** Navigate to **Amazon RDS Dashboard**
- Select **Databases** > **Create database**.

### **Step 2:** Choose **Database Creation Method**
- Select **Standard create**.

### **Step 3:** Select **Database Engine**
- Choose **MySQL** as the **database engine**.
- Engine version: **MySQL 8.0**.

### **Step 4:** Configure **Database Settings**
- **DB instance identifier:** `my-mysql-db`.
- **Master username:** `admin`.
- **Master password:** Create a **strong password**.

### **Step 5:** Configure **Instance Size**
- **Instance type:** `db.t3.micro` (**Free Tier eligible**).

### **Step 6:** Configure **Storage**
- **Storage type:** `General Purpose (SSD)`.
- **Allocated storage:** `20 GB`.

### **Step 7:** Set up **Connectivity**
- **Virtual Private Cloud (VPC):** `my-rds-vpc`.
- **Subnet group:** `Choose default`.
- **Public access:** `Yes` (for testing purposes).
- **VPC security groups:** `Choose existing`, select `my-rds-sg`.

### **Step 8:** Additional Configuration
- **Database name:** `mydb`.
- **Backup retention period:** `7 days` (Optional).
- **Enable automatic backups:** `Yes`.

### **Step 9:** Launch the **Database Instance**
- Click **Create database** and wait for the **status** to change to **Available**.

---

## **4. Connect to the Database Using Terminal**

### **Step 1:** Retrieve the **Database Endpoint**
- Navigate to **Amazon RDS Dashboard** > **Databases**.
- Select **my-mysql-db**.
- Copy the **endpoint** (e.g., `my-mysql-db.xxxxxxx.us-east-1.rds.amazonaws.com`).

### **Step 2:** Connect via **Terminal**
- Open your **terminal** and **connect to the database** using the **MySQL client**:

```bash
mysql -h my-mysql-db.xxxxxxx.us-east-1.rds.amazonaws.com -P 3306 -u admin -p
```

- Enter the **password** when prompted.

---

## **5. Create a Sample Table and Perform CRUD Operations**

### **Step 1:** Create a **Database Table**
```sql
CREATE TABLE Employees (
    EmployeeID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(255) NOT NULL,
    Position VARCHAR(255),
    Salary DECIMAL(10, 2)
);
```

### **Step 2:** Insert **Sample Data**
```sql
INSERT INTO Employees (Name, Position, Salary) VALUES
('John Doe', 'Manager', 75000.00),
('Jane Smith', 'Developer', 60000.00),
('Mike Johnson', 'Analyst', 50000.00);
```

### **Step 3:** Query **Data from the Table**
```sql
SELECT * FROM Employees;
```

### **Step 4:** Update **Existing Data**
```sql
UPDATE Employees SET Salary = 80000 WHERE Name = 'John Doe';
```

### **Step 5:** Delete **Data from the Table**
```sql
DELETE FROM Employees WHERE Name = 'Mike Johnson';
```

---

## **6. Clean Up Resources**

### **Step 1:** Delete the **Database Instance**
- Navigate to **Amazon RDS Dashboard**.
- Select **my-mysql-db** > **Actions** > **Delete**.
- **Skip final snapshot** (for testing purposes).

### **Step 2:** Delete the **Security Group**
- Go to **EC2 Dashboard** > **Security Groups**.
- Select **my-rds-sg** > **Delete**.

### **Step 3:** Delete the **VPC**
- Navigate to **VPC Dashboard**.
- **Delete subnets**, **route tables**, **internet gateway**, and finally the **VPC**.

---

## **7. Conclusion**

By completing this activity, you have:

- **Set up a VPC and security group** for **RDS connectivity**.
- **Launched a MySQL database** instance using **Amazon RDS**.
- **Connected to the database** using the **terminal**.
- **Performed CRUD operations** using **SQL commands**.
- **Cleaned up resources** to avoid **unwanted charges**.

For more information on **Amazon RDS**, visit the [**AWS RDS Documentation**](https://docs.aws.amazon.com/rds/).