# Amazon EC2 Auto Scaling Policies

## Overview

**Scaling Policies** define **when**, **how**, and **by how much** an Auto Scaling Group (ASG) should increase or decrease the number of EC2 instances. They use **Amazon CloudWatch metrics** to automatically respond to changes in application demand, ensuring high availability, fault tolerance, and cost optimization.

Auto Scaling supports multiple policy types to handle different workload patterns, from unpredictable traffic spikes to scheduled business-hour workloads.

---

# Auto Scaling Policies Architecture

![Image](https://images.openai.com/static-rsc-4/UX0osOSfhkMekU5yXAMOKfZ7SwTGEg0WXTfBhEgqFyX-e-lwa7eE6A8U1WZ_qLky43Ic9u_5CLEpbznDjfGHStrkDlU8dMDqXlphjN0eaVDPROgTWHheDdi1yb5xrSX2wzC3J_bwZv4J-Aj__yu0MoH9B3UsCxru-FCLQ9wD1RI3J4NSjPmMJFRRY8Kocobl?purpose=fullsize)


---

# Scaling Policy Workflow

```text
                  Amazon CloudWatch
                         │
                  Monitor Metrics
                         │
               CloudWatch Alarm Triggered
                         │
                         ▼
                Auto Scaling Policy
        ┌────────────┬─────────────┬────────────┐
        ▼            ▼             ▼
  Scale Out      Scale In      No Action
        │            │
        ▼            ▼
 Launch EC2     Terminate EC2
        │
        ▼
 Application Load Balancer
```

---

# What is a Scaling Policy?

A **Scaling Policy** is a set of rules that automatically adjusts the number of EC2 instances based on monitoring metrics such as:

* CPU Utilization
* Memory Utilization (CloudWatch Agent)
* Network In
* Network Out
* Request Count per Target
* Custom CloudWatch Metrics

---

# Types of Scaling Policies

| Policy             | Best For                     | Automatic |
| ------------------ | ---------------------------- | --------- |
| Target Tracking    | Most production applications | ✅         |
| Step Scaling       | Large traffic spikes         | ✅         |
| Simple Scaling     | Small workloads              | ✅         |
| Scheduled Scaling  | Predictable traffic          | ✅         |
| Predictive Scaling | Recurring workloads          | ✅         |

---

# 1. Target Tracking Scaling Policy

## Overview

Target Tracking keeps a selected metric close to a target value.

Example:

```text
Target CPU Utilization = 50%

Current CPU = 75%

↓

Launch New EC2 Instance
```

When CPU usage falls:

```text
Current CPU = 25%

↓

Terminate EC2 Instance
```

### Supported Metrics

* Average CPU Utilization
* ALB Request Count Per Target
* Network In
* Network Out
* Custom Metrics

### Advantages

* Easy to configure
* AWS recommended
* Automatic adjustment
* Stable application performance

---

# 2. Step Scaling Policy

## Overview

Step Scaling performs different scaling actions depending on how far the metric exceeds or falls below a threshold.

### Example

| CPU Usage | Action          |
| --------- | --------------- |
| 60–70%    | Add 1 Instance  |
| 70–85%    | Add 2 Instances |
| Above 85% | Add 4 Instances |

Workflow

```text
CPU = 92%

↓

Launch 4 EC2 Instances
```

### Advantages

* Fine-grained control
* Better for sudden traffic spikes
* Faster response

---

# 3. Simple Scaling Policy

## Overview

Simple Scaling performs one scaling action for each CloudWatch Alarm.

Example:

```text
CPU > 70%

↓

Launch 1 EC2

↓

Cooldown (300 sec)
```

After the cooldown period ends, another scaling action may occur.

### Advantages

* Easy setup
* Suitable for small applications

### Limitation

* Slower response because of the cooldown period

---

# 4. Scheduled Scaling Policy

## Overview

Scheduled Scaling adjusts capacity at predefined times.

Example

| Time     | Desired Capacity |
| -------- | ---------------- |
| 09:00 AM | 6                |
| 06:00 PM | 3                |
| 11:00 PM | 2                |

Workflow

```text
09:00 AM

↓

Increase Capacity

↓

6 EC2 Instances
```

### Best For

* Office applications
* Educational portals
* Business-hour workloads

---

# 5. Predictive Scaling Policy

## Overview

Predictive Scaling uses **AWS Machine Learning** to forecast future traffic based on historical data.

Workflow

```text
Historical Metrics

↓

Machine Learning

↓

Forecast Future Traffic

↓

Launch EC2 Before Peak
```

### Advantages

* Launches capacity before demand increases
* Reduces latency
* Improves user experience

---

# Creating a Target Tracking Policy (AWS Console)

## Step 1

Open:

**EC2 → Auto Scaling Groups**

Select your Auto Scaling Group.

📸 Screenshot 1

```text
screenshots/21-open-asg.png
```

---

## Step 2

Open the **Automatic Scaling** tab.

Click:

**Create Dynamic Scaling Policy**

📸 Screenshot 2

```text
screenshots/22-create-policy.png
```

---

## Step 3

Choose:

```
Policy Type

↓

Target Tracking
```

Select Metric

```
Average CPU Utilization
```

Target Value

```
50%
```

📸 Screenshot 3

```text
screenshots/23-target-tracking.png
```

---

## Step 4

Click

```
Create
```

The scaling policy becomes active immediately.

📸 Screenshot 4

```text
screenshots/24-create.png
```

---

# AWS CLI Example

### Create Target Tracking Policy

```bash
aws autoscaling put-scaling-policy \
  --auto-scaling-group-name WebServer-ASG \
  --policy-name TargetTrackingCPU \
  --policy-type TargetTrackingScaling \
  --target-tracking-configuration file://tracking.json
```

---

### Describe Scaling Policies

```bash
aws autoscaling describe-policies \
  --auto-scaling-group-name WebServer-ASG
```

---

### Delete Scaling Policy

```bash
aws autoscaling delete-policy \
  --auto-scaling-group-name WebServer-ASG \
  --policy-name TargetTrackingCPU
```

---

# CloudWatch Alarm Integration

```text
CloudWatch

↓

CPU > 70%

↓

Alarm Triggered

↓

Scaling Policy

↓

Launch EC2

↓

Register with ALB

↓

Serve Traffic
```

---

# Real-World Example

An online learning platform hosts live classes every weekday.

* During class hours (9:00 AM–5:00 PM), **Scheduled Scaling** increases the desired capacity.
* If CPU utilization exceeds **70%**, **Target Tracking Scaling** automatically launches additional EC2 instances.
* During unexpected traffic surges, **Step Scaling** adds multiple instances based on CPU thresholds.
* At night, Auto Scaling terminates unnecessary instances to reduce infrastructure costs.

---

# Best Practices

* Use **Target Tracking Scaling** for most production workloads.
* Combine **Scheduled Scaling** with **Target Tracking** for predictable traffic.
* Configure realistic CloudWatch thresholds.
* Test scaling policies in a staging environment.
* Monitor scaling activities using **Amazon CloudWatch**.
* Avoid aggressive scaling thresholds that can cause frequent scale-in and scale-out (known as scaling oscillation).
* Use **Predictive Scaling** for workloads with recurring traffic patterns.

---

# Conclusion

Amazon EC2 Auto Scaling Policies automate infrastructure scaling by responding to real-time and predicted demand. Whether using **Target Tracking**, **Step Scaling**, **Simple Scaling**, **Scheduled Scaling**, or **Predictive Scaling**, these policies help maintain application performance, improve availability, and optimize AWS costs while reducing manual intervention.

---


