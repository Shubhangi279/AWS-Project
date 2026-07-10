# Amazon EFS Security

## Overview

Security is a fundamental aspect of Amazon Elastic File System (Amazon EFS). AWS provides multiple layers of security to protect your file system from unauthorized access, including **Amazon VPC**, **Security Groups**, **IAM**, **File System Policies**, **Access Points**, and **encryption**. Together, these features ensure that only authorized users and applications can access your data while keeping it secure both at rest and during transmission.

---

# Amazon EFS Security Architecture

![Image](https://images.openai.com/static-rsc-4/dliSYt1agCJfan-sb9hhaR8WBMXsayGF16EpxmrjvstHHF2oCUxh4dVQRHWG1SE1LdfaYWRqsLVjeN-r31OQjI8ubgrMTdbVIwVGiud1r63osEllJjV0ySUED194SDsRC2adT7__boPJQFoEY2yTyzchAYZlgUmv1JmAogMQpc3fEnHGpuk-rBfwU_N9eiUs?purpose=fullsize)

---

# Security Layers in Amazon EFS

```text
                     IAM Users / Roles
                            │
                            ▼
                   File System Policy
                            │
                            ▼
                     Amazon VPC
                            │
                     Security Group
                   (TCP Port 2049)
                            │
                            ▼
                    Mount Target (EFS)
                            │
                            ▼
                   Amazon EFS File System
                  ┌──────────┴──────────┐
                  ▼                     ▼
          AWS KMS Encryption      TLS Encryption
             (At Rest)            (In Transit)
```

---

# 1. Amazon VPC Security

## Overview

Amazon EFS is created inside an **Amazon Virtual Private Cloud (VPC)**. This ensures that communication between EC2 instances and EFS occurs over a private AWS network instead of the public internet.

### Benefits

* Private communication
* Network isolation
* Improved security
* Reduced exposure to external threats

---

# 2. Security Groups

## Overview

Security Groups act as virtual firewalls that control inbound and outbound traffic to Amazon EFS Mount Targets.

### Required Inbound Rule

| Type | Protocol | Port | Source             |
| ---- | -------- | ---- | ------------------ |
| NFS  | TCP      | 2049 | EC2 Security Group |

### Why Port 2049?

Amazon EFS uses the **Network File System (NFS)** protocol, which communicates over **TCP Port 2049**.

### Best Practices

* Allow access only from trusted EC2 Security Groups.
* Avoid using **0.0.0.0/0** as the source.
* Follow the principle of least privilege.

---

# 3. AWS Identity and Access Management (IAM)

## Overview

IAM controls who can create, modify, or delete Amazon EFS resources.

### Common IAM Permissions

* `elasticfilesystem:CreateFileSystem`
* `elasticfilesystem:DeleteFileSystem`
* `elasticfilesystem:DescribeFileSystems`
* `elasticfilesystem:CreateMountTarget`
* `elasticfilesystem:CreateAccessPoint`

### Benefits

* Fine-grained access control
* Role-based permissions
* Secure administration

---

# 4. File System Policies

## Overview

File System Policies are resource-based policies that define who can access a specific EFS file system.

### Example Policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::123456789012:role/EFSRole"
      },
      "Action": [
        "elasticfilesystem:ClientMount",
        "elasticfilesystem:ClientWrite"
      ],
      "Resource": "*"
    }
  ]
}
```

### Benefits

* Restrict client access
* Control mount permissions
* Improve security

---

# 5. Access Points

## Overview

Access Points provide application-specific access to an EFS file system by enforcing a specific directory and user identity.

### Benefits

* Application isolation
* Simplified permissions
* Secure access for containers and applications
* Reduced risk of accidental file access

---

# 6. Encryption at Rest

## Overview

Amazon EFS supports encryption at rest using **AWS Key Management Service (AWS KMS)**.

### Benefits

* Protects stored data
* Encrypts metadata
* Meets compliance requirements

### Supported Keys

* AWS-managed KMS keys
* Customer-managed KMS keys

---

# 7. Encryption in Transit

## Overview

Data transferred between EC2 and EFS can be encrypted using **Transport Layer Security (TLS)**.

### Benefits

* Protects against data interception
* Secure network communication
* Recommended for production environments

Example Mount Command

```bash
sudo mount -t efs -o tls fs-0123456789abcdef0:/ /mnt/efs
```

---

# 8. POSIX File Permissions

## Overview

Amazon EFS supports standard Linux POSIX permissions.

### Permission Types

* Read (r)
* Write (w)
* Execute (x)

Example

```bash
chmod 755 project
```

```bash
chown ec2-user:ec2-user project
```

### Benefits

* Familiar Linux permission model
* Fine-grained file access control

---

# 9. Monitoring with Amazon CloudWatch

## Overview

Amazon CloudWatch monitors EFS performance and security-related metrics.

### Common Metrics

* Client Connections
* Storage Size
* Throughput
* Burst Credit Balance
* Read/Write Operations

### Benefits

* Performance monitoring
* Early issue detection
* Operational visibility

---

# 10. AWS Backup

## Overview

AWS Backup protects Amazon EFS by creating scheduled backups.

### Benefits

* Automated backups
* Centralized backup management
* Disaster recovery
* Long-term retention

---

# Security Best Practices

* Deploy EFS inside a private VPC.
* Restrict **TCP Port 2049** using Security Groups.
* Use **IAM roles** instead of long-term access keys.
* Enable **AWS KMS** encryption at rest.
* Enable **TLS encryption** for data in transit.
* Use **Access Points** for application-specific access.
* Apply the **principle of least privilege**.
* Monitor activity with **CloudWatch**.
* Enable automated backups using **AWS Backup**.
* Regularly audit IAM policies and file system permissions.

---

# Security Checklist

| Security Feature      | Status |
| --------------------- | ------ |
| VPC Isolation         | ✅      |
| Security Groups       | ✅      |
| IAM Access Control    | ✅      |
| File System Policy    | ✅      |
| Access Points         | ✅      |
| Encryption at Rest    | ✅      |
| Encryption in Transit | ✅      |
| POSIX Permissions     | ✅      |
| CloudWatch Monitoring | ✅      |
| AWS Backup            | ✅      |

---

# Real-World Example

A healthcare organization stores patient records on Amazon EFS.

* The EFS file system is deployed in a **private VPC**.
* Only EC2 instances running the healthcare application can access it through a dedicated Security Group.
* Data is encrypted using **AWS KMS**.
* Communication between EC2 and EFS is protected with **TLS**.
* IAM roles restrict administrative actions.
* Daily backups are managed by **AWS Backup**, while **CloudWatch** monitors storage usage and client connections.

This layered security approach helps protect sensitive medical data and supports compliance requirements.

---

# Conclusion

Amazon EFS provides multiple layers of security, including VPC isolation, Security Groups, IAM, File System Policies, Access Points, encryption, monitoring, and backups. By combining these features and following AWS security best practices, organizations can build secure, reliable, and scalable shared storage solutions for production workloads.

---

## 📂 Images Folder

```text
images/
└── security.png
```

---

