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


<img width="1888" height="907" alt="image" src="https://github.com/user-attachments/assets/fdabd3d4-d1eb-4bc1-9b0c-db5b9971bc18" />



---

# Step 2 — Open IAM Service

1. After login, locate **Search Bar**
2. Type:

```
IAM
```

3. Click **IAM – Identity and Access Management**

### Screenshot

<img width="1910" height="910" alt="image" src="https://github.com/user-attachments/assets/2ec47bc0-44f0-4ded-a505-cd1cea5f1bac" />

---

# Step 3 — Open Users Section

1. From left navigation panel
2. Click:

```
Users
```

3. Click **Create User**

### Screenshot

<img width="1911" height="906" alt="image" src="https://github.com/user-attachments/assets/eee5248d-7030-40a9-9de3-6730a1fdceae" />

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

<img width="1905" height="963" alt="image" src="https://github.com/user-attachments/assets/387819b3-a04f-4036-a957-d7ab923b2f00" />

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

<img width="1910" height="907" alt="image" src="https://github.com/user-attachments/assets/69ba057b-ae39-4a13-81e7-de880f93b396" />

---

# Step 6 — Attach Permissions (Policies)

1. Select policy for the group.

Examples:

* AdministratorAccess
* AmazonS3ReadOnlyAccess
* AmazonEC2FullAccess

2. Click **Create Group**

### Screenshot

<img width="1918" height="906" alt="image" src="https://github.com/user-attachments/assets/c3166bad-f890-42a0-8506-4dc6e80d3ebc" />

---

# Step 7 — Add User to Group

1. Select created group
2. Click **Next**

User automatically inherits permissions.

### Screenshot

<img width="1912" height="900" alt="image" src="https://github.com/user-attachments/assets/f27eddb6-bd94-4c00-9685-1d47be78e54f" />

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

<img width="1917" height="910" alt="image" src="https://github.com/user-attachments/assets/f6261f41-6ebf-4a9c-94c3-85aa004678ef" />

---

# Step 9 — Download Login Credentials

AWS provides:

* Console Login URL
* Username
* Password

Download immediately.

### Screenshot

<img width="1912" height="910" alt="image" src="https://github.com/user-attachments/assets/c404328b-7c1e-473c-8ea5-8526aa591afc" />

---

# Step 10 — Login Using IAM User

1. Open IAM login URL
2. Enter:

* Account ID
* Username
* Password

### Screenshot

<img width="1917" height="967" alt="image" src="https://github.com/user-attachments/assets/b1c85c6d-fcb7-4a4c-935a-cace1a5f2845" />

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

<img width="1916" height="913" alt="image" src="https://github.com/user-attachments/assets/99c42e00-1cfc-4925-87d0-5a643278af45" />

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

IAM is the **first security layer** in AWS.

---

