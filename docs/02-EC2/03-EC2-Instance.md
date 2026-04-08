# What is an Amazon EC2 Instance?

## Introduction

An **Amazon EC2 Instance** is a virtual server provided by **Amazon Web Services** that runs applications in the cloud.

Instead of buying physical computers or servers, users can launch virtual machines on AWS infrastructure within minutes. These virtual machines are called **EC2 Instances**.

An EC2 instance behaves exactly like a real computer — it has:

* Operating System
* CPU (vCPU)
* Memory (RAM)
* Storage
* Network connectivity
* Security controls

---

## EC2 Instance Concept Diagram
<img width="1000" height="905" alt="image" src="https://github.com/user-attachments/assets/97778e9e-5faa-47e8-a471-f9b0fc580dde" />


---

## How EC2 Instance Works

When a user launches an EC2 instance:

1. AWS allocates virtual hardware resources.
2. A selected operating system is installed.
3. Storage volume is attached.
4. Network configuration is applied.
5. Security rules are enforced.
6. Instance becomes accessible via SSH or RDP.

---

## EC2 Instance Architecture Diagram
<img width="600" height="465" alt="image" src="https://github.com/user-attachments/assets/fef21ef7-860e-4c65-aed4-faceb216dd26" />

---

## Main Components of an EC2 Instance

---

### 1️⃣ Amazon Machine Image (AMI)

AMI is a template used to create an instance.

Includes:

* Operating System
* Preinstalled software
* Configuration settings

Examples:

* Amazon Linux
* Ubuntu
* Windows Server

---

### 2️⃣ Instance Type

Defines hardware configuration.

| Type              | Purpose             |
| ----------------- | ------------------- |
| General Purpose   | Balanced workloads  |
| Compute Optimized | CPU intensive apps  |
| Memory Optimized  | Big data processing |
| Storage Optimized | High disk usage     |

---

### 3️⃣ vCPU (Virtual CPU)

Processing power allocated to the instance.

---

### 4️⃣ Memory (RAM)

Handles running applications and processes.

---

### 5️⃣ Storage

#### Elastic Block Store (EBS)

* Persistent storage
* Data saved even after reboot

#### Instance Store

* Temporary storage
* Data lost after stop/terminate

---

### 6️⃣ Networking

Each EC2 instance receives:

* Private IP address
* Optional Public IP
* Security group protection

---

### 7️⃣ Security Groups

Acts as a virtual firewall controlling:

* Inbound traffic
* Outbound traffic

Example:

* Allow SSH → Port 22
* Allow HTTP → Port 80

---

## EC2 Instance Lifecycle

![EC2 Lifecycle](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/instance_lifecycle.png)

### Lifecycle States

1. **Pending** → Instance launching
2. **Running** → Active state
3. **Stopping** → Shutting down
4. **Stopped** → Powered off
5. **Terminated** → Deleted permanently

---

## Key Features of EC2 Instances

* On-demand virtual servers
* Elastic scalability
* Pay-as-you-go pricing
* Full OS control
* Integration with AWS services
* Global deployment capability

---

## Common Use Cases

* Website hosting
* Application servers
* Development & testing environments
* Machine learning workloads
* Gaming servers
* Data processing systems

---

## Advantages

* No physical hardware required
* Fast deployment
* Flexible configurations
* High availability
* Secure environment

---

## Real-World Example

A company hosting an e-commerce website can:

* Launch EC2 instances
* Attach storage volumes
* Use load balancers
* Automatically scale during high traffic

---

## Simple Understanding

**EC2 Instance = Virtual Computer in the Cloud**

You control it like your personal computer, but AWS manages the physical infrastructure.
