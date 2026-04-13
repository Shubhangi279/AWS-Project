# Amazon S3 Storage Classes

## Introduction

**Amazon S3 Storage Classes** allow you to store data at different cost and performance levels depending on **how frequently data is accessed**.

Instead of paying the same price for all data, **S3 optimizes cost automatically** based on usage patterns.

Idea:

* Frequently used data → Fast access storage
* Rarely used data → Low-cost storage
* Archive data → Cheapest storage

---

## S3 Storage Class Architecture (Concept)

```
                Amazon S3
                    │
 ┌──────────────────┼──────────────────┐
 │                  │                  │
Frequent Access   Infrequent Access   Archive Storage
(Standard)        (IA Classes)        (Glacier Classes)
```

---

## Types of Amazon S3 Storage Classes

---

## 1️⃣ S3 Standard

Default storage class

**Best For**

* Frequently accessed data
* Dynamic websites
* Applications & big data analytics

**Features**

* Low latency
* High throughput
* Multi-AZ durability

**Example**

* Website images
* Mobile apps data

---

## 2️⃣ S3 Intelligent-Tiering

Automatically moves data between tiers

**Best For**

* Unknown or changing access patterns

**Features**

* Automatic cost optimization
* No performance impact
* No retrieval fees

**Example**

* Data lakes
* User uploads

---

## 3️⃣ S3 Standard-IA (Infrequent Access)

Less frequently accessed but needs fast access

**Best For**

* Backup files
* Disaster recovery

**Features**

* Lower storage cost
* Retrieval fee applies
* Millisecond access

---

## 4️⃣ S3 One Zone-IA

Stored in single Availability Zone

**Best For**

* Re-creatable data
* Secondary backups

**Features**

* Cheaper than Standard-IA
* Lower redundancy

---

## 5️⃣ S3 Glacier Instant Retrieval

Archive storage with immediate access

**Best For**

* Medical records
* Media archives

**Features**

* Very low cost
* Instant retrieval

---

## 6️⃣ S3 Glacier Flexible Retrieval (Formerly Glacier)

Long-term archive

**Retrieval Options**

* Expedited → Minutes
* Standard → Hours
* Bulk → Cheapest

**Best For**

* Backup archives

---

## 7️⃣ S3 Glacier Deep Archive

Cheapest storage in AWS

**Best For**

* Compliance data
* Long-term retention (7–10 years)

**Features**

* Retrieval time: 12–48 hours

---

## Storage Classes Comparison

| Storage Class       | Access Speed  | Cost      | Use Case           |
| ------------------- | ------------- | --------- | ------------------ |
| Standard            | Milliseconds  | High      | Active data        |
| Intelligent-Tiering | Milliseconds  | Optimized | Unknown usage      |
| Standard-IA         | Milliseconds  | Lower     | Backups            |
| One Zone-IA         | Milliseconds  | Low       | Re-creatable data  |
| Glacier Instant     | Instant       | Very Low  | Archive access     |
| Glacier Flexible    | Minutes-Hours | Cheaper   | Long archive       |
| Deep Archive        | Hours         | Lowest    | Compliance storage |

---

## Lifecycle Management

Amazon S3 can automatically move objects:

```
S3 Standard
     ↓
Standard-IA
     ↓
Glacier
     ↓
Deep Archive
```

This process is called **Lifecycle Policy**.

---

## S3 Storage Classes Diagram 
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/320b2402-0f14-406e-a0e2-3e91150173a1" />


You can use this diagram idea:

```
Hot Data  →  Warm Data  →  Cold Data  →  Archive
Standard → IA → Glacier → Deep Archive
```

---

## Key Advantages

* Cost optimization
* Automatic tiering
* High durability (99.999999999%)
* Lifecycle automation
* Flexible retrieval options

---
