# Amazon EFS AWS CLI Commands

## Overview

The **AWS Command Line Interface (AWS CLI)** enables you to create, manage, monitor, and delete Amazon EFS resources directly from the terminal. It is widely used by Cloud Engineers, DevOps Engineers, and System Administrators to automate infrastructure tasks and manage AWS resources efficiently.

This guide demonstrates how to install and configure the AWS CLI and perform common Amazon EFS operations.

---

# Amazon EFS AWS CLI Workflow

![Image](https://images.openai.com/static-rsc-4/570wJhCf-70XZWFHPleBPlj-XzkyRRi7BMD9_nGyjIR8qaQYG3wDKKpEA3xF7ZnwhIRqACb4bVNAeDs0Z_a5eFiqi4xL6H1eoC1maPzTR9-3-5a8bnm7KzNCQ3DqC1zwcMZ3xnXRtDfoVuFzgE5uNj9ZodTUzwV9m4sUMvOewkdOvROnPNh1kBAiGKsG66Di?purpose=fullsize)

---

# Prerequisites

Before using AWS CLI with Amazon EFS, ensure you have:

* AWS Account
* IAM User with Amazon EFS permissions
* AWS CLI installed
* Configured AWS credentials
* Existing Amazon VPC

---

# Step 1: Install AWS CLI

### Windows

Download and install the AWS CLI from the official AWS website.

Verify installation:

```bash
aws --version
```

Expected Output

```text
aws-cli/2.x.x Python/3.x Windows/10
```

📸 **Screenshot 1**

```text
screenshots/21-install-aws-cli.png
```

---

### Ubuntu

```bash
sudo apt update
sudo apt install awscli -y
```

---

### Amazon Linux

```bash
sudo yum install awscli -y
```

---

# Step 2: Configure AWS CLI

Run:

```bash
aws configure
```

Provide:

```text
AWS Access Key ID:
AWS Secret Access Key:
Default region:
Default output format:
```

Example:

```text
AWS Access Key ID: AKIA****************
AWS Secret Access Key: ****************
Default Region: ap-south-1
Default Output Format: json
```

📸 **Screenshot 2**

```text
screenshots/22-aws-configure.png
```

---

# Step 3: Verify Configuration

```bash
aws sts get-caller-identity
```

Expected Output

```json
{
  "Account": "123456789012",
  "UserId": "AIDA***********",
  "Arn": "arn:aws:iam::123456789012:user/admin"
}
```

📸 **Screenshot 3**

```text
screenshots/23-verify-cli.png
```

---

# Step 4: Create an Amazon EFS File System

```bash
aws efs create-file-system \
--creation-token MyEFS \
--performance-mode generalPurpose \
--throughput-mode elastic
```

Expected Output

```json
{
  "FileSystemId": "fs-0123456789abcdef0",
  "LifeCycleState": "creating"
}
```

📸 **Screenshot 4**

```text
screenshots/24-create-efs-cli.png
```

---

# Step 5: List All EFS File Systems

```bash
aws efs describe-file-systems
```

This command displays all available Amazon EFS file systems.

📸 **Screenshot 5**

```text
screenshots/25-list-file-systems.png
```

---

# Step 6: Describe a Specific File System

```bash
aws efs describe-file-systems \
--file-system-id fs-0123456789abcdef0
```

Displays detailed information about the specified file system.

📸 **Screenshot 6**

```text
screenshots/26-describe-file-system.png
```

---

# Step 7: Create a Mount Target

```bash
aws efs create-mount-target \
--file-system-id fs-0123456789abcdef0 \
--subnet-id subnet-12345678 \
--security-groups sg-12345678
```

Expected Output

```json
{
  "MountTargetId": "fsmt-0123456789abcdef0"
}
```

📸 **Screenshot 7**

```text
screenshots/27-create-mount-target.png
```

---

# Step 8: List Mount Targets

```bash
aws efs describe-mount-targets \
--file-system-id fs-0123456789abcdef0
```

Displays all mount targets for the file system.

📸 **Screenshot 8**

```text
screenshots/28-list-mount-targets.png
```

---

# Step 9: Create an Access Point

```bash
aws efs create-access-point \
--file-system-id fs-0123456789abcdef0
```

Expected Output

```json
{
  "AccessPointId": "fsap-0123456789abcdef0"
}
```

📸 **Screenshot 9**

```text
screenshots/29-create-access-point.png
```

---

# Step 10: List Access Points

```bash
aws efs describe-access-points
```

Displays all available EFS access points.

📸 **Screenshot 10**

```text
screenshots/30-list-access-points.png
```

---

# Step 11: Delete an Access Point

```bash
aws efs delete-access-point \
--access-point-id fsap-0123456789abcdef0
```

---

# Step 12: Delete a Mount Target

```bash
aws efs delete-mount-target \
--mount-target-id fsmt-0123456789abcdef0
```

> **Note:** Delete all mount targets before deleting the EFS file system.

---

# Step 13: Delete the EFS File System

```bash
aws efs delete-file-system \
--file-system-id fs-0123456789abcdef0
```

---

# Frequently Used AWS CLI Commands

| Command                          | Purpose                   |
| -------------------------------- | ------------------------- |
| `aws efs create-file-system`     | Create an EFS file system |
| `aws efs describe-file-systems`  | List EFS file systems     |
| `aws efs create-mount-target`    | Create a mount target     |
| `aws efs describe-mount-targets` | List mount targets        |
| `aws efs create-access-point`    | Create an access point    |
| `aws efs describe-access-points` | List access points        |
| `aws efs delete-access-point`    | Delete an access point    |
| `aws efs delete-mount-target`    | Delete a mount target     |
| `aws efs delete-file-system`     | Delete an EFS file system |

---

# AWS CLI Workflow

```text
Install AWS CLI
        │
        ▼
Configure AWS CLI
        │
        ▼
Verify Credentials
        │
        ▼
Create EFS
        │
        ▼
Create Mount Target
        │
        ▼
Create Access Point
        │
        ▼
Mount on EC2
        │
        ▼
Describe Resources
        │
        ▼
Delete Resources
```

---

# Best Practices

* Use **IAM Roles** instead of long-term access keys whenever possible.
* Avoid embedding AWS credentials in scripts.
* Store sensitive credentials in **AWS Secrets Manager**.
* Use descriptive names for file systems, mount targets, and access points.
* Create mount targets in every Availability Zone where EC2 instances are deployed.
* Regularly review and remove unused EFS resources to optimize costs.
* Automate repetitive tasks using shell scripts, CloudFormation, or Terraform.

---

# Conclusion

The AWS CLI provides a fast and efficient way to manage Amazon EFS resources. It supports automation, scripting, and infrastructure management, making it an essential tool for cloud engineers and DevOps professionals. Learning these commands helps simplify deployment, improve operational efficiency, and prepare for real-world AWS administration tasks.

---

## 📂 Screenshots Folder

```text
screenshots/
├── 21-install-aws-cli.png
├── 22-aws-configure.png
├── 23-verify-cli.png
├── 24-create-efs-cli.png
├── 25-list-file-systems.png
├── 26-describe-file-system.png
├── 27-create-mount-target.png
├── 28-list-mount-targets.png
├── 29-create-access-point.png
└── 30-list-access-points.png
```

---
