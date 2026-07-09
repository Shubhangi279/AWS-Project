# Connect Amazon EC2 to Amazon RDS

## Overview

Connecting an **Amazon EC2 instance** to an **Amazon RDS database** is a common architecture in AWS. The application runs on the EC2 instance, while the database is hosted on Amazon RDS inside a secure **Amazon VPC**. Communication between the EC2 instance and the RDS database occurs through private networking and is controlled by **Security Groups**.

This architecture improves security, scalability, and performance by separating the application layer from the database layer.

---

# EC2 to RDS Architecture

![Image](https://images.openai.com/static-rsc-4/Z_PJ62G8pY9FSOShvn4hEX5oDl33T__QDG7VOaBXtTC7yCLS-_aTc7b7SruusffCRuKRPR1R22q0V--b98hxp6De0dc3K2Z9SWI0LHBAhrT0IMWi5fVlNylMlkzH8QMZDtNGv790RNnoZ9iKu6a0wUPquf4mNkdlq0bKH_eiHcCFjBiB8sWr_JzNwkP_TkH4?purpose=fullsize)


```text
                     Internet
                         │
                  Internet Gateway
                         │
          ┌────────────────────────────┐
          │         Amazon VPC         │
          │                            │
          │  Public Subnet             │
          │ ┌─────────────────────┐    │
          │ │ Amazon EC2          │    │
          │ │ Application Server  │    │
          │ └─────────┬───────────┘    │
          │           │ Port 3306      │
          │           ▼                │
          │  Private Subnet            │
          │ ┌─────────────────────┐    │
          │ │ Amazon RDS MySQL    │    │
          │ └─────────────────────┘    │
          └────────────────────────────┘
```

---

# Prerequisites

Before connecting EC2 to RDS, make sure you have:

* AWS Account
* Running EC2 instance
* Running Amazon RDS instance
* Both resources in the **same VPC**
* Security Groups configured correctly
* MySQL client installed on EC2

---

# Step 1: Verify EC2 Instance

Go to:

**AWS Console → EC2 → Instances**

Verify that:

* Instance State = **Running**
* Public IP is available (if connecting through SSH)

📸 **Screenshot 1:** EC2 Instance Dashboard

---

# Step 2: Verify RDS Instance

Go to:

**AWS Console → Amazon RDS → Databases**

Ensure:

* Database Status = **Available**
* Endpoint is displayed

📸 **Screenshot 2:** RDS Database Dashboard

---

# Step 3: Check VPC

Ensure both EC2 and RDS belong to the **same VPC**.

Example:

| Resource | VPC    |
| -------- | ------ |
| EC2      | My-VPC |
| RDS      | My-VPC |

📸 **Screenshot 3:** VPC Configuration

---

# Step 4: Configure RDS Security Group

Open the Security Group attached to the RDS instance.

Add an inbound rule:

| Type         | Port | Source             |
| ------------ | ---- | ------------------ |
| MySQL/Aurora | 3306 | EC2 Security Group |

This allows only your EC2 instance to connect.

📸 **Screenshot 4:** RDS Security Group

---

# Step 5: Connect to EC2 Using SSH

Linux/macOS:

```bash
ssh -i mykey.pem ec2-user@<EC2-Public-IP>
```

Ubuntu:

```bash
ssh -i mykey.pem ubuntu@<EC2-Public-IP>
```

📸 **Screenshot 5:** SSH Connection

---

# Step 6: Install MySQL Client

For Amazon Linux:

```bash
sudo yum update -y
sudo yum install mysql -y
```

For Ubuntu:

```bash
sudo apt update
sudo apt install mysql-client -y
```

Verify installation:

```bash
mysql --version
```

📸 **Screenshot 6:** MySQL Client Installed

---

# Step 7: Obtain RDS Endpoint

Open the RDS instance and copy the endpoint.

Example:

```text
studentdb.abc123xyz.ap-south-1.rds.amazonaws.com
```

Port:

```text
3306
```

📸 **Screenshot 7:** RDS Endpoint

---

# Step 8: Connect EC2 to RDS

Run:

```bash
mysql -h studentdb.abc123xyz.ap-south-1.rds.amazonaws.com \
-u admin \
-p
```

Enter your password.

If successful:

```sql
Welcome to the MySQL monitor.
```

📸 **Screenshot 8:** Successful Database Connection

---

# Step 9: Verify Connection

Show databases:

```sql
SHOW DATABASES;
```

Example output:

```text
information_schema
mysql
performance_schema
studentdb
```

📸 **Screenshot 9:** Database List

---

# Step 10: Create a Table

```sql
USE studentdb;

CREATE TABLE students (
id INT PRIMARY KEY,
name VARCHAR(50),
city VARCHAR(30)
);
```

Insert a record:

```sql
INSERT INTO students
VALUES
(1,'Shubhangi','Nashik');
```

Retrieve data:

```sql
SELECT * FROM students;
```

📸 **Screenshot 10:** Table Created

---

# Connection Workflow

```text
User
 │
 ▼
Browser
 │
 ▼
EC2 Application
 │
 ▼
Security Group
 │
 ▼
Amazon RDS Endpoint
 │
 ▼
MySQL Database
 │
 ▼
Response Returned
```

---

# Troubleshooting

| Issue                   | Possible Cause          | Solution                                   |
| ----------------------- | ----------------------- | ------------------------------------------ |
| Can't connect           | Incorrect endpoint      | Verify the RDS endpoint                    |
| Access denied           | Wrong username/password | Check database credentials                 |
| Connection timed out    | Security Group issue    | Allow MySQL (3306) from EC2 Security Group |
| Host unreachable        | Different VPC           | Place EC2 and RDS in the same VPC          |
| MySQL command not found | Client not installed    | Install the MySQL client                   |

---

# Best Practices

* Deploy RDS in a **private subnet**.
* Allow access only from the EC2 Security Group.
* Avoid making RDS publicly accessible in production.
* Use IAM roles and AWS Secrets Manager for credential management.
* Enable SSL/TLS encryption for database connections.
* Monitor database performance with Amazon CloudWatch.
* Enable automated backups and Multi-AZ deployments for production environments.

---

# Summary

Connecting Amazon EC2 to Amazon RDS enables applications to securely access managed databases within the same VPC. By using Security Groups, private networking, and the RDS endpoint, you can establish a secure and reliable connection. This architecture is widely used for web applications, enterprise systems, and cloud-native workloads because it improves scalability, security, and operational efficiency.

---


