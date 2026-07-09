# AWS VPC (Virtual Private Cloud) – Introduction

## Introduction

Amazon **Virtual Private Cloud (Amazon VPC)** is a networking service provided by Amazon Web Services (AWS) that enables users to create a **logically isolated virtual network** within the AWS Cloud. It allows you to launch AWS resources such as EC2 instances, RDS databases, and Load Balancers in a secure and customizable environment.

With Amazon VPC, you have complete control over your network configuration, including selecting your own IP address range, creating public and private subnets, configuring route tables, attaching Internet and NAT Gateways, and implementing security using Security Groups and Network ACLs.

A VPC acts like a **private data center in the cloud**, where you define how your resources communicate with each other, with other AWS services, and with the internet. This isolation enhances security, improves network management, and supports scalable cloud architectures.

Amazon VPC is the foundation of AWS networking and is used to build secure, reliable, and highly available cloud infrastructures for web applications, enterprise systems, databases, and hybrid cloud environments.

---

# VPC Architecture Diagram

```text
                              Internet
                                  │
                                  │
                         Internet Gateway (IGW)
                                  │
          ┌───────────────────────┴────────────────────────┐
          │                 Amazon VPC                     │
          │              CIDR: 10.0.0.0/16                 │
          │                                                │
          │  ┌────────────────┐      ┌────────────────┐    │
          │  │ Public Subnet  │      │ Private Subnet │    │
          │  │ 10.0.1.0/24    │      │ 10.0.2.0/24    │    │
          │  │                │      │                │    │
          │  │ EC2 Web Server │──────│ App Server     │    │
          │  │ Load Balancer  │      │ Amazon RDS     │    │
          │  └───────┬────────┘      └────────┬───────┘    │
          │          │                        │            │
          │     NAT Gateway              No Direct         │
          │          │                Internet Access      │
          └──────────┴─────────────────────────────────────┘
```

---

# Key Components

* **VPC** – A private virtual network in AWS.
* **CIDR Block** – Defines the IP address range of the VPC.
* **Public Subnet** – Hosts internet-facing resources like web servers and load balancers.
* **Private Subnet** – Hosts internal resources like application servers and databases.
* **Internet Gateway (IGW)** – Enables internet connectivity for public subnets.
* **NAT Gateway** – Allows private subnet resources to access the internet securely for updates without accepting inbound internet traffic.
* **Route Table** – Determines how network traffic is routed within the VPC.
* **Security Groups** – Instance-level firewalls that control inbound and outbound traffic.
* **Network ACLs (NACLs)** – Subnet-level firewalls providing an additional layer of security.

---

## Real-World Example

Consider an e-commerce application:

* Users access the website through the **Internet**.
* Traffic enters the VPC via the **Internet Gateway**.
* A **Load Balancer** distributes requests to **EC2 web servers** in the **Public Subnet**.
* The web servers communicate with **Application Servers** in the **Private Subnet**.
* Application servers store and retrieve data from an **Amazon RDS** database, which remains inaccessible from the public internet.
* If private resources need software updates, they access the internet securely through the **NAT Gateway**.

This architecture ensures that only the web layer is publicly accessible, while the application and database layers remain protected, improving both security and scalability.

