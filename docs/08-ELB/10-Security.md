# Security in Elastic Load Balancer (ELB)

## Overview

Security is a critical aspect of **Amazon Elastic Load Balancer (ELB)**. AWS provides multiple layers of protection to secure applications from unauthorized access, network attacks, and distributed denial-of-service (DDoS) threats. ELB integrates with several AWS security services such as **IAM**, **Security Groups**, **Network ACLs**, **AWS Certificate Manager (ACM)**, **AWS WAF**, and **AWS Shield** to provide a secure and highly available application environment.

---

# ELB Security Architecture

![Image](https://images.openai.com/static-rsc-4/f2SDNoZNxCiMRp_OChhNr1pFlkG5bleMB4guhRiwltzCDooYRbocDm19GLXHMVyK0Kxna8pKbDqaPVMxyky1eTH5jgLhobeX3rL9ZPDjg091ra5jfK2xQLBbk7C2DiIfz_jvGnGnY8YIYvwNgqxj6uPzAzza_-oHwPz53fnGFyO-fo4Jsm4CX2dMyUkql0bU?purpose=fullsize)

---

# Security Architecture Diagram

```text
                    Internet
                        │
                        ▼
                 AWS Shield (DDoS Protection)
                        │
                        ▼
                AWS WAF (Web Firewall)
                        │
                        ▼
          HTTPS (SSL/TLS via AWS ACM)
                        │
                        ▼
          Application Load Balancer (ALB)
                        │
          Security Group (Allow 80/443)
                        │
                        ▼
                Target Group
                        │
          ┌─────────────┴─────────────┐
          ▼                           ▼
     EC2 Instance 1             EC2 Instance 2
      Security Group             Security Group
                        │
                        ▼
                  Amazon VPC
```

---

# 1. IAM (Identity and Access Management)

## Overview

**AWS IAM** controls who can create, modify, or delete ELB resources.

### Benefits

* Role-based access control (RBAC)
* Least privilege access
* Multi-factor authentication (MFA)
* Temporary credentials using IAM Roles

### Example IAM Permissions

| Permission                                          | Purpose             |
| --------------------------------------------------- | ------------------- |
| `elasticloadbalancing:CreateLoadBalancer`           | Create ELB          |
| `elasticloadbalancing:DeleteLoadBalancer`           | Delete ELB          |
| `elasticloadbalancing:DescribeLoadBalancers`        | View ELBs           |
| `elasticloadbalancing:ModifyLoadBalancerAttributes` | Update ELB settings |

---

# 2. Security Groups

## Overview

Security Groups act as **virtual firewalls** for the Load Balancer and EC2 instances.

### ALB Security Group Example

| Direction | Protocol | Port | Source             |
| --------- | -------- | ---- | ------------------ |
| Inbound   | HTTP     | 80   | 0.0.0.0/0          |
| Inbound   | HTTPS    | 443  | 0.0.0.0/0          |
| Outbound  | All      | All  | EC2 Security Group |

### EC2 Security Group Example

| Direction | Protocol | Port | Source             |
| --------- | -------- | ---- | ------------------ |
| Inbound   | HTTP     | 80   | ALB Security Group |
| Outbound  | All      | All  | Anywhere           |

---

# 3. Network ACLs (NACLs)

## Overview

Network ACLs provide **subnet-level security**.

Unlike Security Groups:

* Stateless
* Allow and Deny rules
* Apply to entire subnets

### Example Rules

| Rule | Protocol | Port | Action |
| ---- | -------- | ---- | ------ |
| 100  | TCP      | 80   | Allow  |
| 110  | TCP      | 443  | Allow  |
| *    | All      | All  | Deny   |

---

# 4. SSL/TLS with AWS Certificate Manager (ACM)

## Overview

Use **AWS Certificate Manager (ACM)** to issue and manage SSL/TLS certificates.

Benefits:

* Encrypts client communication
* Automatic certificate renewal
* Free public certificates
* Easy integration with ALB

### HTTPS Flow

```text
Browser
   │
HTTPS
   │
SSL Certificate (ACM)
   │
Application Load Balancer
```

---

# 5. HTTPS Listener

Configure an HTTPS listener on port **443** to provide encrypted communication.

| Listener | Port | Certificate     |
| -------- | ---- | --------------- |
| HTTPS    | 443  | ACM Certificate |

Advantages:

* Data encryption
* Improved security
* Trusted connections
* Compliance with industry standards

---

# 6. AWS WAF (Web Application Firewall)

## Overview

AWS WAF protects web applications against common attacks.

### Blocks

* SQL Injection (SQLi)
* Cross-Site Scripting (XSS)
* Bot traffic
* IP-based attacks
* Malicious requests

### Example Flow

```text
Internet
     │
AWS WAF
     │
Application Load Balancer
```

---

# 7. AWS Shield

## Overview

AWS Shield provides protection against **Distributed Denial-of-Service (DDoS)** attacks.

### AWS Shield Standard

* Included with AWS
* Protects against common DDoS attacks

### AWS Shield Advanced

* Enhanced DDoS protection
* 24/7 AWS DDoS Response Team
* Advanced attack visibility

---

# 8. Access Logs

Enable **ALB Access Logs** to record incoming requests.

Stored in:

* Amazon S3 Bucket

Example log fields:

* Client IP
* Request URL
* HTTP Method
* Response Code
* Processing Time
* User Agent

Benefits:

* Auditing
* Troubleshooting
* Security analysis
* Compliance

---

# 9. CloudWatch Monitoring

Monitor security-related metrics such as:

* HTTP 4XX Errors
* HTTP 5XX Errors
* Request Count
* Target Response Time
* Rejected Connections

Configure **CloudWatch Alarms** to receive notifications for unusual activity.

---

# Security Workflow

```text
User Request
      │
      ▼
AWS Shield
      │
      ▼
AWS WAF
      │
      ▼
HTTPS (ACM Certificate)
      │
      ▼
Application Load Balancer
      │
      ▼
Security Group
      │
      ▼
Target Group
      │
      ▼
EC2 Instances
```

---

# Best Practices

* Use **HTTPS (443)** instead of HTTP (80) for production.
* Enable **AWS WAF** to block common web attacks.
* Protect internet-facing ALBs with **AWS Shield**.
* Follow the **principle of least privilege** in IAM policies.
* Restrict EC2 access so that only the ALB Security Group can communicate with backend instances.
* Enable **Access Logs** and store them in Amazon S3.
* Monitor metrics and create alarms using Amazon CloudWatch.
* Rotate credentials and enable MFA for privileged IAM users.

---

# Real-World Example

A financial services application uses:

* **IAM Roles** for administrators and deployment pipelines.
* **HTTPS** with ACM-managed certificates.
* **AWS WAF** to block SQL injection and XSS attacks.
* **AWS Shield Advanced** to mitigate DDoS attacks.
* **Security Groups** to ensure backend EC2 instances accept traffic only from the ALB.
* **CloudWatch** and **Access Logs** for continuous monitoring and auditing.

This layered approach significantly improves the security posture of the application.

---

# Conclusion

Amazon Elastic Load Balancer provides multiple integrated security features that help protect applications against unauthorized access and network threats. By combining **IAM**, **Security Groups**, **Network ACLs**, **AWS Certificate Manager**, **AWS WAF**, **AWS Shield**, and **CloudWatch**, organizations can build secure, resilient, and compliant cloud architectures.

---
