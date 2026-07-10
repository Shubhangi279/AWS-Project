# Amazon EFS Components

## Overview

Amazon Elastic File System (Amazon EFS) consists of several key components that work together to provide a scalable, secure, and highly available shared file storage solution. Understanding these components is essential for designing, deploying, and managing EFS effectively.

---

# Amazon EFS Architecture Components

![Image](https://images.openai.com/static-rsc-4/570wJhCf-70XZWFHPleBPlj-XzkyRRi7BMD9_nGyjIR8qaQYG3wDKKpEA3xF7ZnwhIRqACb4bVNAeDs0Z_a5eFiqi4xL6H1eoC1maPzTR9-3-5a8bnm7KzNCQ3DqC1zwcMZ3xnXRtDfoVuFzgE5uNj9ZodTUzwV9m4sUMvOewkdOvROnPNh1kBAiGKsG66Di?purpose=fullsize)

---

# 1. File System

![Image](https://images.openai.com/static-rsc-4/mmEWtJFoD2unp71na2pU9BKkIvkXcQ-CZNGTCEJXNj471Zt5E-eqb8Qy5oxXNDTgxVDR4HZ109olV7f8QgMcFbzvApbcL3eFmReJSASqtXvVUruUf47c9kO3srpITrStNzyrJHM63BH3CPoBODCjA3YdJ0LdcKvGSs6J_-NCN_HNOSK10unmY0-N-91WgCYc?purpose=fullsize)


## Overview

A **File System** is the primary storage resource in Amazon EFS. It stores files and directories that can be accessed by multiple EC2 instances simultaneously.

### Features

* Shared storage
* Automatically scales
* Supports Linux file permissions
* Accessible from multiple clients

### Example

```text
/project
│── app.py
│── images/
│── uploads/
│── logs/
```

---

# 2. Mount Target

![Image](https://images.openai.com/static-rsc-4/2dGzKzzGUYNyk0DkF8H0YvSE96afPal2JkO1WNFhfoVnP58_hGoJ4NU-IXpaYuNmxbimyFFuHC8_gjjXw-BIoJSSbw3MLZtVPnKgCqhH4uWw5V6jzAqki64KRfHRf3gpzXkbpbcRIQmEqkFuBcedgq_8EBednf4AMzuuJ60lfL-zIIw2yGm_h1t4Kre_-A4n?purpose=fullsize)

## Overview

A **Mount Target** is a network endpoint created in a subnet of your VPC. It allows EC2 instances to connect to the EFS file system using the NFS protocol.

### Features

* One mount target per Availability Zone
* Uses private IP addresses
* Improves availability
* Provides secure network access

### Example

```text
EC2
   │
   ▼
Mount Target
   │
   ▼
Amazon EFS
```

---

# 3. Amazon VPC

![Image](https://images.openai.com/static-rsc-4/NJFHbD9e7qADoR_za3hlYE7q6kg0ogmFx7Nwi7iC0JAI1T2fdjJVI5njrW8eI8zsr6Snf8H6LP7WVS7jWv45-oKHurRBivlwCfWBCScLJPZI4rasSQQwktU_OdHSdKWZcIHRMNarFcLIZEQ7KIAF8iIkhiqS93s08It3eFZWPr8s1rxL3SoVAM8gZNuNxugP?purpose=fullsize)

## Overview

Amazon EFS is deployed within an **Amazon VPC**, ensuring secure communication between EC2 instances and the file system.

### Benefits

* Private networking
* Network isolation
* Secure communication
* Integration with Security Groups

---

# 4. Availability Zones (AZs)

![Image](https://images.openai.com/static-rsc-4/2dGzKzzGUYNyk0DkF8H0YvSE96afPal2JkO1WNFhfoVnP58_hGoJ4NU-IXpaYuNmxbimyFFuHC8_gjjXw-BIoJSSbw3MLZtVPnKgCqhH4uWw5V6jzAqki64KRfHRf3gpzXkbpbcRIQmEqkFuBcedgq_8EBednf4AMzuuJ60lfL-zIIw2yGm_h1t4Kre_-A4n?purpose=fullsize)


## Overview

Amazon EFS stores data across multiple Availability Zones within a Region.

### Benefits

* High availability
* Fault tolerance
* Automatic replication
* Disaster resilience

---

# 5. Security Groups

![Image](https://images.openai.com/static-rsc-4/ZyfzREjDdL7Lru_nj9Of6ScsaW0C7Pw4ImQjadFNu6bUrOSUfdKlqfqcn6rqbC7jVeYA4eZY2J1hSsyb2YkTl7UoNL-XEN5KEL3pC49LSf7fX80jC6leJM1Lr7MgJh4FZF_LAW8ZZbaFdifsDbXghurwugZFd1N64OeNxFkpBmZ8Yu0nlRCHDu4y6ZMGgNox?purpose=fullsize)

## Overview

Security Groups control network access to EFS.

### Common Rule

| Protocol | Port | Source             |
| -------- | ---- | ------------------ |
| NFS      | 2049 | EC2 Security Group |

### Benefits

* Restricts access
* Improves security
* Controls inbound traffic

---

# 6. NFS Client

![Image](https://images.openai.com/static-rsc-4/Od_Dz6lUunj7k9XlmzJSDfJmhQ8ySTTxbn2VU6UQaX8rj8ZyKQ-6us-yTMsGNl3RYcGCFg-8ZeKxLpikhGR1LR54w2ElyjU8zC14lBb3R8mGgmN8U0Z53O6M9FdTseq7_nTyig-J7nKaWYPiLP387ywL5fBu0BkKVE03pMFXTK2f1ZrX-7wGfIBErtd_V8a2?purpose=fullsize)

## Overview

A **Network File System (NFS) Client** is installed on Linux EC2 instances to mount the EFS file system.

### Example Commands

```bash
sudo yum install amazon-efs-utils -y
```

Mount EFS:

```bash
sudo mount -t efs fs-12345678:/ /mnt/efs
```

---

# 7. Access Points

![Image](https://images.openai.com/static-rsc-4/-KDGDJd8aVyhFkk-yhwcOp4b93zFiKWkAxoFngVIWzRCjsvL8yBODw5HDU8m6A18d0qm1aZXANoWOd3_YikvmUX6uIpBaypWlvne-8KT75klbFlrg64_1TpcBSaM1Pt14C5GaFhmkaoFBIB-VcHXFbJXCUc8Oig_W3f12LQAHnfCuHDL-mhuaQ5kxyJyNc5Z?purpose=fullsize)


## Overview

An **Access Point** provides a customized entry point into an EFS file system with specific permissions and directories.

### Features

* Directory-level access
* User identity enforcement
* Simplified permissions
* Secure application access

---

# 8. Performance Modes

![Image](https://images.openai.com/static-rsc-4/SI574gnB_zrCWQf4czdsIqIc_O4a0ffuOydguMO42mgS71g3Paq9ntxDZj5tSGGQAqvNd6GaUpen44K5XooT7ydX7DM9ohRJmAH52qshm2pkXcxXSpk9nBknrt5uOWN9ULsh9XctNr1hKPKigYgvOuWrrpG3y9NwqMZSZV6wNFjvkm_ZAaKf9MW3tTuQX_f0?purpose=fullsize)


Amazon EFS supports two performance modes:

| Mode            | Best For                       |
| --------------- | ------------------------------ |
| General Purpose | Low-latency applications       |
| Max I/O         | Large-scale parallel workloads |

---

# 9. Throughput Modes

![Image](https://images.openai.com/static-rsc-4/4kFHIg-J6dLWrh5ZT7sDjDaon2HVhmpfo37y-JntX5rDbA_rNm3IxEFjd-XAZwhg-xRRx58NLQH9_KccNR-vn97cKW85I7hVcWx82KOAo6GUMoiawfZul4ePwoLFe8IWSeiYADOb9suQxVJvaN3d7T7ecY8dwVHltiFRs-MD7jfu4t61FD_jHi19nS-q_25L?purpose=fullsize)


Amazon EFS offers three throughput modes:

| Mode        | Description                                        |
| ----------- | -------------------------------------------------- |
| Bursting    | Throughput scales with storage size                |
| Provisioned | Fixed throughput for predictable workloads         |
| Elastic     | Automatically adjusts throughput based on workload |

---

# 10. Storage Classes

![Image](https://images.openai.com/static-rsc-4/Pup3f_pbM2kUrFD6UQDBIzSHROfBbJufxKilEbadsnMfneSTLbPI587uDAqam_E1lnsuLlgGNMI8yvH6hMXZz98YW_Np0PlwqEaVAeKKp8au3kkUq3NdsmKuMV853mcE5XWE5SPk82Z2rQ9uhfEZE-4EvtS06_08efVOPtqTy_XpIYMg3n0TXowwGw2rzWsi?purpose=fullsize)


Amazon EFS provides multiple storage classes:

| Storage Class | Use Case                    |
| ------------- | --------------------------- |
| Standard      | Frequently accessed files   |
| Standard-IA   | Infrequently accessed files |
| Archive       | Long-term data retention    |

---

# 11. AWS Backup

![Image](https://images.openai.com/static-rsc-4/u_Kp9BPikof6VQGsc93DmPubtn-7_JfPZ7PooQ04UVouKQQ_3KvcDV4cshFasB-X5xHg-KYOzYI2FL1hWpTkVkzIkRzYWQKHw0gAikq4oiITsbok9JBXgSB_XUS3wRGJydJwvBYeV7Qtz_N4warqaE2rZmtgkYlGvtBtLqOp5PIyTUMOFV3V3noFKJOjNLHl?purpose=fullsize)


Amazon EFS integrates with **AWS Backup** for centralized backup management.

### Benefits

* Automated backups
* Policy-based scheduling
* Easy data recovery

---

# 12. Amazon CloudWatch

![Image](https://images.openai.com/static-rsc-4/EdyZ3Yz0y6mwi0CZJzyF6GhAiCOOFxdTuvRXzEo8PIkw1LUULF_71VGy08BUR-nIEJ-XWLoDP8gX4vJzSRSc4RFNUgFsfvOJTSOaIJCm33101IEC-atZ61KBZk2wHTCvSnP9tHqUWTTYp6bHnZxOX1SV-w9RhktBhq5z_53tJtGqVUNxjHDmUZFE_2HqLzC_?purpose=fullsize)

CloudWatch monitors EFS performance and health.

### Common Metrics

* Burst Credit Balance
* Storage Size
* Client Connections
* Data Read/Write
* Throughput

---

# 13. AWS Identity and Access Management (IAM)

![Image](https://images.openai.com/static-rsc-4/6y8L7aXFhLCCL5nOLPmlrVms-eOrpvmsvuHS7HRZ4f1Oka_YaL_Hx-j7rfEBrrR4onjJwvf4NZx_3rKA5TWp5xEbx7ShPfjLQmXRK2cRQRRaIJEW0h6jmcO-t1x7uFHO8oVTvSKOlo14chKi8S8k_cTSv_vi-d4OeJcBSuC66Ix2Xq9HEIDBo8HYEUTEoHrY?purpose=fullsize)

IAM controls access to EFS resources.

### Features

* User authentication
* Role-based access control
* Fine-grained permissions

---

# Component Relationship Diagram

```text
                 User
                   │
                   ▼
            Amazon EC2 Instance
                   │
            Security Group
                   │
              NFS Client
                   │
             Mount Target
                   │
         Amazon EFS File System
          ┌────────┼────────┐
          ▼        ▼        ▼
     Access    Storage   Backup
     Points    Classes   (AWS Backup)
          │
          ▼
     CloudWatch
      Monitoring
```

---

# Summary Table

| Component          | Purpose                             |
| ------------------ | ----------------------------------- |
| File System        | Stores shared files and directories |
| Mount Target       | Network endpoint for EFS access     |
| VPC                | Provides secure networking          |
| Availability Zones | High availability and durability    |
| Security Groups    | Control network access              |
| NFS Client         | Mounts EFS on Linux instances       |
| Access Points      | Application-specific entry points   |
| Performance Modes  | Optimize latency or scalability     |
| Throughput Modes   | Control data transfer performance   |
| Storage Classes    | Reduce storage costs                |
| AWS Backup         | Backup and recovery                 |
| CloudWatch         | Monitoring and metrics              |
| IAM                | Access control and permissions      |

---

# Best Practices

* Create **Mount Targets** in every Availability Zone used by your EC2 instances.
* Restrict NFS traffic (port **2049**) using Security Groups.
* Use **Access Points** for application-specific access.
* Enable **Lifecycle Management** to reduce storage costs.
* Monitor EFS performance with **CloudWatch**.
* Schedule regular backups using **AWS Backup**.
* Use encryption at rest and in transit for sensitive data.

---

# Conclusion

Amazon EFS is built from several integrated components that work together to deliver a secure, scalable, and highly available shared file system. Components such as **Mount Targets**, **Access Points**, **Performance Modes**, **Storage Classes**, **AWS Backup**, and **CloudWatch** make EFS a reliable storage solution for cloud-native applications, enterprise workloads, and shared Linux environments.

---


