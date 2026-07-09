# Create an Amazon RDS Database (Step-by-Step)

## Objective

In this lab, we will create an Amazon RDS MySQL database instance using the AWS Management Console. The database will be deployed inside a Virtual Private Cloud (VPC) with secure network settings, automated backups, and monitoring enabled.

---

# Prerequisites

Before creating an RDS instance, ensure you have:

* AWS Account
* IAM User with RDS permissions
* A VPC with at least two subnets
* Security Group
* Internet connection
* AWS Management Console access

---

# Step 1: Login to AWS Console

1. Open your browser.
2. Visit **[https://console.aws.amazon.com/](https://console.aws.amazon.com/)**
3. Sign in with your AWS credentials.

📸 **Screenshot 1:** AWS Management Console Home

---

# Step 2: Open Amazon RDS

1. In the AWS search bar, type **RDS**.
2. Select **Amazon RDS**.

📸 **Screenshot 2:** Amazon RDS Dashboard

---

# Step 3: Create Database

1. Click **Create database**.

📸 **Screenshot 3:** Create Database Button

---

# Step 4: Choose Database Creation Method

Select:

* **Standard Create**

Click **Next**.

📸 **Screenshot 4:** Standard Create

---

# Step 5: Select Database Engine

Choose:

* **MySQL**

Other supported engines include:

* PostgreSQL
* MariaDB
* Oracle
* SQL Server
* Aurora

📸 **Screenshot 5:** Database Engine Selection

---

# Step 6: Select Version

Choose the latest stable MySQL version (recommended by AWS).

Example:

```
MySQL 8.0.xx
```

📸 **Screenshot 6:** Engine Version

---

# Step 7: Choose Template

Select:

* **Free Tier** (for learning)
* **Dev/Test**
* **Production**

For practice, select **Free Tier**.

📸 **Screenshot 7:** Template Selection

---

# Step 8: Configure DB Instance

Enter:

| Field                  | Example Value |
| ---------------------- | ------------- |
| DB Instance Identifier | studentdb     |
| Master Username        | admin         |
| Master Password        | ********      |

📸 **Screenshot 8:** DB Settings

---

# Step 9: Choose Instance Class

Example:

```
db.t3.micro
```

This is eligible for AWS Free Tier.

📸 **Screenshot 9:** Instance Class

---

# Step 10: Configure Storage

Example:

| Setting             | Value                     |
| ------------------- | ------------------------- |
| Storage Type        | General Purpose SSD (gp3) |
| Allocated Storage   | 20 GB                     |
| Storage Autoscaling | Enabled                   |

📸 **Screenshot 10:** Storage Configuration

---

# Step 11: Connectivity

Choose:

| Option            | Value         |
| ----------------- | ------------- |
| VPC               | My-VPC        |
| Public Access     | No            |
| Security Group    | My-RDS-SG     |
| Availability Zone | No Preference |

📸 **Screenshot 11:** Connectivity Settings

---

# Step 12: Additional Configuration

Enter:

| Field                 | Value     |
| --------------------- | --------- |
| Initial Database Name | studentdb |

Optional:

* Enable Backups
* Enable Monitoring
* Enable Performance Insights

📸 **Screenshot 12:** Additional Configuration

---

# Step 13: Create Database

Click

**Create Database**

AWS begins provisioning the RDS instance.

Status:

```
Creating...
```

After a few minutes:

```
Available
```

📸 **Screenshot 13:** Database Creation Progress

---

# Step 14: View Database Details

Open the database instance to view:

* Endpoint
* Port
* Security Group
* Database Engine
* Availability Zone
* Storage
* Backup Status

📸 **Screenshot 14:** RDS Instance Details

---

# Step 15: Copy Endpoint

Example:

```text
studentdb.abc123xyz.ap-south-1.rds.amazonaws.com
```

Port:

```
3306
```

This endpoint is required to connect applications.

📸 **Screenshot 15:** Endpoint Information

---

# Step 16: Modify Security Group

Allow inbound MySQL access.

Example Rule

| Type  | Port | Source             |
| ----- | ---- | ------------------ |
| MySQL | 3306 | EC2 Security Group |

📸 **Screenshot 16:** Security Group Rule

---

# Step 17: Connect EC2 to RDS

SSH into your EC2 instance and install the MySQL client.

```bash
sudo yum update -y
sudo yum install mysql -y
```

For Ubuntu:

```bash
sudo apt update
sudo apt install mysql-client -y
```

📸 **Screenshot 17:** MySQL Client Installation

---

# Step 18: Connect to the Database

```bash
mysql -h studentdb.abc123xyz.ap-south-1.rds.amazonaws.com \
-u admin \
-p
```

Enter the password.

If successful:

```sql
Welcome to the MySQL monitor.
```

📸 **Screenshot 18:** Successful Connection

---

# Step 19: Create a Sample Database

```sql
CREATE DATABASE college;
```

Check:

```sql
SHOW DATABASES;
```

📸 **Screenshot 19:** Create Database

---

# Step 20: Create Table

```sql
USE college;

CREATE TABLE students(
id INT PRIMARY KEY,
name VARCHAR(50),
city VARCHAR(30)
);
```

Insert data:

```sql
INSERT INTO students
VALUES
(1,'Shubhangi','Nashik');
```

View data:

```sql
SELECT * FROM students;
```

📸 **Screenshot 20:** Table Created Successfully

---

# Complete Workflow

```text
AWS Console
      │
      ▼
Amazon RDS
      │
      ▼
Create Database
      │
      ▼
Configure Engine
      │
      ▼
Configure Storage
      │
      ▼
Configure Networking
      │
      ▼
Create DB Instance
      │
      ▼
Available
      │
      ▼
Copy Endpoint
      │
      ▼
Connect EC2
      │
      ▼
Connect MySQL Client
      │
      ▼
Create Database
      │
      ▼
Run SQL Queries
```

---

# Best Practices

* Use **Private Subnets** for production databases.
* Enable **Automated Backups** and **Multi-AZ** for high availability.
* Restrict database access using **Security Groups**.
* Enable **Storage Autoscaling**.
* Turn on **Performance Insights** and **CloudWatch Monitoring**.
* Rotate database credentials regularly or use **AWS Secrets Manager**.

---

# Expected Output

* ✅ Amazon RDS instance created successfully.
* ✅ MySQL database is available.
* ✅ Security Group configured.
* ✅ EC2 instance connected to RDS.
* ✅ Sample database and table created.
* ✅ SQL queries executed successfully.

---

