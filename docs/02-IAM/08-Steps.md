# AWS IAM — Step-by-Step Setup Guide

## Introduction

AWS Identity and Access Management (IAM) allows you to securely control access to AWS resources by creating users, groups, roles, and policies.

This guide demonstrates the **complete IAM setup process** from scratch.

---

# Step 1 — Login to AWS Console

1. Open browser
2. Go to:

```
https://console.aws.amazon.com
```

3. Sign in using **Root User**

Root account should only be used for initial setup.

### Screenshot

```md
![AWS Login Page](images/step1-login.png)
```

---

# Step 2 — Open IAM Service

1. After login, locate **Search Bar**
2. Type:

```
IAM
```

3. Click **IAM – Identity and Access Management**

### Screenshot

```md
![IAM Dashboard](images/step2-iam-dashboard.png)
```

---

# Step 3 — Open Users Section

1. From left navigation panel
2. Click:

```
Users
```

3. Click **Create User**

### Screenshot

```md
![Users Section](images/step3-users.png)
```

---

# Step 4 — Create IAM User

1. Enter **User Name**

Example:

```
dev-user
```

2. Select Access Type:

AWS Management Console access
(Optional) Programmatic access

3. Set password option:

* Auto generated password

Click **Next**

### Screenshot

```md
![Create User](images/step4-create-user.png)
```

---

# Step 5 — Create IAM Group (Recommended)

Instead of assigning permissions directly:

1. Click **Create Group**
2. Enter Group Name

Example:

```
Developers
```

### Screenshot

```md
![Create Group](images/step5-create-group.png)
```

---

# Step 6 — Attach Permissions (Policies)

1. Select policy for the group.

Examples:

* AdministratorAccess
* AmazonS3ReadOnlyAccess
* AmazonEC2FullAccess

2. Click **Create Group**

### Screenshot

```md
![Attach Policy](images/step6-attach-policy.png)
```

---

# Step 7 — Add User to Group

1. Select created group
2. Click **Next**

User automatically inherits permissions.

### Screenshot

```md
![Add User To Group](images/step7-add-group.png)
```

---

# Step 8 — Review & Create User

1. Verify:

* Username
* Permissions
* Access type

2. Click:

```
Create User
```

### Screenshot

```md
![Review User](images/step8-review.png)
```

---

# Step 9 — Download Login Credentials

AWS provides:

* Console Login URL
* Username
* Password

Download immediately.

### Screenshot

```md
![Credentials Page](images/step9-credentials.png)
```

---

# Step 10 — Login Using IAM User

1. Open IAM login URL
2. Enter:

* Account ID
* Username
* Password

### Screenshot

```md
![IAM Login](images/step10-user-login.png)
```

---

# Step 11 — Enable MFA (Highly Recommended)

1. Go to:

```
IAM → Users → Security Credentials
```

2. Click:

```
Assign MFA Device
```

3. Scan QR using Authenticator App.

### Screenshot

```md
![Enable MFA](images/step11-mfa.png)
```

---

# IAM Setup Architecture

```text
Root Account
      │
Create IAM Group
      │
Attach Policy
      │
Create IAM User
      │
Add User To Group
      │
Secure AWS Access
```

---

# IAM Best Practices

* Never use Root account daily
* Create IAM users for individuals
* Use groups for permission management
* Enable MFA for all users
* Apply Least Privilege Principle
* Rotate credentials regularly

---

# Summary

IAM setup process:

1. Login AWS
2. Open IAM
3. Create Group
4. Attach Policy
5. Create User
6. Assign Group
7. Download Credentials
8. Enable MFA

👉 IAM is the **first security layer** in AWS.

---

