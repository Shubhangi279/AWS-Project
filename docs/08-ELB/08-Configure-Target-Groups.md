# Configure Target Groups in Elastic Load Balancer (ELB)

## Overview

A **Target Group** is a logical collection of backend resources that receive traffic from an **Elastic Load Balancer (ELB)**. Instead of sending requests directly to EC2 instances, the Load Balancer forwards traffic to a Target Group, which then routes requests to healthy registered targets.

Target Groups also perform **health checks** to ensure that only healthy targets receive application traffic.

---

# Target Group Architecture

![Image](https://images.openai.com/static-rsc-4/v2dIHO-Hg5kV5WvhlVj5AcZqVsqsb89t4HurzPlKoeo0pyUtz2TvWh-ZAOKlIaR1hbX8JHKfwKBL7sYTJLEPpqCS5caaJv23JgXlpgp-aGIFGT7CXKes7iaN4kj0oAnJWvZNhv2N2h0f-rRiBNzvt88U07b8tH93xVtYSQHGTIICEJ-e07Ezfu_S8rhITKGb?purpose=fullsize)

---

# Target Group Workflow

```text
                Internet
                    │
                    ▼
        Application Load Balancer
                    │
             Listener (80/443)
                    │
                    ▼
              Target Group
         ┌──────────┴──────────┐
         ▼                     ▼
   EC2 Instance 1        EC2 Instance 2
     (Healthy)             (Healthy)
```

---

# What is a Target Group?

A **Target Group** acts as a bridge between the **Load Balancer** and backend servers.

### Responsibilities

* Receive traffic from the Load Balancer
* Route requests to registered targets
* Monitor target health
* Automatically stop sending traffic to unhealthy targets

---

# Types of Target Groups

| Target Type    | Description                            | Common Use Case         |
| -------------- | -------------------------------------- | ----------------------- |
| **Instance**   | Routes traffic to EC2 instances        | Web applications        |
| **IP Address** | Routes traffic to private IP addresses | Hybrid environments     |
| **AWS Lambda** | Invokes Lambda functions               | Serverless applications |

---

# Step 1: Open Target Groups

1. Open the **AWS Management Console**
2. Navigate to **EC2 Dashboard**
3. In the left menu, select **Target Groups**
4. Click **Create Target Group**

📸 **Screenshot 1**

```text
screenshots/16-target-groups-dashboard.png
```

---

# Step 2: Choose Target Type

Select the target type.

Example:

| Option      | Selected  |
| ----------- | --------- |
| Target Type | Instances |
| Protocol    | HTTP      |
| Port        | 80        |

📸 **Screenshot 2**

```text
screenshots/17-select-target-type.png
```

---

# Step 3: Configure Basic Details

Enter:

| Setting           | Example          |
| ----------------- | ---------------- |
| Target Group Name | Web-Target-Group |
| Protocol          | HTTP             |
| Port              | 80               |
| VPC               | Default VPC      |

Click **Next**.

📸 **Screenshot 3**

```text
screenshots/18-configure-target-group.png
```

---

# Step 4: Configure Health Checks

Health Checks determine whether a target is healthy.

Recommended settings:

| Setting             | Value      |
| ------------------- | ---------- |
| Protocol            | HTTP       |
| Path                | `/`        |
| Interval            | 30 seconds |
| Timeout             | 5 seconds  |
| Healthy Threshold   | 5          |
| Unhealthy Threshold | 2          |

📸 **Screenshot 4**

```text
screenshots/19-health-check-settings.png
```

---

# Step 5: Register Targets

Select the EC2 instances to receive traffic.

Example:

* Web-Server-1
* Web-Server-2

Click **Include as Pending Below**, then **Create Target Group**.

📸 **Screenshot 5**

```text
screenshots/20-register-targets.png
```

---

# Step 6: Verify Registered Targets

After creation, open the Target Group and select the **Targets** tab.

Expected status:

```text
Target 1 - Healthy
Target 2 - Healthy
```

📸 **Screenshot 6**

```text
screenshots/21-healthy-targets.png
```

---

# Registering and Deregistering Targets

### Register a Target

1. Open the Target Group.
2. Click **Register Targets**.
3. Select EC2 instances.
4. Click **Include as Pending Below**.
5. Click **Register Pending Targets**.

### Deregister a Target

1. Open the Target Group.
2. Select the target.
3. Click **Deregister**.

This is useful during server maintenance or upgrades.

---

# Target Group Attributes

| Attribute                | Description                     |
| ------------------------ | ------------------------------- |
| Protocol                 | HTTP, HTTPS, TCP, TLS, UDP      |
| Port                     | Application listening port      |
| Health Checks            | Monitors target health          |
| Stickiness               | Maintains user sessions         |
| Deregistration Delay     | Waits before removing a target  |
| Load Balancing Algorithm | Determines request distribution |

---

# Health Check Process

```text
Application Load Balancer
           │
           ▼
     Health Check
           │
     ┌─────┴─────┐
     ▼           ▼
 Healthy     Unhealthy
     │           │
Receives    No Traffic
 Traffic
```

---

# Target Group Lifecycle

```text
Create Target Group
        │
        ▼
Register Targets
        │
        ▼
Run Health Checks
        │
        ▼
Healthy Targets Receive Traffic
        │
        ▼
Unhealthy Targets Removed
        │
        ▼
Target Recovers
        │
        ▼
Automatically Added Back
```

---

# Best Practices

* Use separate Target Groups for different applications or microservices.
* Configure Health Checks with realistic paths (such as `/health`).
* Register instances across multiple Availability Zones.
* Enable **Stickiness** only if your application requires session affinity.
* Monitor Target Group health using **Amazon CloudWatch**.
* Remove unused targets to simplify management.

---

# Real-World Example

A company hosts an e-commerce platform:

* **Target Group A** serves the website frontend.
* **Target Group B** serves REST APIs.
* The **Application Load Balancer** routes `/api/*` requests to the API Target Group and all other requests to the frontend Target Group.
* If one EC2 instance fails, Health Checks automatically stop sending traffic to it until it recovers.

This architecture ensures high availability and a seamless user experience.

---

# Conclusion

Target Groups are a core component of AWS Elastic Load Balancer. They organize backend resources, perform continuous health checks, and ensure that traffic is routed only to healthy targets. Properly configured Target Groups improve application reliability, simplify traffic management, and enable scalable cloud architectures.

---

