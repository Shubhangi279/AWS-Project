# AWS IAM Architecture Overview

## Introduction

The **AWS Identity and Access Management (IAM) Architecture** defines how identities, permissions, and AWS resources interact securely inside an AWS account.

IAM ensures that only authorized users and services can access AWS resources by using **authentication** and **authorization mechanisms**.

---

## IAM Architecture Diagram

```text
          AWS Account
               │
 ┌─────────────┼─────────────┐
 │             │             │
Users        Groups         Roles
 │             │             │
 └────────── Policies ──────────┘
               │
        AWS Resources
```
<img width="2175" height="1333" alt="image" src="https://github.com/user-attachments/assets/63f61159-2aaf-42b3-8207-bcd643178a10" />


---

## Architecture Components

---

### 1. AWS Account

The AWS Account acts as the **security boundary**.

It contains:

* IAM users
* IAM groups
* IAM roles
* Policies
* AWS services and resources

Every action performed inside AWS belongs to an account.

---

### 2. IAM Users

IAM Users represent individual identities.

Examples:

* Developers
* Administrators
* Applications

Each user receives:

* Login credentials
* Access keys
* Assigned permissions

Users authenticate to AWS before accessing resources.

---

### 3. IAM Groups

IAM Groups organize multiple users.

Instead of assigning permissions individually:

Attach policies to groups
Add users to the group

Example Groups:

* Developers
* DevOps Team
* ReadOnly Users

This simplifies permission management.

---

### 4. IAM Roles

IAM Roles provide **temporary access permissions**.

Roles are assumed by:

* AWS services (EC2, Lambda)
* Applications
* External accounts
* GitHub Actions / CI-CD pipelines

Key Advantage:
No long-term credentials required.

---

### 5. IAM Policies

Policies define **what actions are allowed or denied**.

Policies are JSON documents that specify:

* Allowed actions
* Target resources
* Permission effects

Example Policy:

```json
{
  "Effect": "Allow",
  "Action": "ec2:StartInstances",
  "Resource": "*"
}
```

Policies can be attached to:

* Users
* Groups
* Roles

---

### 6. AWS Resources

Resources are AWS services accessed through IAM permissions.

Examples:

* Amazon EC2
* Amazon S3
* AWS Lambda
* RDS Databases

IAM evaluates policies before granting access.

---

## IAM Permission Flow

1. Identity sends request
2. IAM authenticates identity
3. Policies are evaluated
4. Permission granted or denied
5. Resource accessed securely

---

## Key Security Principle

**Least Privilege Access**

Users receive only the permissions required to perform their tasks — nothing more.

---

## Architecture Benefits

* Centralized access management
* Secure cloud environment
* Scalable permission system
* Reduced security risks
* Easy administration

---

## Summary

AWS IAM Architecture connects **identities**, **permissions**, and **resources** inside an AWS account, forming the backbone of AWS security.

---

