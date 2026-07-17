# Create an Amazon EC2 Auto Scaling Group (ASG)

## Overview

An **Amazon EC2 Auto Scaling Group (ASG)** is a collection of EC2 instances that are managed together for automatic scaling and high availability. The Auto Scaling Group uses a **Launch Template** to launch new instances and maintains the desired number of instances by automatically adding or removing EC2 instances based on demand.

An Auto Scaling Group can also integrate with an **Application Load Balancer (ALB)** to distribute incoming traffic across healthy instances.

---

# Auto Scaling Group Architecture

![Image](https://images.openai.com/static-rsc-4/DG9lg6mJJKOTl-R9APK8EZsddbolm5nMDXxaCbzZNhu6XbGBQdvH7d5goYWuq_NRdIkOaRq7n276vdwwlwuaZhi7Hz5tCcpheBb1aephF3c_kA_DQDQo0UxvuH2BrFE3eAsxpNga3fXo31S-3Q4lOIEsaMsUIyh57LAYxPnT20oKDxb-tfbUt5KJE0OgcJIh?purpose=fullsize)

---

# Auto Scaling Group Workflow

```text
                    Internet
                        │
                        ▼
          Application Load Balancer (ALB)
                        │
                 Target Group
                        │
                        ▼
             Auto Scaling Group (ASG)
          ┌─────────────┼─────────────┐
          ▼             ▼             ▼
     EC2 Instance 1  EC2 Instance 2  EC2 Instance 3
                        ▲
                        │
                Launch Template
                        │
                        ▼
               Amazon CloudWatch
                        │
                Scaling Policies
```

---

# Prerequisites

Before creating an Auto Scaling Group, ensure you have:

* AWS Account
* Existing Amazon VPC
* At least two Public Subnets
* Launch Template
* Security Group
* IAM Role (optional)
* Application Load Balancer (optional)
* Target Group (if using ALB)

---

# Step 1: Open Auto Scaling Groups

1. Sign in to the **AWS Management Console**
2. Open **EC2 Dashboard**
3. Click **Auto Scaling Groups**
4. Select **Create Auto Scaling Group**

📸 **Screenshot 1**

```text
screenshots/11-asg-dashboard.png
```

---

# Step 2: Enter Auto Scaling Group Name

Example

| Field                   | Value              |
| ----------------------- | ------------------ |
| Auto Scaling Group Name | WebServer-ASG      |
| Launch Template         | WebServer-Template |

Click **Next**

📸 **Screenshot 2**

```text
screenshots/12-asg-name.png
```

---

# Step 3: Choose Network

Select:

* VPC
* Availability Zones
* Public Subnets

Example

| Setting            | Value                            |
| ------------------ | -------------------------------- |
| VPC                | Default VPC                      |
| Availability Zones | ap-south-1a, ap-south-1b         |
| Subnets            | Public Subnet A, Public Subnet B |

📸 **Screenshot 3**

```text
screenshots/13-network.png
```

---

# Step 4: Attach Load Balancer (Optional)

Choose:

* Attach to an existing Load Balancer
* Select an existing Target Group

Example

```text
Application Load Balancer

↓

Target Group

↓

Auto Scaling Group
```

📸 **Screenshot 4**

```text
screenshots/14-load-balancer.png
```

---

# Step 5: Configure Health Checks

Enable:

* EC2 Health Checks
* Elastic Load Balancer Health Checks

Example

| Health Check | Enabled |
| ------------ | ------- |
| EC2          | Yes     |
| ELB          | Yes     |

Health Check Grace Period:

```text
300 Seconds
```

📸 **Screenshot 5**

```text
screenshots/15-health-check.png
```

---

# Step 6: Configure Group Size

Set the capacity values.

Example

| Capacity         | Value |
| ---------------- | ----: |
| Desired Capacity |     2 |
| Minimum Capacity |     2 |
| Maximum Capacity |     6 |

📸 **Screenshot 6**

```text
screenshots/16-capacity.png
```

---

# Step 7: Configure Scaling Policy

Recommended:

**Target Tracking Scaling Policy**

Example

Target Metric

```text
Average CPU Utilization = 50%
```

AWS automatically scales the instances to maintain this target.

📸 **Screenshot 7**

```text
screenshots/17-scaling-policy.png
```

---

# Step 8: Configure Notifications (Optional)

Use **Amazon SNS** to receive notifications.

Examples

* EC2 launched
* EC2 terminated
* Scaling activity
* Health check failure

📸 **Screenshot 8**

```text
screenshots/18-notifications.png
```

---

# Step 9: Add Tags

Example

| Key         | Value       |
| ----------- | ----------- |
| Name        | WebServer   |
| Environment | Production  |
| Project     | AutoScaling |

📸 **Screenshot 9**

```text
screenshots/19-tags.png
```

---

# Step 10: Review and Create

Review all settings.

Click:

**Create Auto Scaling Group**

📸 **Screenshot 10**

```text
screenshots/20-review-create.png
```

---

# Verify Auto Scaling Group

After creation, verify:

* Auto Scaling Group status
* Desired capacity
* Running EC2 instances
* Activity history
* Scaling policies
* Health status

Expected Output

```text
Auto Scaling Group

Status : Active

Desired Capacity : 2

Running Instances : 2

Health Status : Healthy
```

---

# Auto Scaling Group Lifecycle

```text
Create Launch Template
          │
          ▼
Create Auto Scaling Group
          │
          ▼
Launch EC2 Instances
          │
          ▼
Health Checks
          │
          ▼
Receive Traffic
          │
          ▼
CloudWatch Monitoring
          │
     ┌────┴────┐
     ▼         ▼
Scale Out   Scale In
```

---

# Capacity Example

| CPU Utilization | Action                 |
| --------------- | ---------------------- |
| 25%             | Keep 2 Instances       |
| 55%             | Launch 1 Instance      |
| 75%             | Launch 2 Instances     |
| 90%             | Launch 4 Instances     |
| 20%             | Remove Extra Instances |

---

# Best Practices

* Use **Launch Templates** instead of Launch Configurations.
* Deploy instances across multiple Availability Zones.
* Enable **ELB Health Checks**.
* Configure **Target Tracking Scaling Policies**.
* Set realistic minimum, desired, and maximum capacities.
* Use **Amazon SNS** for scaling notifications.
* Monitor Auto Scaling Groups using **Amazon CloudWatch**.
* Apply resource tags for better management and cost allocation.

---

# Real-World Example

A news website expects heavy traffic during breaking news events.

* The Auto Scaling Group starts with **2 EC2 instances**.
* When CPU utilization exceeds **70%**, CloudWatch triggers the scaling policy.
* Two additional EC2 instances are launched automatically from the Launch Template.
* The Application Load Balancer registers the new instances and distributes incoming traffic.
* When traffic decreases below **30%**, Auto Scaling safely terminates the extra instances while maintaining the minimum required capacity.

---

# Conclusion

Amazon EC2 Auto Scaling Groups provide automatic capacity management, ensuring applications remain highly available and cost-efficient. By integrating Launch Templates, CloudWatch, and Elastic Load Balancers, Auto Scaling Groups automatically respond to changing workloads while maintaining application performance and reliability.

---
