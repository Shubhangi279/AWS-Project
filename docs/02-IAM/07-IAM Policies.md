# IAM Policies

## Introduction

An **IAM Policy** in AWS Identity and Access Management (IAM) is a JSON document that defines **permissions**.

Policies specify:

* **What actions** are allowed or denied
* **Which resources** can be accessed
* **Under what conditions** access is granted

IAM policies are the **core authorization mechanism** of AWS security.

---

## IAM Policy Architecture Diagram

```text id="9v72lm"
        IAM Policy
            │
 ┌──────────┼──────────┐
 │          │          │
User      Group       Role
            │
       AWS Resources
```

---

## Purpose of IAM Policies

IAM policies control access to AWS services and resources.

Examples:

* Allow developers to start EC2 instances
* Grant read-only access to S3 buckets
* Restrict database deletion
* Enable deployment permissions

Without policies, IAM identities have **no permissions**.

---

## Policy Structure

IAM policies are written in **JSON format**.

### Example Policy

```json id="tv65rm"
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "*"
    }
  ]
}
```

---

## Policy Elements Explained

| Element   | Description             |
| --------- | ----------------------- |
| Version   | Policy language version |
| Statement | Permission rules        |
| Effect    | Allow or Deny           |
| Action    | AWS service operation   |
| Resource  | Target resource         |
| Condition | Optional access rule    |

---

## Types of IAM Policies

### 1️⃣ Managed Policies

Reusable policies.

#### AWS Managed Policies

Created and maintained by AWS.

Example:

* AmazonS3ReadOnlyAccess
* AdministratorAccess

#### Customer Managed Policies

Created by users for custom permissions.

Reusable across multiple identities.

---

### 2️⃣ Inline Policies

Policies directly attached to a single:

* User
* Group
* Role

Not reusable
One-to-one relationship

---

## Policy Evaluation Logic

```text id="o3u19k"
Request → Authentication → Policy Evaluation
        → Explicit Deny?
             │
      Yes → Access Denied
      No  → Allow Permission?
             │
      Yes → Access Granted
```

### Important Rule

**Explicit Deny always overrides Allow.**

---

## Principle of Least Privilege

Always grant only required permissions.

Example:

AdministratorAccess for everyone
Specific EC2 start/stop permission only

---

## Common IAM Policy Use Cases

* Read-only access for analysts
* Deployment permissions for DevOps
* Secure application API access
* Service-to-service communication
* Cross-account authorization

---

## IAM Policy Best Practices

* Use managed policies when possible
* Avoid wildcard `"*"` permissions
* Regularly review permissions
* Apply least privilege principle
* Use conditions for stronger security
* Monitor using AWS CloudTrail

---

## Where Policies Can Be Attached

Policies can be attached to:

* IAM Users
* IAM Groups
* IAM Roles

---

## Benefits of IAM Policies

✔ Fine-grained permission control
✔ Centralized security management
✔ Flexible authorization model
✔ Scalable access control
✔ Strong AWS security foundation

---

## Summary

IAM Policies define **who can do what in AWS**.
They are the backbone of authorization and play a critical role in protecting AWS infrastructure.

---

