# IAM Groups

## Introduction

An **IAM Group** in AWS Identity and Access Management (IAM) is a collection of IAM users that share the same permissions.

Instead of assigning permissions individually to every user, IAM Groups allow administrators to manage access **efficiently and consistently**.

Permissions are attached to the **group**, and all users inside the group automatically inherit those permissions.

---

## IAM Group Architecture Diagram

```text id="k92xpe"
              AWS Account
                   │
               IAM Group
        ┌──────────┼──────────┐
        │          │          │
      User1      User2      User3
                   │
              Attached Policy
                   │
              AWS Resources
```

---

## Purpose of IAM Groups

IAM Groups simplify permission management by organizing users based on job roles.

Common examples:

* Developers Group
* DevOps Team
* Administrators
* ReadOnly Users
* Finance Team

---

## How IAM Groups Work

1. Create an IAM Group
2. Attach permission policies to the group
3. Add IAM users to the group
4. Users automatically receive group permissions

One change updates permissions for all users.

---

## Permissions in IAM Groups

Permissions are defined using **IAM Policies**.

Policies attached to a group determine:

* Allowed actions
* Accessible resources
* Security conditions

Example Policy:

```json id="8y9zmk"
{
  "Effect": "Allow",
  "Action": "ec2:DescribeInstances",
  "Resource": "*"
}
```

---

## IAM Group Best Practices

* Assign permissions to groups instead of users
* Organize users based on responsibilities
* Follow the least privilege principle
* Avoid granting administrator access unnecessarily
* Regularly review group membership

---

## IAM Users vs IAM Groups

| Feature               | IAM User            | IAM Group           |
| --------------------- | ------------------- | ------------------- |
| Represents            | Individual identity | Collection of users |
| Permission Assignment | Direct              | Shared              |
| Management            | Harder at scale     | Easy & centralized  |
| Best Use              | Specific access     | Role-based access   |

---

## Real-World Use Cases

* Developers accessing EC2 & S3 resources
* QA team with read-only permissions
* Admin team managing infrastructure
* Finance users accessing billing dashboards

---

## Benefits of IAM Groups

✔ Centralized permission management
✔ Reduced administrative effort
✔ Consistent security policies
✔ Scalable user access control

---

## Summary

IAM Groups help organizations manage AWS access efficiently by assigning permissions to multiple users at once, improving both security and operational simplicity.

