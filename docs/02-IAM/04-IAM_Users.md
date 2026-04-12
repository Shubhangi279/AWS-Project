# IAM Users

## Introduction

An **IAM User** in AWS Identity and Access Management (IAM) represents a **person or application** that interacts with AWS services.

Each IAM user has unique security credentials and specific permissions that define what actions they can perform in an AWS account.

IAM Users allow organizations to securely manage access without using the AWS root account.

---

## IAM User Concept Diagram

```text id="w9c81y"
        AWS Account
             │
         IAM User
             │
       Attached Policies
             │
        AWS Resources
```

---

## Purpose of IAM Users

IAM users are created to:

* Provide secure AWS Console access
* Allow programmatic access via APIs
* Assign individual permissions
* Track user activities

Example users:

* Cloud Administrator
* Developer
* DevOps Engineer
* Application service user

---

## IAM User Credentials

Each IAM user can have different authentication methods.

### 1️⃣ AWS Management Console Access

Used for web login.

Includes:

* Username
* Password
* MFA (recommended)

---

### 2️⃣ Programmatic Access

Used by applications or CLI tools.

Credentials include:

* Access Key ID
* Secret Access Key

Used with:

* AWS CLI
* SDKs
* Automation scripts

---

## Permissions for IAM Users

Permissions are not automatically granted.

Access is controlled using **IAM Policies**.

Policies define:

* Allowed actions
* Resources accessed
* Conditions for access

Example:

```json id="p94u1a"
{
  "Effect": "Allow",
  "Action": "s3:ListBucket",
  "Resource": "*"
}
```

---

## IAM Users vs Root User

| Feature            | Root User         | IAM User       |
| ------------------ | ----------------- | -------------- |
| Full Access        |   Yes             |  Limited       |
| Daily Usage        |   Not Recommended |  Recommended   |
| Permission Control |   No restriction  |  Policy based  |
| Security           |   Lower           |  Higher        |

Best Practice: Use IAM users instead of the root account.

---

## IAM User Security Best Practices

* Enable Multi-Factor Authentication (MFA)
* Grant least privilege permissions
* Rotate access keys regularly
* Avoid sharing credentials
* Use IAM groups for permission management
* Disable unused users

---

## Steps to Create an IAM User

1. Open AWS Management Console
2. Navigate to **IAM Service**
3. Select **Users → Create User**
4. Enter username
5. Choose access type
6. Attach permissions or group
7. Review and create user

---

## Common Use Cases

* Developer accessing EC2 instances
* Analyst reading S3 data
* DevOps automation scripts
* Application API access

---

## Advantages of IAM Users

✔ Individual access control
✔ Activity tracking and auditing
✔ Improved security
✔ Scalable user management

---

## Summary

IAM Users provide secure, controlled access to AWS resources by assigning identities with defined permissions, forming an essential part of AWS security architecture.
