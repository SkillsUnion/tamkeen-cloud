# **Working with Non-Relational Databases on Amazon DynamoDB**

---

## **Objective:**
Set up a **Non-Relational Database (NoSQL)** using **Amazon DynamoDB**, create a **key-value store**, and perform **CRUD (Create, Read, Update, Delete)** operations using the **AWS Management Console**.

---

## **Prerequisites:**
1. An **active AWS account**.
2. **IAM permissions** to access **Amazon DynamoDB**, **IAM**, and **AWS Management Console**.
3. **Basic understanding** of **NoSQL databases** and **key-value data models**.

---

## **1. Set Up a DynamoDB Table**

### **Step 1:** Navigate to the **DynamoDB Console**
- Open the **AWS Management Console**.
- Search for and select **DynamoDB**.

### **Step 2:** Create a **New Table**
- Click on **Create table**.
- **Table name:** `Products`
- **Partition key:** `ProductID` (**Data type:** `String`)

### **Step 3:** Configure **Table Settings**
- **Default settings:** Leave enabled for this exercise.
- **Capacity mode:** Choose **On-demand** (for simplified management and avoiding scaling concerns).
- **Encryption:** Leave the default **AWS owned key** selected.
- Click **Create table**.

---

## **2. Add Items to the DynamoDB Table**

### **Step 1:** Open the **Products Table**
- Go to **Tables** > **Products** > **Explore items**.

### **Step 2:** Add **New Items**
- Click **Create item**.
- Switch to **JSON** view and add the following item:

```json
{
    "ProductID": "P001",
    "Name": "Smartphone",
    "Category": "Electronics",
    "Price": 499.99,
    "Stock": 50
}
```

- Add a **second item**:

```json
{
    "ProductID": "P002",
    "Name": "Laptop",
    "Category": "Electronics",
    "Price": 999.99,
    "Stock": 30
}
```

- Click **Create item**.

---

## **3. Query and Scan the DynamoDB Table**

### **Step 1:** Perform a **Scan Operation**
- In the **Explore items** section, click **Run** to **scan all items**.
- Verify that the **items added** are **displayed correctly**.

### **Step 2:** Perform a **Query Operation**
- Choose **Query** instead of **Scan**.
- Set the **partition key** to `ProductID`.
- Enter the **value** `P001` and run the query.
- The **query result** should return only the **Smartphone item**.

---

## **4. Update and Delete Items in the Table**

### **Step 1:** Update an **Existing Item**
- Select the **Smartphone item (P001)**.
- Click **Actions** > **Edit item**.
- Change the **Stock** value from **50** to **45**.
- Click **Save changes**.

### **Step 2:** Delete an **Item**
- Select the **Laptop item (P002)**.
- Click **Actions** > **Delete item**.
- Confirm the **deletion**.

---

## **5. Configure IAM Permissions for DynamoDB**

### **Step 1:** Navigate to the **IAM Console**
- Go to **Services** > **IAM**.

### **Step 2:** Create an **IAM Role**
- Click **Roles** > **Create role**.
- **Select trusted entity:** **AWS service**.
- **Use case:** Choose **DynamoDB**.

### **Step 3:** Attach a **Policy**
- Select **AmazonDynamoDBFullAccess**.
- **Role name:** `DynamoDBFullAccessRole`.
- Click **Create role**.

---

## **6. Clean Up Resources**

### **Step 1:** Delete the **DynamoDB Table**
- Navigate to **DynamoDB Console** > **Tables** > **Products**.
- Click **Actions** > **Delete table**.
- Confirm the **deletion**.

### **Step 2:** Remove the **IAM Role**
- Go to **IAM Console** > **Roles** > **DynamoDBFullAccessRole**.
- Click **Delete role** and confirm.

---

## **7. Conclusion**

By completing this activity, you have:

- **Set up a NoSQL database** using **Amazon DynamoDB**.
- Performed **CRUD operations** using the **AWS Management Console**.
- Configured **IAM permissions** for **DynamoDB access**.
- Cleaned up resources to **avoid unnecessary costs**.

For more information on **Amazon DynamoDB**, visit the [**AWS DynamoDB Documentation**](https://docs.aws.amazon.com/dynamodb/).