# Create Amazon Elastic File System (Amazon EFS)

## Overview

In this practical, you will create an **Amazon Elastic File System (EFS)** using the AWS Management Console and configure it for use with Amazon EC2. The process includes selecting a VPC, creating Mount Targets, configuring Security Groups, and verifying that the file system is ready to be mounted.

---

## Amazon EFS Creation Workflow


![Image](https://images.openai.com/static-rsc-4/Jn5bt2ukg1wbl7VgWMAC_HV-k3wiUZ4dQblFbfQTcXIw8pKgb6F2vXG821SC5Lupumu7QqNH4EjGq5XNYU_E1I5CEPBv2eNu10qW8PRzAwjBpr0YmcsL1q-v-6uPFHBK17RpEtvwq02Vfl_VbKO0BRVaIhABptFmnEj5SB8wlhz93yJWScvYGjBJL9lMkPA7?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/fQkrES2ymLH7GML7AKQDBZv_ALeiWH_ojRNpitPlqU8Z6yrmuwEyoE-IrZoPzSDiE3Ik4jkO48Hd38t3trymDpXDGu7p_CiBZlSM-KHRsGU18UNpLzPKu2669BtycoGbjCHBtit7cqD01qSwaXs6xxPO1RtZvICtDksCF6xmVyILhpSMKQuPgzvSH0twCmoO?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/lf223s5VHIVx_O9mDZxgVEkcqFIzAKttdcvVnDC4B7LMpixRqHAT0RKCzc1hbbw9RR1wr4bWk6lqKrqb8eTKZW5msEUDzPFmNIp3yLb818vRtTAs0tQP8vZcgB8cVfwpFXX8mSG4dpuVPXTbylXVnYgtue6_SkqZtwn2I3hxF9NYDpO_gWVO7dv4F3AER5-4?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/tvOENHVHapkJzvrZctSYjjvtus5Q_ncuYoA1O2OzPuCIwLCj1nMqRnBRzH9LIlr4o5FbvasYRQaT_pXrPZGHFmt2MG3NC5H7u4iIFfcBXEfoql6n1LZicsW0k0BgTeRSmHDkObzjVaK_d-IDIubkCHZd6-nOP0Tra7-wpW1eVCXUu3Ce9cfvZGM_WHX0-8TD?purpose=fullsize)

---

# Prerequisites

Before creating an Amazon EFS file system, ensure you have:

* AWS Account
* IAM user with EFS permissions
* Amazon VPC
* At least one running Amazon EC2 instance
* Security Group allowing NFS (Port 2049)

---

# Step 1: Sign in to AWS Console

1. Open your browser.
2. Go to **[https://console.aws.amazon.com/](https://console.aws.amazon.com/)**
3. Sign in with your AWS account.

📸 **Screenshot 1**

**File Name**

```text
images/01-aws-console-home.png
```

**Capture**

AWS Management Console Home Page.

---

# Step 2: Open Amazon EFS

1. In the search bar type **EFS**.
2. Click **Elastic File System**.

📸 **Screenshot 2**

```text
images/02-efs-dashboard.png
```

Capture the EFS Dashboard.

---

# Step 3: Click "Create File System"

Click the **Create file system** button.

📸 **Screenshot 3**

```text
images/03-create-file-system.png
```

Capture the Create File System page.

---

# Step 4: Configure File System

Enter the following values.

| Setting      | Example     |
| ------------ | ----------- |
| Name         | My-EFS      |
| VPC          | Default VPC |
| Availability | Regional    |

Leave the remaining settings as default.

📸 **Screenshot 4**

```text
images/04-file-system-settings.png
```

Capture the configuration page.

---

# Step 5: Configure Network Access

Select the VPC and verify the Mount Targets.

| Setting      | Example     |
| ------------ | ----------- |
| VPC          | Default VPC |
| Subnet       | Default     |
| Mount Target | Automatic   |

📸 **Screenshot 5**

```text
images/05-network-settings.png
```

Capture the Network configuration page.

---

# Step 6: Configure Security Groups

Attach a Security Group that allows **NFS (Port 2049)**.

Example Inbound Rule:

| Type | Protocol | Port | Source             |
| ---- | -------- | ---- | ------------------ |
| NFS  | TCP      | 2049 | EC2 Security Group |

📸 **Screenshot 6**

```text
images/06-security-group.png
```

Capture the Security Group configuration.

---

# Step 7: Configure File System Policy (Optional)

You can keep the default policy or configure a custom IAM policy if required.

📸 **Screenshot 7**

```text
images/07-file-system-policy.png
```

Capture the File System Policy page.

---

# Step 8: Review Configuration

Verify:

* File System Name
* VPC
* Mount Targets
* Security Groups
* Performance Mode
* Throughput Mode

Click **Create**.

📸 **Screenshot 8**

```text
images/08-review-create.png
```

Capture the Review page.

---

# Step 9: File System Created Successfully

Wait until the status changes to **Available**.

Example:

```text
File System ID:
fs-0abcd1234efgh5678

Status:
Available
```

📸 **Screenshot 9**

```text
images/09-file-system-created.png
```

Capture the EFS dashboard showing the created file system.

---

# Step 10: Verify Mount Targets

Open the created file system.

Click **Network**.

Verify Mount Targets are created for each Availability Zone.

📸 **Screenshot 10**

```text
images/10-mount-targets.png
```

Capture the Mount Targets page.

---

# Step 11: Create an Access Point (Optional)

1. Open **Access Points**.
2. Click **Create Access Point**.
3. Enter:

| Setting        | Example        |
| -------------- | -------------- |
| Name           | AppAccessPoint |
| Root Directory | /appdata       |

Click **Create**.

📸 **Screenshot 11**

```text
images/11-access-point.png
```

Capture the Access Point creation page.

---

# Step 12: Verify File System Details

Check the following information:

* File System ID
* DNS Name
* Performance Mode
* Throughput Mode
* Lifecycle Management
* Encryption
* Size
* Mount Targets

📸 **Screenshot 12**

```text
images/12-file-system-details.png
```

Capture the Details page.

---

# Expected Output

After completing the above steps:

* Amazon EFS File System created successfully.
* Mount Targets available in the selected Availability Zones.
* Security Group configured for NFS access.
* File System status shows **Available**.
* Ready to mount on Amazon EC2.

---

# Complete Workflow

```text
AWS Console
      │
      ▼
Amazon EFS
      │
      ▼
Create File System
      │
      ▼
Configure VPC
      │
      ▼
Configure Mount Targets
      │
      ▼
Configure Security Groups
      │
      ▼
Review Settings
      │
      ▼
Create File System
      │
      ▼
Available
      │
      ▼
Verify Mount Targets
      │
      ▼
Create Access Point (Optional)
      │
      ▼
Ready to Mount on EC2
```

---

# Best Practices

* Use **Regional** EFS for production environments.
* Create Mount Targets in every Availability Zone where EC2 instances are running.
* Restrict NFS access to trusted Security Groups.
* Enable encryption using AWS KMS.
* Enable Lifecycle Management to reduce storage costs.
* Monitor the file system using Amazon CloudWatch.
* Use AWS Backup for regular backups.

---

