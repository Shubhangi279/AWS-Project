# Amazon EC2 Components

## Introduction

Amazon EC2 is built using multiple cloud components that work together to deliver scalable and secure virtual computing services.
These components are part of the infrastructure provided by **Amazon Web Services**.

Each EC2 component plays an important role in launching, securing, storing, and managing virtual servers.

---

## EC2 Components Overview Diagram
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/9b232945-80a0-4104-8df3-bb13879ea1ff" />

---

## Core EC2 Components

---

## 1️⃣ Amazon Machine Image (AMI)

An **AMI** is a preconfigured template used to launch EC2 instances.

### Includes:

* Operating System
* Application software
* Configuration settings

### Examples:

* Amazon Linux
* Ubuntu
* Windows Server

---

## 2️⃣ EC2 Instance

An EC2 Instance is a virtual machine running in AWS cloud.

### Contains:

* vCPU
* RAM
* Storage
* Network interface
* Operating system

Works like a real computer in the cloud.

---

## 3️⃣ Instance Types

Instance type defines hardware capacity.

| Category          | Purpose                 |
| ----------------- | ----------------------- |
| General Purpose   | Balanced workloads      |
| Compute Optimized | CPU intensive tasks     |
| Memory Optimized  | Large datasets          |
| Storage Optimized | High disk performance   |
| GPU Instances     | AI & graphics workloads |

---

## 4️⃣ Key Pair

Used for secure login authentication.

* **Public Key** → Stored in AWS
* **Private Key** → Stored by user

Used for:

* SSH (Linux)
* RDP (Windows)

---

## 5️⃣ Security Groups

Acts as a **virtual firewall** controlling traffic.

### Controls:

* Inbound rules
* Outbound rules

Example:

* Allow Port 22 → SSH
* Allow Port 80 → HTTP

---

## 6️⃣ Elastic Block Store (EBS)

Persistent storage attached to EC2 instances.

### Features:

* Data survives reboot
* Snapshot backup support
* High performance storage

---

## 7️⃣ Instance Store

Temporary storage physically attached to host machine.

Data lost when instance stops or terminates.

---

## 8️⃣ Elastic IP Address

Static public IP address assigned to an EC2 instance.

### Benefits:

* Fixed public IP
* Easy server replacement

---

## 9️⃣ Virtual Private Cloud (VPC)

Private network where EC2 instances operate securely.

### Provides:

* Network isolation
* Custom IP ranges
* Routing control

---

## 🔟 Internet Gateway

Enables communication between EC2 instances and the internet.

Used for:

* Public websites
* Remote server access

---

## 1️⃣1️⃣ Elastic Load Balancer (ELB)

Distributes incoming traffic across multiple EC2 instances.

### Advantages:

* High availability
* Improved performance
* Fault tolerance

---

## 1️⃣2️⃣ Auto Scaling

Automatically adjusts the number of EC2 instances.

Example:

* Traffic increases → Add instances
* Traffic decreases → Remove instances

---

## EC2 Component Interaction Diagram
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/c319da98-59ab-4ec0-8e29-19cb250db20f" />

---

## How EC2 Components Work Together

1. User selects AMI
2. Instance launched inside VPC
3. Security Groups protect instance
4. Storage attached via EBS
5. Internet Gateway enables access
6. Load Balancer distributes traffic
7. Auto Scaling manages demand

---

## Benefits of EC2 Components

* Modular cloud architecture
* Secure infrastructure
* High scalability
* Flexible deployment
* Reliable application hosting

---

## Conclusion

Amazon EC2 components collectively create a powerful cloud computing environment where users can deploy, manage, and scale applications efficiently without handling physical infrastructure.

---
