# AWS CLI Commands for EC2 Auto Scaling

## Overview

The **AWS Command Line Interface (AWS CLI)** is a unified tool that allows you to manage AWS services directly from the terminal or command prompt. It enables automation, scripting, and infrastructure management without using the AWS Management Console.

This guide covers the most commonly used AWS CLI commands for **Amazon EC2 Auto Scaling**, including creating Launch Templates, Auto Scaling Groups, Scaling Policies, and monitoring scaling activities.

---

# AWS CLI Workflow

![Image](https://images.openai.com/static-rsc-4/LR7XNCPvH6MjLjMJdb4vcxCkIm01b8vAJ6HSqz-tEaOrxoA4c4H5rRadeUBj-PPmfn708wc5OvvjW4Jo8lM6SllFqItQKXc_C5KQ3hpCNw4ex7l2Yeufc50y0dZaYBhyGsNsrNtNb-ynaPLpxX9_YZiBX7KGYxV3mH6-y9lQ0wTLzfiJpjFOyrLG17lnMQ0L?purpose=fullsize)

---

# Architecture

```text
                User / Administrator
                         │
                         ▼
                   AWS CLI Terminal
                         │
        ┌────────────────┼────────────────┐
        ▼                ▼                ▼
 Launch Template     Auto Scaling     CloudWatch
        │                │                │
        └────────────────┼────────────────┘
                         ▼
               EC2 Auto Scaling Group
                         │
                  EC2 Instances
```

---

# Prerequisites

Before using AWS CLI:

* Install AWS CLI Version 2
* Configure AWS credentials
* Create an IAM user with required permissions
* Verify installation

---

# 1. Check AWS CLI Version

```bash
aws --version
```

Example Output

```text
aws-cli/2.17.0 Python/3.x Windows/64-bit
```

---

# 2. Configure AWS CLI

```bash
aws configure
```

Example

```text
AWS Access Key ID: AKIA****************
AWS Secret Access Key: ****************
Default region name: ap-south-1
Default output format: json
```

---

# 3. Verify AWS Identity

```bash
aws sts get-caller-identity
```

Example Output

```json
{
    "UserId": "AIDAXXXXXXXXX",
    "Account": "123456789012",
    "Arn": "arn:aws:iam::123456789012:user/Admin"
}
```

---

# Launch Template Commands

## Create Launch Template

```bash
aws ec2 create-launch-template \
--launch-template-name WebServer-Template \
--version-description "Version 1" \
--launch-template-data '{
"ImageId":"ami-xxxxxxxx",
"InstanceType":"t3.micro",
"KeyName":"MyKeyPair",
"SecurityGroupIds":["sg-xxxxxxxx"]
}'
```

---

## Describe Launch Templates

```bash
aws ec2 describe-launch-templates
```

---

## Describe Launch Template Versions

```bash
aws ec2 describe-launch-template-versions \
--launch-template-name WebServer-Template
```

---

## Delete Launch Template

```bash
aws ec2 delete-launch-template \
--launch-template-name WebServer-Template
```

---

# Auto Scaling Group Commands

## Create Auto Scaling Group

```bash
aws autoscaling create-auto-scaling-group \
--auto-scaling-group-name WebServer-ASG \
--launch-template LaunchTemplateName=WebServer-Template \
--min-size 2 \
--max-size 6 \
--desired-capacity 2 \
--vpc-zone-identifier subnet-11111111,subnet-22222222
```

---

## Describe Auto Scaling Groups

```bash
aws autoscaling describe-auto-scaling-groups
```

---

## Update Auto Scaling Group

```bash
aws autoscaling update-auto-scaling-group \
--auto-scaling-group-name WebServer-ASG \
--desired-capacity 3
```

---

## Delete Auto Scaling Group

```bash
aws autoscaling delete-auto-scaling-group \
--auto-scaling-group-name WebServer-ASG \
--force-delete
```

---

# Scaling Policy Commands

## Create Target Tracking Scaling Policy

```bash
aws autoscaling put-scaling-policy \
--auto-scaling-group-name WebServer-ASG \
--policy-name TargetTrackingCPU \
--policy-type TargetTrackingScaling \
--target-tracking-configuration file://tracking.json
```

---

## List Scaling Policies

```bash
aws autoscaling describe-policies \
--auto-scaling-group-name WebServer-ASG
```

---

## Delete Scaling Policy

```bash
aws autoscaling delete-policy \
--auto-scaling-group-name WebServer-ASG \
--policy-name TargetTrackingCPU
```

---

# CloudWatch Commands

## List Metrics

```bash
aws cloudwatch list-metrics
```

---

## Describe Alarms

```bash
aws cloudwatch describe-alarms
```

---

## Create CPU Alarm

```bash
aws cloudwatch put-metric-alarm \
--alarm-name HighCPUAlarm \
--metric-name CPUUtilization \
--namespace AWS/EC2 \
--statistic Average \
--period 300 \
--threshold 70 \
--comparison-operator GreaterThanThreshold \
--evaluation-periods 2
```

---

# EC2 Commands

## Launch an EC2 Instance

```bash
aws ec2 run-instances \
--launch-template LaunchTemplateName=WebServer-Template
```

---

## Describe EC2 Instances

```bash
aws ec2 describe-instances
```

---

## Stop an Instance

```bash
aws ec2 stop-instances \
--instance-ids i-0123456789abcdef0
```

---

## Start an Instance

```bash
aws ec2 start-instances \
--instance-ids i-0123456789abcdef0
```

---

## Terminate an Instance

```bash
aws ec2 terminate-instances \
--instance-ids i-0123456789abcdef0
```

---

# Load Balancer Commands

## Describe Load Balancers

```bash
aws elbv2 describe-load-balancers
```

---

## Describe Target Groups

```bash
aws elbv2 describe-target-groups
```

---

## Register Target

```bash
aws elbv2 register-targets \
--target-group-arn arn:aws:elasticloadbalancing:... \
--targets Id=i-0123456789abcdef0
```

---

## Deregister Target

```bash
aws elbv2 deregister-targets \
--target-group-arn arn:aws:elasticloadbalancing:... \
--targets Id=i-0123456789abcdef0
```

---

# Monitoring Commands

## View Scaling Activities

```bash
aws autoscaling describe-scaling-activities \
--auto-scaling-group-name WebServer-ASG
```

---

## Describe Instance Health

```bash
aws autoscaling describe-auto-scaling-instances
```

---

## View CloudWatch Metrics

```bash
aws cloudwatch get-metric-statistics \
--namespace AWS/EC2 \
--metric-name CPUUtilization \
--statistics Average \
--period 300 \
--start-time 2026-07-01T00:00:00Z \
--end-time 2026-07-02T00:00:00Z
```

---

# Useful IAM Commands

## List IAM Users

```bash
aws iam list-users
```

---

## List IAM Roles

```bash
aws iam list-roles
```

---

## Attach IAM Role to EC2

```bash
aws ec2 associate-iam-instance-profile \
--instance-id i-0123456789abcdef0 \
--iam-instance-profile Name=EC2Role
```

---

# Complete Auto Scaling Workflow Using CLI

```text
Configure AWS CLI
        │
        ▼
Create Launch Template
        │
        ▼
Create Auto Scaling Group
        │
        ▼
Create Scaling Policy
        │
        ▼
Create CloudWatch Alarm
        │
        ▼
Launch EC2 Instances
        │
        ▼
Monitor Metrics
        │
        ▼
Scale Out / Scale In
```

---

# Common AWS CLI Commands Summary

| Service            | Command                                       |
| ------------------ | --------------------------------------------- |
| AWS CLI Version    | `aws --version`                               |
| Configure CLI      | `aws configure`                               |
| Identity           | `aws sts get-caller-identity`                 |
| Launch Template    | `aws ec2 create-launch-template`              |
| Auto Scaling Group | `aws autoscaling create-auto-scaling-group`   |
| Scaling Policy     | `aws autoscaling put-scaling-policy`          |
| CloudWatch Alarm   | `aws cloudwatch put-metric-alarm`             |
| Launch EC2         | `aws ec2 run-instances`                       |
| Describe EC2       | `aws ec2 describe-instances`                  |
| Scaling Activities | `aws autoscaling describe-scaling-activities` |

---

# Best Practices

* Install the latest **AWS CLI v2**.
* Use **IAM roles** instead of hardcoding credentials.
* Store configuration files securely.
* Use **JSON or YAML** files for complex CLI commands.
* Test CLI commands in a non-production environment first.
* Use descriptive names for Launch Templates, ASGs, and Scaling Policies.
* Monitor activities using **CloudWatch** and **Auto Scaling Activity History**.

---

# Real-World Example

A DevOps engineer automates the deployment of a web application using AWS CLI:

1. Creates a **Launch Template** with Amazon Linux and Apache installed.
2. Creates an **Auto Scaling Group** spanning two Availability Zones.
3. Configures a **Target Tracking Scaling Policy** to maintain 50% CPU utilization.
4. Sets a **CloudWatch Alarm** to trigger scaling actions.
5. Uses `describe-scaling-activities` to monitor all scaling events.

This approach enables repeatable, script-based infrastructure deployment and is widely used in CI/CD pipelines.

---

# Conclusion

AWS CLI provides a fast, scriptable, and reliable way to manage Amazon EC2 Auto Scaling resources. By mastering these commands, administrators and DevOps engineers can automate infrastructure provisioning, monitor application health, and efficiently manage cloud resources without relying on the AWS Management Console.

---

