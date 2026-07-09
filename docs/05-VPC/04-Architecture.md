# AWS VPC Architecture

## Overview

The **Amazon Virtual Private Cloud (VPC) Architecture** represents a secure and isolated networking environment where AWS resources communicate with each other and the internet. A typical VPC consists of **public and private subnets**, **Internet Gateway**, **NAT Gateway**, **Route Tables**, **Security Groups**, and **Network ACLs**.

In a standard three-tier architecture:

* The **Public Subnet** hosts internet-facing resources such as Load Balancers and Web Servers.
* The **Private Subnet** hosts Application Servers and Databases, which are protected from direct internet access.
* An **Internet Gateway (IGW)** allows public subnet resources to communicate with the internet.
* A **NAT Gateway** enables private subnet resources to access the internet securely for software updates without exposing them to inbound traffic.
* **Route Tables** determine the path of network traffic.
* **Security Groups** and **Network ACLs** provide multiple layers of network security.

This architecture improves **security, scalability, high availability, and fault tolerance**, making it suitable for production cloud applications.

---

## AWS VPC Architecture Diagram

```text
                                    Internet
                                        │
                                        │
                              Internet Gateway (IGW)
                                        │
                         ┌──────────────┴──────────────┐
                         │       Amazon VPC            │
                         │      CIDR: 10.0.0.0/16      │
                         │                             │
         ┌───────────────┴─────────────────────────────┴───────────────┐
         │                                                             │
         │                    Public Subnet                            │
         │                    10.0.1.0/24                              │
         │                                                             │
         │   ┌──────────────────┐     ┌──────────────────────────┐      │
         │   │ Application Load │────▶│       EC2 Web Server     │      │
         │   │ Balancer (ALB)   │     │      (Public Instance)   │      │
         │   └──────────────────┘     └─────────────┬────────────┘      │
         │                                          │                   │
         │                                   NAT Gateway               │
         └──────────────────────────────────────────┼───────────────────┘
                                                    │
                                        Outbound Internet Access
                                                    │
         ┌──────────────────────────────────────────┼───────────────────┐
         │                    Private Subnet                            │
         │                    10.0.2.0/24                               │
         │                                                              │
         │   ┌──────────────────┐     ┌────────────────────────────┐     │
         │   │ Application EC2  │────▶│      Amazon RDS Database   │     │
         │   │    Server         │     │      (Private Instance)    │     │
         │   └──────────────────┘     └────────────────────────────┘     │
         │                                                              │
         └──────────────────────────────────────────────────────────────┘

                 Route Tables • Security Groups • Network ACLs
```

---

## Architecture Components

| Component                           | Purpose                                                                                                    |
| ----------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| **VPC**                             | Provides an isolated virtual network in AWS.                                                               |
| **CIDR Block**                      | Defines the IP address range of the VPC (e.g., `10.0.0.0/16`).                                             |
| **Public Subnet**                   | Hosts internet-facing resources like Load Balancers and Web Servers.                                       |
| **Private Subnet**                  | Hosts backend resources such as Application Servers and Databases.                                         |
| **Internet Gateway (IGW)**          | Enables internet connectivity for resources in the public subnet.                                          |
| **NAT Gateway**                     | Allows private subnet resources to access the internet securely without allowing inbound internet traffic. |
| **Route Table**                     | Determines how network traffic is routed between subnets and gateways.                                     |
| **Security Group**                  | Acts as a stateful firewall at the instance level.                                                         |
| **Network ACL**                     | Acts as a stateless firewall at the subnet level.                                                          |
| **Amazon RDS**                      | Stores application data securely in a private subnet.                                                      |
| **Application Load Balancer (ALB)** | Distributes incoming traffic across multiple EC2 instances.                                                |

---

## Traffic Flow

1. Users access the application through the **Internet**.
2. Traffic enters the VPC via the **Internet Gateway (IGW)**.
3. The **Application Load Balancer (ALB)** distributes requests to EC2 web servers in the **Public Subnet**.
4. Web servers communicate with **Application Servers** in the **Private Subnet**.
5. Application servers retrieve or store data in the **Amazon RDS Database**.
6. Private subnet resources use the **NAT Gateway** to download updates or access AWS services without being directly accessible from the internet.
7. **Security Groups** and **Network ACLs** filter and secure network traffic at the instance and subnet levels.

---


