# Working of Amazon EFS

## Overview

Amazon Elastic File System (Amazon EFS) is a fully managed network file system that enables multiple Amazon EC2 instances to access the same shared storage simultaneously. It uses the **Network File System (NFSv4)** protocol to provide secure, scalable, and highly available file storage.

When an EC2 instance reads or writes a file, the request is sent through a **Mount Target** inside the Virtual Private Cloud (VPC). The Mount Target communicates with the EFS file system, where the data is stored across multiple Availability Zones for durability and availability.

---

## Amazon EFS Working Diagram

![Image](https://images.openai.com/static-rsc-4/Roi7VpwfvAQZH1x2mEkLW-FJ-fnHXxCmEO3tMvHZmtqxnCDISVzmDimpAaGLANDVJytUP8ecTY-rWm7JrjQl4qFpXxA9w8etIPGpfvSo6OayzPCBsgbpx0gp9N_mIfuAEIxPxrtsjCJp60tsBIy3Eb8-TzhqHVxcj1GlKgi8eJTjXrTBKG3hL33m_y0GICuL?purpose=fullsize)

---

## Working Architecture

```text
              User
                │
                ▼
      Application Running on EC2
                │
                ▼
       NFS Client (Port 2049)
                │
                ▼
         Amazon EFS Mount Target
                │
                ▼
      Amazon EFS File System
                │
      ┌─────────┼─────────┐
      ▼         ▼         ▼
 Storage    CloudWatch   AWS Backup
```

---

# Step-by-Step Working Process

## Step 1: User Sends a Request

A user accesses an application hosted on an Amazon EC2 instance.

**Example:**

* Uploading an image
* Opening a document
* Saving application logs

---

## Step 2: Application Processes the Request

The application running on the EC2 instance processes the request and determines whether it needs to read or write data.

For example:

* Read a profile image
* Save a PDF document
* Store uploaded files

---

## Step 3: EC2 Uses the NFS Client

The EC2 instance communicates with Amazon EFS using the **NFSv4 protocol**.

Default port:

| Protocol | Port |
| -------- | ---- |
| NFS      | 2049 |

The NFS client sends the request securely to the Mount Target.

---

## Step 4: Request Reaches the Mount Target

A **Mount Target** acts as the network entry point for Amazon EFS within the VPC.

Responsibilities:

* Accept requests from EC2 instances
* Authenticate network access
* Forward requests to the EFS file system

Each Availability Zone should have its own Mount Target to improve availability and reduce latency.

---

## Step 5: Amazon EFS Stores or Retrieves Data

The EFS file system performs the requested operation.

### Read Operation

* Locates the requested file
* Sends it back through the Mount Target to the EC2 instance

### Write Operation

* Stores the new file
* Automatically replicates data across multiple Availability Zones

---

## Step 6: Data Is Shared Across Multiple EC2 Instances

Since Amazon EFS provides shared storage, multiple EC2 instances can access the same files at the same time.

Example:

```text
EC2-1  ─┐
EC2-2  ─┼──► Amazon EFS
EC2-3  ─┘
```

If one instance uploads a file, all other connected instances can immediately access it.

---

## Step 7: Monitoring and Backup

While the file system is in use:

* **Amazon CloudWatch** monitors storage usage, throughput, and client connections.
* **AWS Backup** creates scheduled backups to protect against accidental data loss.

---

# Data Flow

```text
User
 │
 ▼
Application (EC2)
 │
 ▼
NFS Client
 │
 ▼
Mount Target
 │
 ▼
Amazon EFS
 │
 ├── Store File
 ├── Retrieve File
 ├── Replicate Data
 └── Monitor & Backup
```

---

# Example Scenario

Imagine a company hosts a photo-sharing website.

1. A user uploads a photo.
2. The EC2 web server receives the upload.
3. The server sends the file to Amazon EFS using NFS.
4. Amazon EFS stores the file.
5. The file becomes instantly available to all other EC2 instances serving the website.
6. CloudWatch monitors usage, and AWS Backup protects the stored data.

---

# Advantages of the Working Model

* Shared storage across multiple EC2 instances
* Automatic storage scaling
* High availability with Multi-AZ architecture
* Low-latency file access
* Secure communication through VPC and Security Groups
* Continuous monitoring with CloudWatch
* Automated backups with AWS Backup

---

# Summary

Amazon EFS works by allowing EC2 instances to access a centralized file system through **Mount Targets** using the **NFSv4 protocol**. Files are automatically stored, replicated, and shared across multiple Availability Zones, providing a highly available, scalable, and secure storage solution. This architecture is ideal for web applications, content management systems, analytics workloads, and shared development environments.

---
