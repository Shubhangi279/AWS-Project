# Working of Elastic Load Balancer (ELB)

## Overview

Amazon **Elastic Load Balancer (ELB)** automatically distributes incoming client requests across multiple backend resources such as **Amazon EC2 instances, containers, IP addresses, and AWS Lambda functions**. It continuously monitors the health of these resources and ensures that traffic is routed only to healthy targets.

This intelligent routing mechanism improves **availability, scalability, performance, and fault tolerance**, making ELB a core networking service in AWS.

---

# ELB Working Architecture

![Image](https://images.openai.com/static-rsc-4/uPHyJn-_5NOT8PmJCSKarciEMG9vG_A7pfelrnTLCWWVA8MqVJJexdMP90qa87yDsksl87NudYTwYktwsKTNCTElyZiZ-mGAPyr0gYspbkdbNpWpIw6NiAyZ7D1Taik5wvI9t3SRrx3g-FDDxvtLOop2-OymGsdtw7v62nZ3qRzTweR0K-M8UsXmltz1xT6L?purpose=fullsize)

---

# End-to-End Request Flow

```text
                 User Request
                      │
                      ▼
             Route 53 (DNS)
                      │
                      ▼
             Internet Gateway
                      │
                      ▼
      Application Load Balancer (ALB)
                      │
              Listener (80/443)
                      │
             Listener Rules
                      │
             Target Group Selection
                      │
         Health Check Verification
                      │
        ┌─────────────┴─────────────┐
        ▼                           ▼
   EC2 Instance 1              EC2 Instance 2
    (Healthy)                   (Healthy)
        │                           │
        └─────────────┬─────────────┘
                      ▼
            Application Response
                      │
                      ▼
                     User
```

---

# Step-by-Step Working Process

## Step 1: User Sends a Request

A client opens a browser and enters the application URL.

Example:

```text
https://www.example.com
```

The request first reaches the DNS service.

---

## Step 2: Route 53 Resolves the Domain

If you're using **Amazon Route 53**, it resolves the domain name to the DNS name of the Elastic Load Balancer.

Example:

```text
www.example.com
        │
        ▼
my-alb-123456.ap-south-1.elb.amazonaws.com
```

---

## Step 3: Request Reaches the Load Balancer

The Application Load Balancer receives the incoming request.

Responsibilities:

* Accept client connections
* Handle SSL/TLS termination (HTTPS)
* Forward requests to backend targets
* Maintain high availability

---

## Step 4: Listener Receives the Request

The Listener waits for requests on a configured protocol and port.

Example:

| Protocol | Port |
| -------- | ---- |
| HTTP     | 80   |
| HTTPS    | 443  |

If HTTPS is used, ELB decrypts the traffic using an SSL/TLS certificate from **AWS Certificate Manager (ACM)**.

---

## Step 5: Listener Rules Are Evaluated

The Listener checks its routing rules.

Example:

| Incoming Request | Target Group       |
| ---------------- | ------------------ |
| `/api/*`         | API Target Group   |
| `/images/*`      | Image Target Group |
| `/admin/*`       | Admin Target Group |

This enables multiple applications to run behind a single Load Balancer.

---

## Step 6: Target Group Selection

The request is forwarded to the appropriate **Target Group**.

A Target Group may contain:

* EC2 Instances
* IP Addresses
* AWS Lambda Functions

Example:

```text
Target Group

EC2-1
EC2-2
EC2-3
```

---

## Step 7: Health Check Verification

Before forwarding the request, ELB checks whether the selected target is healthy.

Healthy Target:

```text
✔ Receives Traffic
```

Unhealthy Target:

```text
✖ Removed from Load Balancing
```

Health Check Example

| Setting  | Value     |
| -------- | --------- |
| Protocol | HTTP      |
| Port     | 80        |
| Path     | `/health` |
| Interval | 30 sec    |
| Timeout  | 5 sec     |

---

## Step 8: Request Is Processed

The healthy EC2 instance processes the request.

Example:

```text
User Login
Product Search
API Request
Image Download
```

---

## Step 9: Response Returns Through ELB

The backend server sends its response to the Load Balancer.

The Load Balancer then forwards the response back to the user.

```text
EC2
 │
 ▼
Elastic Load Balancer
 │
 ▼
User
```

---

# Cross-Zone Load Balancing

When enabled, ELB distributes requests evenly across all Availability Zones.

```text
                    Internet
                        │
                        ▼
                Elastic Load Balancer
                  ┌──────────────┐
                  │              │
                  ▼              ▼
               AZ-A            AZ-B
            ┌────────┐      ┌────────┐
            │ EC2-1  │      │ EC2-2  │
            │ EC2-3  │      │ EC2-4  │
            └────────┘      └────────┘
```

Benefits:

* Better resource utilization
* Higher availability
* Even traffic distribution

---

# Integration with Auto Scaling

When traffic increases:

```text
High Traffic
      │
      ▼
Auto Scaling
      │
      ▼
Launch New EC2 Instance
      │
      ▼
Automatically Registered
      │
      ▼
Elastic Load Balancer
```

When traffic decreases:

* Auto Scaling terminates extra instances.
* ELB automatically stops routing traffic to them.

---

# Failure Scenario

```text
Internet
     │
     ▼
Elastic Load Balancer
     │
 ┌───┴───────────┐
 ▼               ▼
EC2-1          EC2-2
(Healthy)     (Unhealthy)
```

Result:

* Traffic is sent only to **EC2-1**
* **EC2-2** is automatically removed until it becomes healthy again.

---

# Complete Workflow

```text
User
 │
 ▼
DNS (Route 53)
 │
 ▼
Elastic Load Balancer
 │
 ▼
Listener
 │
 ▼
Listener Rules
 │
 ▼
Target Group
 │
 ▼
Health Check
 │
 ▼
Healthy EC2
 │
 ▼
Application Response
 │
 ▼
User
```

---

# Real-World Example

An online food delivery platform experiences a surge in traffic during dinner hours.

1. Customers access the website through a custom domain.
2. Route 53 resolves the domain to the Application Load Balancer.
3. The ALB receives HTTPS requests.
4. Listener Rules route `/orders/*` requests to the Order Service and `/payments/*` requests to the Payment Service.
5. Health Checks ensure only healthy EC2 instances receive requests.
6. Auto Scaling launches additional EC2 instances as traffic grows.
7. Users experience fast response times without service interruption.

---

# Advantages of ELB Working Mechanism

* Automatic request distribution
* High availability across multiple Availability Zones
* Automatic failover for unhealthy instances
* Secure HTTPS support
* Seamless integration with Auto Scaling
* Reduced server overload
* Improved application performance
* Better user experience

---

# Best Practices

* Deploy targets across at least two Availability Zones.
* Configure Health Checks with appropriate paths and intervals.
* Use HTTPS listeners with certificates from AWS Certificate Manager (ACM).
* Enable Cross-Zone Load Balancing.
* Integrate ELB with Auto Scaling Groups.
* Monitor ELB metrics using Amazon CloudWatch.
* Protect internet-facing applications with AWS WAF and AWS Shield.

---

# Conclusion

Elastic Load Balancer simplifies traffic management by automatically distributing requests, monitoring backend health, and ensuring continuous application availability. Its integration with Route 53, Auto Scaling, CloudWatch, and AWS security services enables organizations to build resilient, scalable, and secure cloud applications with minimal operational overhead.

---
