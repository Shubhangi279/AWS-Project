# AWS Launch Template

## Overview

An **AWS Launch Template** is a reusable configuration that defines how Amazon EC2 instances should be launched. It is the recommended method for creating instances in **Amazon EC2 Auto Scaling**, replacing the older **Launch Configuration** feature.

A Launch Template stores all the information required to launch an EC2 instance, including the **Amazon Machine Image (AMI)**, **instance type**, **security groups**, **IAM role**, **storage**, **key pair**, and **user data scripts**.

By using Launch Templates, organizations can maintain consistent, repeatable, and automated EC2 deployments across development, testing, and production environments.

---

# AWS Launch Template Architecture

![Image](https://images.openai.com/static-rsc-4/QUOGGoDYvWUFtBEkBwhV303fBeynO0BJ8WlANPj58kUaPSPmrnc8_X3UO8fKYLw3pRFInr3exEDi89Ov5d2iM3UktXu-RW-FR3Xy3vq_cnsDhNxgVTXfK49r_lvT9hvuUFflABvsqbAQGF6InO2npRdJWxeSNcE6JFGqQbuiCm12odMI06p1WnqWA5QTituE?purpose=fullsize)

---

# Launch Template Workflow

```text
                  Launch Template
                        │
        ┌───────────────┼───────────────┐
        ▼               ▼               ▼
      AMI         Instance Type    Security Group
        │               │               │
        └───────────────┼───────────────┘
                        ▼
             Auto Scaling Group (ASG)
                        │
        ┌───────────────┼───────────────┐
        ▼               ▼               ▼
    EC2 Instance 1  EC2 Instance 2  EC2 Instance 3
```

---

# What is a Launch Template?

A **Launch Template** acts as a blueprint for launching EC2 instances.

Instead of configuring every EC2 instance manually, you define the settings once and reuse them whenever new instances are required.

---

# Features of Launch Templates

* Reusable EC2 configuration
* Version management
* Supports Auto Scaling Groups
* Supports Spot and On-Demand Instances
* User Data automation
* IAM Role integration
* Network configuration
* EBS volume configuration
* Advanced monitoring options

---

# Components of a Launch Template

| Component                  | Description                                            |
| -------------------------- | ------------------------------------------------------ |
| Amazon Machine Image (AMI) | Operating system and software image                    |
| Instance Type              | EC2 hardware specification (e.g., t2.micro, t3.medium) |
| Key Pair                   | SSH login credentials                                  |
| Security Groups            | Firewall rules                                         |
| IAM Role                   | Grants AWS service permissions                         |
| Storage (EBS)              | Root and additional volumes                            |
| Network Interface          | VPC, subnet, and IP settings                           |
| User Data                  | Startup automation script                              |
| Monitoring                 | Enable CloudWatch detailed monitoring                  |
| Tags                       | Resource identification                                |

---

# Launch Template Architecture

```text
               Launch Template
                      │
     ┌────────────────┼────────────────┐
     ▼                ▼                ▼
   AMI           Instance Type      IAM Role
     │                │                │
     ├────────────────┼────────────────┤
     ▼                ▼                ▼
Security Group     EBS Volume      User Data
                     │
                     ▼
          Auto Scaling Group (ASG)
                     │
          ┌──────────┴──────────┐
          ▼                     ▼
      EC2 Instance 1      EC2 Instance 2
```

---

# Steps to Create a Launch Template

## Step 1: Open EC2 Dashboard

1. Sign in to the **AWS Management Console**.
2. Navigate to **EC2 Dashboard**.
3. In the left navigation pane, click **Launch Templates**.
4. Click **Create Launch Template**.

📸 **Screenshot 1**

```text
screenshots/01-launch-template-dashboard.png
```

---

## Step 2: Enter Template Details

Provide the following information:

| Field                | Example                          |
| -------------------- | -------------------------------- |
| Launch Template Name | WebServer-Template               |
| Description          | Launch template for Auto Scaling |

📸 **Screenshot 2**

```text
screenshots/02-template-details.png
```

---

## Step 3: Choose an Amazon Machine Image (AMI)

Select an operating system image.

Examples:

* Amazon Linux 2023
* Ubuntu Server 24.04 LTS
* Red Hat Enterprise Linux
* Microsoft Windows Server

📸 **Screenshot 3**

```text
screenshots/03-select-ami.png
```

---

## Step 4: Select an Instance Type

Choose the EC2 instance type based on your workload.

Examples:

| Instance Type | Use Case                |
| ------------- | ----------------------- |
| t2.micro      | Free Tier testing       |
| t3.micro      | Small web applications  |
| t3.medium     | Production workloads    |
| m5.large      | Enterprise applications |

📸 **Screenshot 4**

```text
screenshots/04-instance-type.png
```

---

## Step 5: Configure Key Pair

Choose an existing SSH key pair or create a new one.

Purpose:

* Secure SSH access
* Remote administration

📸 **Screenshot 5**

```text
screenshots/05-key-pair.png
```

---

## Step 6: Configure Security Group

Allow only required traffic.

Example:

| Protocol | Port | Source         |
| -------- | ---- | -------------- |
| SSH      | 22   | Your Public IP |
| HTTP     | 80   | 0.0.0.0/0      |
| HTTPS    | 443  | 0.0.0.0/0      |

📸 **Screenshot 6**

```text
screenshots/06-security-group.png
```

---

## Step 7: Configure Storage

Example configuration:

| Volume      | Size  | Type    |
| ----------- | ----- | ------- |
| Root Volume | 20 GB | gp3 SSD |

📸 **Screenshot 7**

```text
screenshots/07-storage.png
```

---

## Step 8: Add IAM Role (Optional)

Attach an IAM Role to allow EC2 instances to access AWS services securely.

Examples:

* AmazonS3ReadOnlyAccess
* CloudWatchAgentServerPolicy

📸 **Screenshot 8**

```text
screenshots/08-iam-role.png
```

---

## Step 9: Add User Data (Optional)

Use **User Data** to automatically install software when the instance starts.

Example:

```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl enable httpd
systemctl start httpd
echo "<h1>Welcome to AWS Auto Scaling</h1>" > /var/www/html/index.html
```

📸 **Screenshot 9**

```text
screenshots/09-user-data.png
```

---

## Step 10: Review and Create

Review all settings and click **Create Launch Template**.

📸 **Screenshot 10**

```text
screenshots/10-review-create-template.png
```

---

# AWS CLI Example

Create a Launch Template using the AWS CLI:

```bash
aws ec2 create-launch-template \
  --launch-template-name WebServer-Template \
  --version-description "Version 1" \
  --launch-template-data '{
    "ImageId":"ami-xxxxxxxx",
    "InstanceType":"t3.micro",
    "SecurityGroupIds":["sg-xxxxxxxx"],
    "KeyName":"MyKeyPair"
  }'
```

---

# Best Practices

* Use **Launch Templates** instead of Launch Configurations.
* Create new template versions for updates instead of modifying existing versions.
* Keep AMIs updated with the latest security patches.
* Attach IAM Roles instead of storing AWS credentials on EC2 instances.
* Restrict Security Group rules to only necessary ports.
* Use User Data for automated instance configuration.
* Apply consistent resource tags for management and billing.

---

# Real-World Example

A software company hosts its application behind an Application Load Balancer. During peak traffic, the Auto Scaling Group launches new EC2 instances automatically. Each new instance is created from the **Launch Template**, which includes:

* Amazon Linux 2023 AMI
* `t3.medium` instance type
* Web server installation through User Data
* IAM role for CloudWatch logging
* Security Group allowing HTTP and HTTPS traffic

This ensures that every newly launched instance is configured identically and can immediately begin serving user requests.

---

# Conclusion

AWS Launch Templates provide a standardized and reusable method for launching EC2 instances. They simplify infrastructure management, improve deployment consistency, and integrate seamlessly with Auto Scaling Groups, making them a foundational component of modern AWS architectures.

---


