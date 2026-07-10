# Elastic Load Balancer (ELB) Architecture

## Overview

Amazon **Elastic Load Balancer (ELB)** is designed to distribute incoming client requests across multiple backend resources, ensuring **high availability**, **fault tolerance**, and **scalability**. It acts as a single entry point for applications and intelligently routes traffic to healthy targets deployed across multiple Availability Zones (AZs).

In a typical AWS architecture, users access an application through the Load Balancer. The Load Balancer evaluates incoming requests based on configured **listeners**, **listener rules**, and **target groups**, then forwards them to healthy EC2 instances or other supported targets.

---

# Elastic Load Balancer Architecture

![Image](https://images.openai.com/static-rsc-4/fBDcbNLPoEMIDdUr3NBmdqLqfmnxH523uBDz8AzcKQtogR1jmpKF2kgn0ogzlRzg2_i3smaj7saLEmRHrOu1PIGMdqM0vWxZlwTGug7dBPEa8YTMY4ZvmtprJ-qqyRZ6VAxlepdpP-hfc_umjTgTT4rtsk0URTl5_OgmlGKKK--9ykaTAR_-2cm52lQ9fHiD?purpose=fullsize)

---

# Complete Architecture Diagram

```text
                              Internet
                                  │
                                  ▼
                         Route 53 (Optional)
                                  │
                                  ▼
                         Internet Gateway
                                  │
                                  ▼
                  Application Load Balancer (ALB)
                         Listener (HTTP/HTTPS)
                                  │
                    ┌─────────────┴─────────────┐
                    │                           │
             Target Group A              Target Group B
              (Web Servers)               (API Servers)
                    │                           │
          ┌─────────┴─────────┐       ┌─────────┴─────────┐
          ▼                   ▼       ▼                   ▼
      EC2 Instance 1     EC2 Instance 2     EC2 Instance 3
      (AZ-1)             (AZ-2)             (AZ-2)
          │                   │                   │
          └─────────── Amazon VPC ────────────────┘
                        │
                        ▼
                  CloudWatch Logs
```

---

# Architecture Components

## 1. Internet

The architecture begins with users accessing your application from the internet.

Users may use:

* Web browsers
* Mobile applications
* REST API clients
* Third-party integrations

---

## 2. Amazon Route 53 (Optional)

Amazon Route 53 is AWS's DNS service.

It resolves a custom domain such as:

```text
www.example.com
```

to the DNS name of the Load Balancer.

### Benefits

* Domain management
* Health-based routing
* Failover routing
* Low latency routing

---

## 3. Internet Gateway

The Internet Gateway connects your **Amazon VPC** to the public internet.

Responsibilities:

* Enables inbound internet traffic
* Enables outbound internet access
* Works with Route Tables

---

## 4. Application Load Balancer (ALB)

The Application Load Balancer receives all incoming requests and distributes them across healthy targets.

### Responsibilities

* Traffic distribution
* SSL/TLS termination
* Health monitoring
* Path-based routing
* Host-based routing

Example:

```text
Internet
      │
      ▼
Application Load Balancer
```

---

## 5. Listener

A Listener waits for incoming connections on a specific protocol and port.

Example:

| Protocol | Port |
| -------- | ---- |
| HTTP     | 80   |
| HTTPS    | 443  |

When a request arrives, the Listener evaluates the configured Listener Rules.

---

## 6. Listener Rules

Listener Rules define how requests should be routed.

### Examples

| Request     | Target Group       |
| ----------- | ------------------ |
| `/api/*`    | API Target Group   |
| `/images/*` | Image Target Group |
| `/admin/*`  | Admin Target Group |

This allows a single Load Balancer to route requests to multiple applications.

---

## 7. Target Groups

A Target Group contains one or more backend resources that receive requests.

Supported targets include:

* Amazon EC2 Instances
* IP Addresses
* AWS Lambda Functions

Each Target Group has its own:

* Health Check
* Port
* Protocol
* Routing configuration

---

## 8. Amazon EC2 Instances

These are the backend application servers.

Examples:

* Web servers
* API servers
* Authentication servers
* Application servers

The Load Balancer distributes requests evenly among healthy instances.

---

## 9. Availability Zones

For high availability, EC2 instances are deployed across multiple Availability Zones.

Example:

```text
Availability Zone A

EC2-1

Availability Zone B

EC2-2
EC2-3
```

If one Availability Zone fails, the Load Balancer automatically routes traffic to healthy instances in the remaining zones.

---

## 10. Amazon VPC

All resources are deployed inside an Amazon Virtual Private Cloud (VPC).

Benefits:

* Network isolation
* Secure communication
* Controlled access
* Private networking

---

## 11. Security Groups

Security Groups protect both the Load Balancer and backend EC2 instances.

Example rules:

### ALB Security Group

| Direction | Port | Source   |
| --------- | ---- | -------- |
| Inbound   | 80   | Internet |
| Inbound   | 443  | Internet |

### EC2 Security Group

| Direction | Port | Source             |
| --------- | ---- | ------------------ |
| Inbound   | 80   | ALB Security Group |

This ensures EC2 instances only receive traffic from the Load Balancer.

---

## 12. Amazon CloudWatch

CloudWatch monitors ELB performance.

Common metrics:

* Request Count
* Healthy Host Count
* Unhealthy Host Count
* Response Time
* HTTP Error Codes

CloudWatch can trigger alarms when thresholds are exceeded.

---

# Request Flow

```text
User
 │
 ▼
Route 53
 │
 ▼
Internet Gateway
 │
 ▼
Application Load Balancer
 │
 ▼
Listener (HTTP/HTTPS)
 │
 ▼
Listener Rules
 │
 ▼
Target Group
 │
 ▼
Healthy EC2 Instance
 │
 ▼
Application Response
 │
 ▼
User
```

---

# High Availability Workflow

```text
              Internet
                  │
                  ▼
      Application Load Balancer
                  │
      ┌───────────┴───────────┐
      ▼                       ▼
 Availability Zone A    Availability Zone B
      │                       │
    EC2-1                 EC2-2
                           EC2-3
```

If **EC2-1** becomes unhealthy, the Load Balancer automatically sends traffic only to **EC2-2** and **EC2-3**.

---

# Architecture Benefits

| Benefit           | Description                                            |
| ----------------- | ------------------------------------------------------ |
| High Availability | Multi-AZ deployment improves uptime                    |
| Scalability       | Supports Auto Scaling Groups                           |
| Fault Tolerance   | Routes traffic away from failed targets                |
| Security          | Integrates with Security Groups, IAM, ACM, and AWS WAF |
| Performance       | Balances requests efficiently                          |
| Reliability       | Automatic health checks and failover                   |

---

# Real-World Example

An online banking application serves millions of users daily.

* Customers access **bank.example.com**.
* **Amazon Route 53** resolves the domain to the **Application Load Balancer**.
* The ALB accepts HTTPS requests using an SSL certificate from **AWS Certificate Manager (ACM)**.
* Requests to `/accounts/*` are routed to the **Account Service Target Group**.
* Requests to `/payments/*` are routed to the **Payment Service Target Group**.
* EC2 instances run across two Availability Zones.
* If one instance or one Availability Zone fails, the ALB automatically redirects traffic to healthy instances, ensuring uninterrupted service.

---

# Best Practices

* Deploy the Load Balancer across **at least two Availability Zones**.
* Use **HTTPS (Port 443)** with certificates from **AWS Certificate Manager (ACM)**.
* Configure separate **Target Groups** for different applications or services.
* Enable **Cross-Zone Load Balancing**.
* Configure **Health Checks** with appropriate thresholds.
* Protect internet-facing ALBs with **AWS WAF** and **AWS Shield**.
* Monitor performance using **Amazon CloudWatch**.
* Integrate with **Auto Scaling Groups** for automatic capacity management.

---

# Conclusion

The Elastic Load Balancer architecture provides a robust foundation for building highly available, scalable, and secure applications on AWS. By combining **Application Load Balancers**, **Target Groups**, **Listeners**, **Health Checks**, **Multi-AZ deployment**, and **CloudWatch monitoring**, ELB ensures efficient traffic distribution and seamless failover, making it a key component of modern cloud architectures.

---

