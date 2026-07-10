# AWS CLI Commands for Elastic Load Balancer (ELB)

## Overview

The **AWS Command Line Interface (AWS CLI)** enables you to create, configure, monitor, and manage **Elastic Load Balancers (ELB)** directly from the terminal. It is widely used by **Cloud Engineers, DevOps Engineers, and System Administrators** to automate infrastructure tasks and manage AWS resources efficiently.

This guide demonstrates how to install and configure the AWS CLI and perform common operations for **Application Load Balancer (ALB)**, **Target Groups**, and **Listeners**.

---

# AWS CLI Workflow

![Image](https://images.openai.com/static-rsc-4/PSeKAAn_BZWBd4YzBiGN-G5m-ojcx39ZsAgMNuz29Dk9HeAG7MkRRBRj404CWo1FSxAHRjFz_sYSwErv1qOHsx_7HxYxHuyPvUyz4TYTdsNebxpUCmNqWE6IhbEYiBL8K5QLbSqXn0TS-d8Jh6TIpCk7P8MfNNij_w2guPElPU3m6-uymvKFi7vgeAx98Tgz?purpose=fullsize)

---

# Prerequisites

Before using AWS CLI with ELB, ensure you have:

* AWS Account
* IAM User with ELB permissions
* AWS CLI installed
* Configured AWS credentials
* Existing Amazon VPC
* Public Subnets
* EC2 Instances
* Security Groups

---

# Step 1: Install AWS CLI

### Windows

Download and install the AWS CLI from the official AWS website.

Verify installation:

```bash
aws --version
```

Example Output

```text
aws-cli/2.17.0 Python/3.12 Windows/11 exe/AMD64
```

📸 **Screenshot 1**

```text
screenshots/22-install-aws-cli.png
```

---

### Amazon Linux

```bash
sudo yum install awscli -y
```

---

### Ubuntu

```bash
sudo apt update
sudo apt install awscli -y
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

Example

```text
AWS Access Key ID: AKIA****************
AWS Secret Access Key: ****************
Default Region: ap-south-1
Output Format: json
```

📸 **Screenshot 2**

```text
screenshots/23-configure-cli.png
```

---

# Step 3: Verify Configuration

```bash
aws sts get-caller-identity
```

Example Output

```json
{
  "Account": "123456789012",
  "Arn": "arn:aws:iam::123456789012:user/admin"
}
```

📸 **Screenshot 3**

```text
screenshots/24-verify-cli.png
```

---

# Step 4: Create a Target Group

```bash
aws elbv2 create-target-group \
--name MyTargetGroup \
--protocol HTTP \
--port 80 \
--vpc-id vpc-0123456789abcdef0 \
--target-type instance
```

Example Output

```json
{
  "TargetGroups": [
    {
      "TargetGroupArn": "arn:aws:elasticloadbalancing:..."
    }
  ]
}
```

📸 **Screenshot 4**

```text
screenshots/25-create-target-group.png
```

---

# Step 5: Register EC2 Instances

```bash
aws elbv2 register-targets \
--target-group-arn arn:aws:elasticloadbalancing:... \
--targets Id=i-0123456789abcdef0
```

📸 **Screenshot 5**

```text
screenshots/26-register-targets.png
```

---

# Step 6: Create an Application Load Balancer

```bash
aws elbv2 create-load-balancer \
--name MyApplicationLB \
--subnets subnet-11111111 subnet-22222222 \
--security-groups sg-12345678 \
--scheme internet-facing \
--type application
```

Example Output

```json
{
  "LoadBalancers": [
    {
      "DNSName": "myapplicationlb.ap-south-1.elb.amazonaws.com"
    }
  ]
}
```

📸 **Screenshot 6**

```text
screenshots/27-create-alb.png
```

---

# Step 7: Create a Listener

```bash
aws elbv2 create-listener \
--load-balancer-arn arn:aws:elasticloadbalancing:... \
--protocol HTTP \
--port 80 \
--default-actions Type=forward,TargetGroupArn=arn:aws:elasticloadbalancing:...
```

📸 **Screenshot 7**

```text
screenshots/28-create-listener.png
```

---

# Step 8: Describe Load Balancers

```bash
aws elbv2 describe-load-balancers
```

📸 **Screenshot 8**

```text
screenshots/29-describe-load-balancers.png
```

---

# Step 9: Describe Target Groups

```bash
aws elbv2 describe-target-groups
```

📸 **Screenshot 9**

```text
screenshots/30-describe-target-groups.png
```

---

# Step 10: Check Target Health

```bash
aws elbv2 describe-target-health \
--target-group-arn arn:aws:elasticloadbalancing:...
```

Example Output

```text
TargetHealth:
State: healthy
```

📸 **Screenshot 10**

```text
screenshots/31-target-health.png
```

---

# Step 11: Delete Listener

```bash
aws elbv2 delete-listener \
--listener-arn arn:aws:elasticloadbalancing:...
```

---

# Step 12: Delete Load Balancer

```bash
aws elbv2 delete-load-balancer \
--load-balancer-arn arn:aws:elasticloadbalancing:...
```

---

# Step 13: Delete Target Group

```bash
aws elbv2 delete-target-group \
--target-group-arn arn:aws:elasticloadbalancing:...
```

---

# Frequently Used ELB CLI Commands

| Command                             | Purpose                             |
| ----------------------------------- | ----------------------------------- |
| `aws elbv2 create-load-balancer`    | Create an Application Load Balancer |
| `aws elbv2 describe-load-balancers` | List Load Balancers                 |
| `aws elbv2 create-target-group`     | Create a Target Group               |
| `aws elbv2 describe-target-groups`  | List Target Groups                  |
| `aws elbv2 register-targets`        | Register EC2 instances              |
| `aws elbv2 deregister-targets`      | Remove EC2 instances                |
| `aws elbv2 create-listener`         | Create Listener                     |
| `aws elbv2 describe-target-health`  | Check Health Status                 |
| `aws elbv2 delete-load-balancer`    | Delete Load Balancer                |
| `aws elbv2 delete-target-group`     | Delete Target Group                 |

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
Create Target Group
        │
        ▼
Register Targets
        │
        ▼
Create Load Balancer
        │
        ▼
Create Listener
        │
        ▼
Verify Health
        │
        ▼
Delete Resources
```

---

# Best Practices

* Use **IAM Roles** instead of long-term access keys whenever possible.
* Store credentials securely using AWS IAM or AWS Secrets Manager.
* Use meaningful names for Load Balancers and Target Groups.
* Deploy the Load Balancer across multiple Availability Zones.
* Automate deployments using shell scripts, CloudFormation, or Terraform.
* Monitor ELB resources with Amazon CloudWatch.
* Regularly remove unused Load Balancers and Target Groups to reduce costs.

---

# Real-World Example

A DevOps engineer automates the deployment of a production web application using AWS CLI. The script creates a Target Group, registers EC2 instances, provisions an Application Load Balancer, configures a Listener, and verifies target health. This approach enables repeatable, consistent deployments across development, testing, and production environments.

---

# Conclusion

The AWS CLI provides a fast and efficient way to manage Elastic Load Balancer resources. It enables infrastructure automation, simplifies deployments, and integrates seamlessly with DevOps workflows. Learning these commands is valuable for AWS certification preparation, cloud administration, and real-world production environments.

---

