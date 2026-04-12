# IAM Roles

## Introduction

An **IAM Role** in AWS Identity and Access Management (IAM) is an identity that provides **temporary permissions** to access AWS resources.

Unlike IAM Users, a role **does not have permanent credentials**.
Instead, trusted entities **assume the role** to obtain temporary security credentials.

IAM Roles are widely used for secure service-to-service communication and automation.

---

## IAM Role Architecture Diagram

```text id="3qv1pn"
        Trusted Entity
 (User / AWS Service / App)
                │
           Assume Role
                │
            IAM Role
                │
        Temporary Credentials
                │
          AWS Resources
```

---

## Purpose of IAM Roles

IAM Roles allow secure access without sharing long-term credentials.

Common purposes:

* AWS services accessing other AWS services
* Cross-account access
* Temporary user access
* CI/CD deployments
* External application authentication

---

## How IAM Roles Work

1. Create an IAM Role
2. Define **Trusted Entity** (who can assume the role)
3. Attach permission policies
4. Entity assumes role
5. AWS provides temporary credentials

These credentials automatically expire.

---

## Key Components of an IAM Role

### 1️⃣ Trusted Entity (Trust Policy)

Defines **who can assume the role**.

Examples:

* EC2 instance
* Lambda function
* Another AWS account
* GitHub Actions

---

### 2️⃣ Permission Policy

Defines **what actions are allowed**.

Example policy:

```json id="g5n72x"
{
  "Effect": "Allow",
  "Action": "s3:GetObject",
  "Resource": "*"
}
```

---

### 3️⃣ Temporary Security Credentials

When a role is assumed, AWS Security Token Service (STS) provides:

* Temporary Access Key
* Secret Access Key
* Session Token

Automatically rotated
More secure than static credentials

---

## IAM Role Assumption Flow

```text id="rxn41p"
Service/User → Request Role → IAM Validation
            → Temporary Credentials Issued
            → Access AWS Resource
```

---

## Common IAM Role Use Cases

### EC2 Accessing S3

Attach a role to an EC2 instance instead of storing keys.

---

### Lambda Execution Role

Allows Lambda functions to:

* Write logs
* Access databases
* Read S3 objects

---

### Cross-Account Access

One AWS account securely accesses resources in another account.

---

### GitHub Actions Deployment

CI/CD pipelines assume IAM roles for secure AWS deployments.

---

## IAM Users vs IAM Roles

| Feature        | IAM User  | IAM Role              |
| -------------- | --------- | --------------------- |
| Credentials    | Permanent | Temporary             |
| Login Identity | Yes       | No                    |
| Best For       | Humans    | Services & automation |
| Security Level | Good      | Very High             |

---

## IAM Role Security Best Practices

* Use roles instead of access keys
* Grant least privilege permissions
* Limit role session duration
* Use MFA for role assumption
* Regularly audit role permissions

---

## Benefits of IAM Roles

✔ No long-term credentials
✔ Enhanced security
✔ Automatic credential rotation
✔ Ideal for automation & DevOps
✔ Supports cross-account access

---

## Summary

IAM Roles provide secure, temporary access to AWS resources without exposing permanent credentials, making them essential for modern cloud security and automation workflows.

---

