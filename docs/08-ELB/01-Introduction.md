# Elastic Load Balancer (ELB)

## Overview

Amazon **Elastic Load Balancer (ELB)** is a fully managed AWS service that automatically distributes incoming application traffic across multiple targets, such as **Amazon EC2 instances, containers, IP addresses, and AWS Lambda functions**. It helps improve the **availability, scalability, fault tolerance, and performance** of applications by ensuring that no single server becomes overloaded.

ELB continuously monitors the health of registered targets using **health checks** and routes traffic only to healthy resources. If an instance becomes unhealthy, ELB automatically stops sending requests to it until it recovers.

Whether you are running a small web application or a large enterprise system, ELB provides secure and efficient traffic distribution without requiring manual intervention.

---

# Elastic Load Balancer Architecture

![Image](https://images.openai.com/static-rsc-4/niJxL9JmsDhD-OVPmA_6TSNd0id3BtKuXl0DQD0cza2K0btHvcKPse-8HYqQEw8pNIbou_wTyiUKm3mHxkyjyj9nxaoBwhNF6XCIFxAHsRsOJAPtLsTFqO-vVrHMHKvnV9ckEPib_uwJHrCvpbLc2yjh2fqk-v_izVEonaVeVoPJ9H5BpvW-JuYf6_52677M?purpose=fullsize)

---

# Architecture Diagram

```text
                     Internet Users
                           │
                           ▼
                 Elastic Load Balancer
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
        ▼                  ▼                  ▼
   EC2 Instance 1     EC2 Instance 2     EC2 Instance 3
   (Healthy)          (Healthy)          (Healthy)
        │                  │                  │
        └──────────────────┼──────────────────┘
                           │
                           ▼
                    Application Response
```

---

# Why Do We Need a Load Balancer?

Without a Load Balancer:

```text
Internet
    │
    ▼
EC2 Instance
```

Problems:

* Single Point of Failure
* Server overload during high traffic
* Poor application performance
* No automatic failover
* Limited scalability

---

With Elastic Load Balancer:

```text
Internet
    │
    ▼
Elastic Load Balancer
    │
 ┌──┴───┐
 ▼      ▼
EC2-1  EC2-2
```

Benefits:

* Traffic distributed automatically
* High availability
* Fault tolerance
* Better performance
* Automatic failover

---

# How ELB Works

1. A user sends a request to the application.
2. The request reaches the Elastic Load Balancer.
3. ELB checks the health of all registered targets.
4. It selects a healthy target using a routing algorithm.
5. The selected target processes the request.
6. The response is returned to the user through the Load Balancer.

---

# Key Features

| Feature                        | Description                                                         |
| ------------------------------ | ------------------------------------------------------------------- |
| Automatic Traffic Distribution | Distributes incoming requests across multiple targets               |
| High Availability              | Works across multiple Availability Zones                            |
| Health Checks                  | Routes traffic only to healthy targets                              |
| Fault Tolerance                | Automatically redirects traffic if an instance fails                |
| Auto Scaling Integration       | Supports dynamic addition and removal of instances                  |
| SSL/TLS Termination            | Offloads SSL encryption from backend servers                        |
| Cross-Zone Load Balancing      | Evenly distributes traffic across Availability Zones                |
| IPv4 & IPv6 Support            | Supports both network protocols                                     |
| AWS Integration                | Works with EC2, ECS, EKS, Lambda, Auto Scaling, ACM, and CloudWatch |

---

# Benefits of ELB

* Improves application availability
* Increases fault tolerance
* Automatically scales with traffic
* Simplifies infrastructure management
* Enhances application performance
* Supports secure HTTPS connections
* Integrates seamlessly with other AWS services

---

# Real-World Example

An online shopping website experiences heavy traffic during a festive sale.

Without ELB:

* One EC2 instance receives all user requests.
* The server becomes overloaded.
* Users experience slow response times or service outages.

With ELB:

* Requests are distributed across multiple EC2 instances.
* If one instance fails, traffic is automatically redirected to healthy instances.
* Users continue accessing the website without interruption.

---

# Common Use Cases

* E-commerce websites
* Banking applications
* Online learning platforms
* Streaming services
* SaaS applications
* APIs and microservices
* Enterprise web applications
* Gaming platforms

---

# Advantages

* Fully managed by AWS
* Automatic traffic distribution
* Supports multiple Availability Zones
* Continuous health monitoring
* Easy integration with Auto Scaling
* Improved application performance
* High reliability
* Secure communication with HTTPS

---

# Limitations

* Additional AWS cost
* Initial configuration required
* Depends on correctly configured target groups and health checks
* Some advanced routing features are available only in specific ELB types

---

# Summary

Amazon Elastic Load Balancer (ELB) is an essential AWS networking service that distributes incoming traffic across multiple compute resources to ensure high availability, scalability, and fault tolerance. By automatically routing requests to healthy targets and integrating with services such as EC2, Auto Scaling, CloudWatch, and AWS Certificate Manager, ELB simplifies application deployment and improves user experience.

---

