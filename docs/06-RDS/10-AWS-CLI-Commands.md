# Amazon RDS AWS CLI Commands

## Overview

The **AWS Command Line Interface (AWS CLI)** is a unified tool that allows you to manage AWS services from the terminal. With AWS CLI, you can create, modify, monitor, and delete Amazon RDS resources without using the AWS Management Console. It is widely used for automation, scripting, and DevOps workflows.

---

# AWS CLI Workflow

```text
User
   │
   ▼
AWS CLI
   │
   ▼
AWS Credentials
   │
   ▼
Amazon RDS Service
   │
   ▼
Create / Modify / Delete Database
```

---

# Prerequisites

Before using the AWS CLI with Amazon RDS:

* Install AWS CLI
* Create an AWS account
* Configure IAM user with RDS permissions
* Configure AWS CLI with credentials

---

# Step 1: Install AWS CLI

### Windows

Download the installer from the official AWS CLI page.

Verify installation:

```bash
aws --version
```

Example Output:

```text
aws-cli/2.17.xx Python/3.xx Windows/10
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

Enter:

```text
AWS Access Key ID:
AWS Secret Access Key:
Default Region:
Default Output Format:
```

Example:

```text
AWS Access Key ID: AKIAxxxxxxxx
AWS Secret Access Key: ****************
Default Region: ap-south-1
Default Output Format: json
```

---

# Step 3: Verify Configuration

```bash
aws sts get-caller-identity
```

Example Output:

```json
{
 "Account":"123456789012",
 "UserId":"AIDXXXXXXXX",
 "Arn":"arn:aws:iam::123456789012:user/admin"
}
```

---

# Step 4: List Available DB Instances

```bash
aws rds describe-db-instances
```

This command displays all RDS database instances in your AWS account.

---

# Step 5: Create an RDS MySQL Instance

```bash
aws rds create-db-instance \
--db-instance-identifier studentdb \
--db-instance-class db.t3.micro \
--engine mysql \
--master-username admin \
--master-user-password Password123 \
--allocated-storage 20
```

### Explanation

| Parameter                  | Description     |
| -------------------------- | --------------- |
| `--db-instance-identifier` | Database name   |
| `--db-instance-class`      | Instance size   |
| `--engine`                 | Database engine |
| `--master-username`        | Admin username  |
| `--master-user-password`   | Admin password  |
| `--allocated-storage`      | Storage in GB   |

---

# Step 6: Check Database Status

```bash
aws rds describe-db-instances \
--db-instance-identifier studentdb
```

Example Status:

```text
creating
```

After a few minutes:

```text
available
```

---

# Step 7: List Database Endpoints

```bash
aws rds describe-db-instances \
--query "DBInstances[*].Endpoint.Address"
```

Example Output:

```text
studentdb.abc123xyz.ap-south-1.rds.amazonaws.com
```

---

# Step 8: Modify DB Instance

Increase storage:

```bash
aws rds modify-db-instance \
--db-instance-identifier studentdb \
--allocated-storage 30 \
--apply-immediately
```

---

# Step 9: Reboot Database

```bash
aws rds reboot-db-instance \
--db-instance-identifier studentdb
```

---

# Step 10: Create Manual Snapshot

```bash
aws rds create-db-snapshot \
--db-instance-identifier studentdb \
--db-snapshot-identifier studentdb-backup
```

---

# Step 11: List Snapshots

```bash
aws rds describe-db-snapshots
```

---

# Step 12: Restore Database from Snapshot

```bash
aws rds restore-db-instance-from-db-snapshot \
--db-instance-identifier restored-db \
--db-snapshot-identifier studentdb-backup
```

---

# Step 13: Start Database

```bash
aws rds start-db-instance \
--db-instance-identifier studentdb
```

---

# Step 14: Stop Database

```bash
aws rds stop-db-instance \
--db-instance-identifier studentdb
```

> **Note:** Not all RDS engines or configurations support stopping instances.

---

# Step 15: Delete Database

```bash
aws rds delete-db-instance \
--db-instance-identifier studentdb \
--skip-final-snapshot
```

> **Note:** In production, it's recommended to create a final snapshot before deletion.

---

# Step 16: List Available Database Engines

```bash
aws rds describe-db-engine-versions
```

---

# Step 17: View Pending Maintenance

```bash
aws rds describe-pending-maintenance-actions
```

---

# Step 18: List Read Replicas

```bash
aws rds describe-db-instances \
--query "DBInstances[*].ReadReplicaDBInstanceIdentifiers"
```

---

# Step 19: View Logs

```bash
aws rds describe-db-log-files \
--db-instance-identifier studentdb
```

---

# Common AWS CLI Commands

| Command                                        | Purpose                |
| ---------------------------------------------- | ---------------------- |
| `aws rds describe-db-instances`                | List databases         |
| `aws rds create-db-instance`                   | Create RDS instance    |
| `aws rds modify-db-instance`                   | Modify database        |
| `aws rds reboot-db-instance`                   | Reboot database        |
| `aws rds stop-db-instance`                     | Stop database          |
| `aws rds start-db-instance`                    | Start database         |
| `aws rds create-db-snapshot`                   | Create snapshot        |
| `aws rds restore-db-instance-from-db-snapshot` | Restore database       |
| `aws rds delete-db-instance`                   | Delete database        |
| `aws rds describe-db-engine-versions`          | List supported engines |

---

# Best Practices

* Use **IAM roles** instead of long-term access keys where possible.
* Never hard-code AWS credentials in scripts.
* Store secrets securely using **AWS Secrets Manager**.
* Enable automated backups before making major changes.
* Use descriptive names for database instances and snapshots.
* Monitor RDS resources with **Amazon CloudWatch**.
* Test CLI commands in a development environment before running them in production.

---

# Summary

The AWS CLI provides a powerful and efficient way to manage Amazon RDS resources from the command line. It supports creating, modifying, monitoring, backing up, restoring, and deleting databases, making it an essential tool for cloud engineers, system administrators, and DevOps professionals. Mastering these commands helps automate database operations and simplifies infrastructure management.

---

