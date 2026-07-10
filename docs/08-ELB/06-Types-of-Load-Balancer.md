# Types of Elastic Load Balancer (ELB)

## Overview

Amazon Elastic Load Balancer (ELB) offers **four types of load balancers**, each designed for different networking and application requirements. Choosing the appropriate load balancer depends on factors such as the **OSI layer**, **protocols**, **performance requirements**, and **application architecture**.

The four types of AWS Load Balancers are:

* **Application Load Balancer (ALB)**
* **Network Load Balancer (NLB)**
* **Gateway Load Balancer (GWLB)**
* **Classic Load Balancer (CLB)**

Each type provides unique capabilities and is optimized for specific workloads.

---

# AWS Load Balancer Types

![Image](https://images.openai.com/static-rsc-4/MG2MSt4a_dkNfLtgG_Goi1ZOUDeHSIIphNVsWZ6g4aq7RiWLF4lNaR099R4-qXQTrTCY_SU2TtZ7Yl1rFoTheRAS0582drpx7bhlk92fKVgEd-4fF-uWxmOJcFx5dGzoAJdhBRFMsZUeYilqm5N6P6pZgbvY539PvgRQvllB4_9nuLtN_UrqXkr6K00BiyCc?purpose=fullsize)

---

# Overview Diagram

```text
                     Elastic Load Balancer
                              │
      ┌─────────────┬──────────────┬──────────────┬──────────────┐
      ▼             ▼              ▼              ▼
     ALB           NLB            GWLB           CLB
 Layer 7        Layer 4        Layer 3/4      Layer 4 & 7
 HTTP/HTTPS    TCP/UDP/TLS     Appliances     Legacy Apps
```

---

# 1. Application Load Balancer (ALB)

## Overview

The **Application Load Balancer (ALB)** operates at **Layer 7 (Application Layer)** of the OSI model. It is designed for modern web applications and microservices, allowing intelligent routing based on the content of HTTP/HTTPS requests.

### Supported Protocols

* HTTP
* HTTPS
* HTTP/2
* WebSocket
* gRPC

### Key Features

* Path-based routing
* Host-based routing
* SSL/TLS termination
* WebSocket support
* HTTP/2 support
* Integration with ECS, EKS, and Lambda

### Example

```text
Internet
     │
     ▼
Application Load Balancer
     │
 ┌───┴──────────┐
 ▼              ▼
/api/*      /images/*
 │              │
 ▼              ▼
API EC2     Image EC2
```

### Best Use Cases

* Web applications
* REST APIs
* Microservices
* Containerized applications
* Serverless applications

### Advantages

* Intelligent routing
* Layer 7 features
* Native AWS integration
* Supports Lambda targets

---

# 2. Network Load Balancer (NLB)

## Overview

The **Network Load Balancer (NLB)** operates at **Layer 4 (Transport Layer)** and is designed for ultra-high performance with very low latency.

### Supported Protocols

* TCP
* UDP
* TLS

### Key Features

* Static IP addresses
* Millions of requests per second
* Very low latency
* High throughput
* Preserves client IP

### Example

```text
Clients
    │
    ▼
Network Load Balancer
    │
 ┌──┴────┐
 ▼       ▼
EC2-1   EC2-2
```

### Best Use Cases

* Gaming applications
* Financial systems
* Real-time applications
* VoIP
* IoT platforms

### Advantages

* High performance
* Low latency
* Static IP support
* Excellent scalability

---

# 3. Gateway Load Balancer (GWLB)

## Overview

The **Gateway Load Balancer (GWLB)** operates at **Layer 3 and Layer 4**, enabling the deployment and scaling of virtual network appliances.

### Common Appliances

* Firewalls
* Intrusion Detection Systems (IDS)
* Intrusion Prevention Systems (IPS)
* Deep Packet Inspection (DPI)

### Example

```text
Internet
     │
     ▼
Gateway Load Balancer
     │
 ┌───┴────────┐
 ▼            ▼
Firewall   IDS/IPS
```

### Best Use Cases

* Network security
* Traffic inspection
* Firewall management
* Enterprise networking

### Advantages

* Transparent traffic inspection
* High availability
* Easy appliance scaling

---

# 4. Classic Load Balancer (CLB)

## Overview

The **Classic Load Balancer (CLB)** is the original AWS load balancer. It supports both **Layer 4** and **Layer 7** features but has limited functionality compared to newer load balancers.

### Supported Protocols

* HTTP
* HTTPS
* TCP
* SSL

### Example

```text
Internet
     │
     ▼
Classic Load Balancer
     │
 ┌──┴─────┐
 ▼        ▼
EC2-1   EC2-2
```

### Best Use Cases

* Legacy applications
* Older AWS deployments

### Limitations

* No path-based routing
* No host-based routing
* Limited modern features

---

# Feature Comparison

| Feature            | ALB | NLB | GWLB |  CLB  |
| ------------------ | :-: | :-: | :--: | :---: |
| OSI Layer          |  7  |  4  |  3/4 | 4 & 7 |
| HTTP/HTTPS         |  ✅  |  ❌  |   ❌  |   ✅   |
| TCP                |  ❌  |  ✅  |   ✅  |   ✅   |
| UDP                |  ❌  |  ✅  |   ❌  |   ❌   |
| TLS                |  ✅  |  ✅  |   ❌  |   ✅   |
| Static IP          |  ❌  |  ✅  |   ✅  |   ❌   |
| Path-Based Routing |  ✅  |  ❌  |   ❌  |   ❌   |
| Host-Based Routing |  ✅  |  ❌  |   ❌  |   ❌   |
| WebSocket          |  ✅  |  ❌  |   ❌  |   ❌   |
| Lambda Support     |  ✅  |  ❌  |   ❌  |   ❌   |

---

# OSI Layer Comparison

```text
Layer 7 ───────────► Application Load Balancer

Layer 4 ───────────► Network Load Balancer

Layer 3 & 4 ───────► Gateway Load Balancer

Layer 4 & 7 ───────► Classic Load Balancer
```

---

# Real-World Examples

| Application                    | Recommended Load Balancer |
| ------------------------------ | ------------------------- |
| E-commerce Website             | Application Load Balancer |
| Banking API                    | Application Load Balancer |
| Online Multiplayer Game        | Network Load Balancer     |
| Video Streaming Platform       | Network Load Balancer     |
| Enterprise Firewall Deployment | Gateway Load Balancer     |
| Legacy Enterprise Application  | Classic Load Balancer     |

---

# Which Load Balancer Should You Choose?

| Requirement            | Recommended ELB |
| ---------------------- | --------------- |
| Web Applications       | ALB             |
| REST APIs              | ALB             |
| Microservices          | ALB             |
| Kubernetes / ECS       | ALB             |
| Ultra-low Latency      | NLB             |
| TCP/UDP Applications   | NLB             |
| Security Appliances    | GWLB            |
| Older AWS Applications | CLB             |

---

# Best Practices

* Use **Application Load Balancer** for modern web applications and APIs.
* Choose **Network Load Balancer** for high-performance TCP/UDP workloads.
* Deploy **Gateway Load Balancer** to simplify network appliance management.
* Avoid using **Classic Load Balancer** for new projects; it is mainly intended for legacy workloads.
* Combine ELB with **Auto Scaling**, **CloudWatch**, and **AWS WAF** for a highly available and secure architecture.

---

# Conclusion

AWS provides four types of Elastic Load Balancers to address different networking and application needs. **Application Load Balancer (ALB)** is the preferred choice for HTTP/HTTPS applications, **Network Load Balancer (NLB)** excels at high-performance Layer 4 traffic, **Gateway Load Balancer (GWLB)** is ideal for deploying security appliances, and **Classic Load Balancer (CLB)** remains available for legacy environments. Selecting the right load balancer improves performance, scalability, security, and reliability.

---
