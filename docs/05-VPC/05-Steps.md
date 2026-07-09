# Steps to Create an Amazon VPC

# Prerequisites

Before creating a VPC, ensure you have:

* An AWS Account
* IAM User with VPC permissions
* Internet connection
* AWS Management Console access

---

# Step 1: Login to AWS Management Console

1. Open your browser.
2. Go to **[https://console.aws.amazon.com/](https://console.aws.amazon.com/)**
3. Sign in to your AWS account.

📸 **Screenshot 1:** AWS Management Console Home Page

> **Image:** `images/01-AWS-Console.png`

---

# Step 2: Open the VPC Dashboard

1. In the search bar, type **VPC**.
2. Select **VPC** from the AWS services list.

📸 **Screenshot 2:** VPC Dashboard

> **Image:** `images/02-VPC-Dashboard.png`

---

# Step 3: Create a New VPC

1. Click **Create VPC**.
2. Select **VPC only**.

Enter the following details:

| Field     | Value       |
| --------- | ----------- |
| Name      | My-VPC      |
| IPv4 CIDR | 10.0.0.0/16 |
| IPv6 CIDR | None        |
| Tenancy   | Default     |

Click **Create VPC**.

📸 **Screenshot 3:** Create VPC Page

> **Image:** `images/03-Create-VPC.png`

---

# Step 4: Verify the VPC

After creation, verify the VPC details.

Example:

| Property | Value        |
| -------- | ------------ |
| Name     | My-VPC       |
| VPC ID   | vpc-xxxxxxxx |
| CIDR     | 10.0.0.0/16  |
| State    | Available    |

📸 **Screenshot 4:** Created VPC

> **Image:** `images/04-VPC-Created.png`

---

# Step 5: Create a Public Subnet

1. Click **Subnets**.
2. Click **Create Subnet**.
3. Select **My-VPC**.

Enter:

| Field             | Value         |
| ----------------- | ------------- |
| Name              | Public-Subnet |
| Availability Zone | ap-south-1a   |
| CIDR              | 10.0.1.0/24   |

Click **Create Subnet**.

📸 **Screenshot 5:** Public Subnet

> **Image:** `images/05-Public-Subnet.png`

---

# Step 6: Create a Private Subnet

Again click **Create Subnet**.

Enter:

| Field             | Value          |
| ----------------- | -------------- |
| Name              | Private-Subnet |
| Availability Zone | ap-south-1b    |
| CIDR              | 10.0.2.0/24    |

Click **Create Subnet**.

📸 **Screenshot 6:** Private Subnet

> **Image:** `images/06-Private-Subnet.png`

---

# Step 7: Create an Internet Gateway

1. Select **Internet Gateways**.
2. Click **Create Internet Gateway**.
3. Name it **My-IGW**.
4. Click **Create**.

📸 **Screenshot 7:** Internet Gateway Created

> **Image:** `images/07-Internet-Gateway.png`

---

# Step 8: Attach Internet Gateway

1. Select **My-IGW**.
2. Click **Actions → Attach to VPC**.
3. Select **My-VPC**.
4. Click **Attach**.

📸 **Screenshot 8:** Attach Internet Gateway

> **Image:** `images/08-Attach-IGW.png`

---

# Step 9: Create a Public Route Table

1. Open **Route Tables**.
2. Click **Create Route Table**.

Enter:

| Name | Public-RT |
| ---- | --------- |
| VPC  | My-VPC    |

Click **Create**.

📸 **Screenshot 9:** Public Route Table

> **Image:** `images/09-Route-Table.png`

---

# Step 10: Add Internet Route

1. Open **Routes**.
2. Click **Edit Routes**.
3. Add:

| Destination | Target           |
| ----------- | ---------------- |
| 0.0.0.0/0   | Internet Gateway |

Save changes.

📸 **Screenshot 10:** Internet Route

> **Image:** `images/10-Internet-Route.png`

---

# Step 11: Associate Public Subnet

1. Click **Subnet Associations**.
2. Select **Public-Subnet**.
3. Save.

📸 **Screenshot 11:** Route Table Association

> **Image:** `images/11-Subnet-Association.png`

---

# Step 12: Create NAT Gateway

1. Open **NAT Gateways**.
2. Click **Create NAT Gateway**.
3. Select **Public-Subnet**.
4. Allocate an Elastic IP.
5. Click **Create**.

📸 **Screenshot 12:** NAT Gateway

> **Image:** `images/12-NAT-Gateway.png`

---

# Step 13: Create Private Route Table

Create another Route Table.

| Name | Private-RT |
| ---- | ---------- |
| VPC  | My-VPC     |

📸 **Screenshot 13:** Private Route Table

> **Image:** `images/13-Private-Route-Table.png`

---

# Step 14: Add NAT Route

Edit Routes.

Add:

| Destination | Target      |
| ----------- | ----------- |
| 0.0.0.0/0   | NAT Gateway |

Save.

📸 **Screenshot 14:** NAT Route

> **Image:** `images/14-NAT-Route.png`

---

# Step 15: Associate Private Subnet

Associate **Private-Subnet** with **Private-RT**.

📸 **Screenshot 15:** Private Subnet Association

> **Image:** `images/15-Private-Association.png`

---

# Step 16: Launch EC2 Instances

Launch:

* **Web Server** → Public Subnet
* **Application Server** → Private Subnet

📸 **Screenshot 16:** EC2 Instances

> **Image:** `images/16-EC2-Instances.png`

---

# Final Architecture

```text
Internet
    │
Internet Gateway
    │
┌────────────── Amazon VPC ──────────────┐
│                                        │
│ Public Subnet      Private Subnet      │
│ ┌─────────────┐    ┌───────────────┐   │
│ │ EC2 Web     │──▶ │ EC2 App       │   │
│ │ Server      │    │ Server        │   │
│ └─────┬───────┘    └──────┬────────┘   │
│       │                   │            │
│ NAT Gateway          Amazon RDS        │
└────────────────────────────────────────┘
```

---

# Expected Output

* ✅ Custom VPC created
* ✅ Public and Private Subnets configured
* ✅ Internet Gateway attached
* ✅ NAT Gateway configured
* ✅ Route Tables associated correctly
* ✅ EC2 instances deployed in appropriate subnets
* ✅ Secure network architecture ready for hosting applications

---


This structure is clean, easy to navigate, and looks professional in a GitHub portfolio.

