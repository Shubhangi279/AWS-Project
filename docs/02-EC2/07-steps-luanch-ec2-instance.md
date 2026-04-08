# Steps to Launch an EC2 Instance

## Introduction

An **EC2 Instance** is a virtual server in the cloud provided by **Amazon Web Services**.
Launching an EC2 instance allows you to run applications, host websites, deploy databases, and build scalable infrastructure without owning physical hardware.

---

## EC2 Launch Workflow Diagram
<img width="1536" height="1024" alt="839b9af6-405a-4f68-a28f-a6b6b17ffc41" src="https://github.com/user-attachments/assets/753e337a-54c3-4bcd-9d0e-0cad5a0afb36" />
---

## Step-by-Step Guide to Launch EC2 Instance

---

## Step 1 — Login to AWS Console

1. Open AWS Management Console
2. Search **EC2** in the services search bar
3. Click **EC2 Dashboard**

---

## EC2 Dashboard
<img width="1920" height="909" alt="Screenshot 2026-04-08 233457" src="https://github.com/user-attachments/assets/3aac6211-eae9-44f4-b950-94658428ab4a" />

---

## Step 2 — Click Launch Instance

* Select **Instances**
* Click **Launch Instance**

---

## Launch Instance Page
<img width="1920" height="903" alt="Screenshot 2026-04-08 234106" src="https://github.com/user-attachments/assets/b776cd20-6c96-46c5-94c7-5946db07d28a" />

---

## Step 3 — Choose Amazon Machine Image (AMI)

AMI contains:

* Operating System
* Preinstalled software
* Configuration settings

Examples:

* Amazon Linux
* Ubuntu
* Windows Server

---


## Step 4 — Choose Instance Type

Instance type defines:

* CPU
* Memory
* Performance

Example:

| Instance Type | Use Case             |
| ------------- | -------------------- |
| t2.micro      | Free tier testing    |
| t3.medium     | Applications         |
| m5.large      | Production workloads |

---

## Instance Type Selection
<img width="1920" height="910" alt="Screenshot 2026-04-08 234345" src="https://github.com/user-attachments/assets/f51a20d1-903f-47aa-bb97-2dd178d499a6" />

---

## Step 5 — Configure Instance Details

Configure:

* Number of instances
* Network (VPC)
* Subnet
* Auto assign public IP

---


## Step 6 — Add Storage

Attach storage using **EBS Volume**.

Example:

* 8 GB (Free Tier)
* SSD or HDD storage

---

## Storage Configuration
<img width="1920" height="907" alt="Screenshot 2026-04-08 234545" src="https://github.com/user-attachments/assets/339e3fd7-ef2c-4274-a378-1c45a0589859" />

---

## Step 7 — Add Tags

Tags help organize resources.

Example:

```
Name = My-Server
Environment = Dev
```

---

## Step 8 — Configure Security Group

Acts as a firewall.

Common Rules:

| Protocol | Port | Purpose        |
| -------- | ---- | -------------- |
| SSH      | 22   | Linux Access   |
| HTTP     | 80   | Website        |
| HTTPS    | 443  | Secure Website |

---

## Security Group Configuration
<img width="1920" height="910" alt="Screenshot 2026-04-08 234729" src="https://github.com/user-attachments/assets/d53b29fe-80c1-4718-adba-09630e4bcb4a" />

---

## Step 9 — Create Key Pair

Key Pair is required for secure login.

* Download `.pem` file
* Keep it safe

---

## Key Pair Creation
<img width="1920" height="907" alt="Screenshot 2026-04-08 234929" src="https://github.com/user-attachments/assets/6587affd-9bca-4376-a8f9-09d5314ae4d3" />

---

## tep 10 — Launch Instance

Click:

**Launch Instance**

Your EC2 server will start within seconds.

---

## Instance Running State
<img width="1920" height="907" alt="Screenshot 2026-04-08 235334" src="https://github.com/user-attachments/assets/657f3886-7f20-4fc7-8e4d-e922c27eaa46" />

---

## EC2 Instance Lifecycle

```
Launch → Pending → Running → Stopping → Stopped → Terminated
```

---

## Result

After launching, you can:

✅ Connect using SSH
✅ Deploy Web Applications
✅ Install Software
✅ Host Websites
✅ Run Cloud Projects

---

