# Components of Elastic Load Balancer (ELB)

## Overview

Amazon **Elastic Load Balancer (ELB)** consists of several key components that work together to distribute incoming traffic, monitor application health, and ensure high availability. Understanding these components is essential for designing scalable and fault-tolerant cloud architectures.

Each component has a specific role in receiving client requests, routing traffic, monitoring backend resources, and maintaining secure communication.

---

# Elastic Load Balancer Components

![Image](https://images.openai.com/static-rsc-4/y1nsWXf9XBs8cc6SK0MClB1H1TwFFwDSIZL9AYUU27Zs0yMn9kJZS5k3wJkyEgzQtTTs571KlUJkyHZQz9BMRpEcNhxSU0x_x6d_MOY0xOEnPWugaBHmLzy4yTIIhrgx3yo7lzBPA5RKElhHGGBK0jubRM88RsDx0a2Ev7ESnKIIyNWTUsXo9ayb6RG1owIO?purpose=fullsize)

---

# ELB Component Architecture

```text
                      Internet Users
                            │
                            ▼
                  Elastic Load Balancer
                            │
          ┌─────────────────┼─────────────────┐
          │                 │                 │
          ▼                 ▼                 ▼
      Listener         Listener Rule    Security Group
          │
          ▼
      Target Group
          │
     ┌────┴─────┐
     ▼          ▼
 EC2 Instance  EC2 Instance
     │          │
     └────┬─────┘
          ▼
     Health Checks
```

---

# 1. Elastic Load Balancer

## Overview

The **Load Balancer** is the main component that receives requests from users and distributes them across registered targets.

It acts as the **single entry point** for your application.

### Responsibilities

* Receives incoming requests
* Distributes traffic
* Monitors backend health
* Improves application availability
* Provides failover

### Example

```text
Client
   │
   ▼
Elastic Load Balancer
   │
 ┌─┴────────┐
 ▼          ▼
EC2-1     EC2-2
```

---

# 2. Listener

## Overview

A **Listener** checks incoming connection requests using a specific **protocol** and **port**.

It forwards requests to the appropriate Target Group.

### Common Listener Ports

| Protocol | Port |
| -------- | ---- |
| HTTP     | 80   |
| HTTPS    | 443  |
| TCP      | 80   |
| TLS      | 443  |

### Example

```text
HTTPS : 443
        │
        ▼
Application Load Balancer
```

---

# 3. Listener Rules

## Overview

Listener Rules determine **where traffic should be sent** based on conditions.

### Rule Types

* Path-based routing
* Host-based routing
* HTTP header
* Query string
* Source IP

### Example

| URL         | Target Group |
| ----------- | ------------ |
| `/images/*` | Image Server |
| `/api/*`    | API Server   |
| `/admin/*`  | Admin Server |

### Example Diagram

```text
User Request
      │
      ▼
Listener
      │
 ┌────┴────────────┐
 │                 │
 ▼                 ▼
/api/*         /images/*
 │                 │
 ▼                 ▼
API TG       Image TG
```

---

# 4. Target Group

## Overview

A **Target Group** contains one or more backend resources that receive traffic from the Load Balancer.

### Supported Targets

* Amazon EC2
* IP Addresses
* AWS Lambda Functions

### Responsibilities

* Route requests
* Perform health checks
* Register/Deregister targets

### Example

```text
Target Group
     │
 ┌───┴─────┐
 ▼         ▼
EC2-1    EC2-2
```

---

# 5. Targets

## Overview

Targets are the backend resources that process user requests.

### Supported Target Types

| Target          | Supported |
| --------------- | --------- |
| EC2 Instance    | ✅         |
| IP Address      | ✅         |
| Lambda Function | ✅         |

### Responsibilities

* Process requests
* Generate responses
* Return data to ELB

---

# 6. Health Checks

## Overview

Health Checks verify whether registered targets are healthy.

If a target becomes unhealthy, ELB automatically stops sending traffic to it.

### Example

```text
Health Check
      │
 ┌────┴────┐
 │         │
 ▼         ▼
Healthy   Unhealthy
   │          │
   ▼          ✖
Receives   No Traffic
Traffic
```

### Common Health Check Settings

| Setting  | Example |
| -------- | ------- |
| Protocol | HTTP    |
| Port     | 80      |
| Path     | /health |
| Interval | 30 sec  |
| Timeout  | 5 sec   |

---

# 7. Security Groups

## Overview

Security Groups control network access to the Load Balancer.

### Typical Rules

| Direction | Port | Purpose                    |
| --------- | ---- | -------------------------- |
| Inbound   | 80   | HTTP Traffic               |
| Inbound   | 443  | HTTPS Traffic              |
| Outbound  | All  | Forward traffic to targets |

### Benefits

* Protects backend resources
* Restricts unauthorized access
* Improves security

---

# 8. Availability Zones (AZs)

## Overview

Elastic Load Balancer can distribute traffic across multiple Availability Zones.

### Benefits

* High Availability
* Fault Tolerance
* Disaster Recovery

### Example

```text
Availability Zone A

EC2-1

Availability Zone B

EC2-2

        ▲
        │
 Elastic Load Balancer
```

---

# 9. DNS Name

## Overview

Each Elastic Load Balancer is assigned a unique DNS name.

Example:

```text
my-alb-123456789.ap-south-1.elb.amazonaws.com
```

Users access the application using this DNS name or a custom domain configured through **Amazon Route 53**.

### Benefits

* Easy access
* Supports custom domains
* Automatically updated by AWS

---

# Component Summary

| Component          | Purpose                                   |
| ------------------ | ----------------------------------------- |
| Load Balancer      | Distributes incoming traffic              |
| Listener           | Accepts client requests on specific ports |
| Listener Rules     | Determines request routing                |
| Target Group       | Groups backend resources                  |
| Targets            | Process application requests              |
| Health Checks      | Detect healthy and unhealthy targets      |
| Security Groups    | Control network access                    |
| Availability Zones | Improve availability and resilience       |
| DNS Name           | Provides endpoint for clients             |

---

# Real-World Example

A banking application is deployed across two Availability Zones.

* Customers connect to the **Application Load Balancer** using a custom domain.
* The **Listener** accepts HTTPS traffic on port 443.
* **Listener Rules** route `/api/*` requests to API servers and `/web/*` requests to web servers.
* **Target Groups** contain EC2 instances for each service.
* **Health Checks** ensure only healthy instances receive requests.
* If one server fails, traffic is automatically redirected to healthy servers without affecting customers.

---

# Best Practices

* Use **HTTPS (Port 443)** for secure communication.
* Configure **Health Checks** with appropriate intervals and thresholds.
* Organize backend servers into separate **Target Groups**.
* Enable **Cross-Zone Load Balancing** for even traffic distribution.
* Restrict access using **Security Groups**.
* Use meaningful names for Listeners and Target Groups.
* Monitor ELB metrics with **Amazon CloudWatch**.

---

# Conclusion

The components of Amazon Elastic Load Balancer work together to deliver a secure, highly available, and scalable application infrastructure. By understanding how Load Balancers, Listeners, Target Groups, Health Checks, Security Groups, and Availability Zones interact, you can design robust cloud architectures that efficiently handle traffic and provide a seamless user experience.

---

