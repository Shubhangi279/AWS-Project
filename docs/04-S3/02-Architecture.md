# Amazon S3 — Architecture Overview

## Overview

**Amazon Simple Storage Service (S3)** is an object storage service provided by **Amazon Web Services** that stores data as objects inside buckets and provides secure, scalable, and highly durable cloud storage.

Amazon S3 architecture is designed to allow users and applications to store and retrieve data from anywhere using web-based APIs.

---

## Amazon S3 Architecture Diagram

```
                    ┌──────────────────────┐
                    │      End Users        │
                    │ (Browser / Application)
                    └──────────┬───────────┘
                               │ HTTPS/API
                               ▼
                    ┌──────────────────────┐
                    │   AWS IAM Security    │
                    │ Authentication & Auth │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │      Amazon S3        │
                    │   Object Storage      │
                    └──────────┬───────────┘
                               │
        ┌──────────────────────┼──────────────────────┐
        │                      │                      │
        ▼                      ▼                      ▼
   S3 Bucket A           S3 Bucket B           S3 Bucket C
        │                      │                      │
   ┌────┴────┐            ┌────┴────┐            ┌────┴────┐
   │ Objects │            │ Objects │            │ Objects │
   │ Images  │            │ Videos  │            │ Backups │
   └─────────┘            └─────────┘            └─────────┘
```
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/fa0b3899-0a54-4497-8eec-389ef7520e73" />

---

## Architecture Components

### 1️⃣ Users & Applications

* Web browsers
* Mobile apps
* Backend applications
* AWS services

They interact with S3 using:

* HTTPS requests
* AWS SDK
* CLI commands

---

### 2️⃣ IAM Security Layer

IAM controls:

* Who can access S3
* What actions are allowed
* Resource-level permissions

---

### 3️⃣ Amazon S3 Service

Core storage layer responsible for:

* Object storage
* Data replication
* High durability
* Automatic scaling

---

### 4️⃣ Buckets

Buckets act as storage containers.

Features:

* Globally unique name
* Region-specific deployment
* Unlimited objects

---

### 5️⃣ Objects

Objects represent actual stored data.

Each object contains:

* File data
* Metadata
* Object key

---

## Data Flow

```
User Upload → Authentication → S3 Bucket → Object Stored
User Request → Permission Check → Object Retrieved
```

---

## Security Layer in Architecture

* IAM Policies
* Bucket Policies
* Encryption (SSE-S3 / KMS)
* Access Control Lists
* Block Public Access

---

## Key Advantages

✔ Unlimited storage
✔ Highly scalable
✔ Secure access management
✔ Global availability
✔ Cost optimization using storage classes

