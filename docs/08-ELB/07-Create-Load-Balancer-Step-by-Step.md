# Create an Application Load Balancer (ALB) – Step-by-Step

## Overview

An **Application Load Balancer (ALB)** distributes incoming **HTTP/HTTPS** traffic across multiple EC2 instances. In this practical, you will create an ALB using the AWS Management Console, configure listeners, create a target group, register EC2 instances, and verify that the load balancer is working correctly.

---

# Application Load Balancer Creation Workflow

![Image](https://images.openai.com/static-rsc-4/VEYlZBNKPVVXtUSVizETXBqJuHuYInwKiaKaToGSdljjmBoFQTALxo8RokWLmP1cEfnr2N_9633G3VC2GxAz9Xo6_Uc77BmBUkKqtxpa6Xl4IHJTZE9nhleDWf4OhNr2QaLskyGZP-1S3GwoyUS_bskz4U57glQprLSvJcUTmtKAChmk4xGFZbiPN_D6EOqr?purpose=fullsize)

---

# Prerequisites

Before creating an ALB, ensure you have:

* AWS Account
* Amazon VPC
* Internet Gateway attached to the VPC
* Two Public Subnets (different Availability Zones)
* Two EC2 Instances with a running web server (Apache or Nginx)
* Security Groups configured
* Internet connectivity

---

# Step 1: Launch EC2 Instances

1. Open the **AWS Management Console**.
2. Navigate to **EC2 Dashboard**.
3. Click **Launch Instance**.
4. Create **two Amazon Linux 2** instances.
5. Place each instance in a different Availability Zone.

📸 **Screenshot 1**

```text
screenshots/01-launch-ec2.png
```

Capture:

* Instance Name
* AMI
* Instance Type
* VPC
* Subnet

---

# Step 2: Install Apache Web Server

Connect to each EC2 instance.

```bash
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
```

Create a unique homepage on each server.

**Server 1**

```bash
echo "<h1>Server 1</h1>" | sudo tee /var/www/html/index.html
```

**Server 2**

```bash
echo "<h1>Server 2</h1>" | sudo tee /var/www/html/index.html
```

📸 **Screenshot 2**

```text
screenshots/02-apache-installed.png
```

---

# Step 3: Open the EC2 Dashboard

Go to:

**AWS Console → EC2 → Load Balancers**

Click **Create Load Balancer**.

📸 **Screenshot 3**

```text
screenshots/03-load-balancer-dashboard.png
```

---

# Step 4: Choose Application Load Balancer

You will see four load balancer types.

Select:

✅ **Application Load Balancer**

Click **Create**.

📸 **Screenshot 4**

```text
screenshots/04-select-alb.png
```

---

# Step 5: Configure Basic Settings

Enter:

| Setting         | Value             |
| --------------- | ----------------- |
| Name            | My-Application-LB |
| Scheme          | Internet-facing   |
| IP Address Type | IPv4              |

📸 **Screenshot 5**

```text
screenshots/05-basic-settings.png
```

---

# Step 6: Select Network Mapping

Choose:

* VPC
* Public Subnet 1
* Public Subnet 2

Each subnet should belong to a different Availability Zone.

📸 **Screenshot 6**

```text
screenshots/06-network-mapping.png
```

---

# Step 7: Configure Security Group

Create or select a Security Group.

Allow:

| Type  | Port | Source               |
| ----- | ---- | -------------------- |
| HTTP  | 80   | 0.0.0.0/0            |
| HTTPS | 443  | 0.0.0.0/0 (optional) |

📸 **Screenshot 7**

```text
screenshots/07-security-group.png
```

---

# Step 8: Create a Target Group

Click **Create Target Group**.

Configure:

| Setting     | Value     |
| ----------- | --------- |
| Target Type | Instances |
| Protocol    | HTTP      |
| Port        | 80        |
| VPC         | Your VPC  |

Click **Next**.

📸 **Screenshot 8**

```text
screenshots/08-create-target-group.png
```

---

# Step 9: Register EC2 Instances

Select:

* EC2 Instance 1
* EC2 Instance 2

Click:

**Include as Pending Below**

Then click **Create Target Group**.

📸 **Screenshot 9**

```text
screenshots/09-register-targets.png
```

---

# Step 10: Attach Target Group to ALB

Return to the ALB creation page.

Choose the Target Group created in the previous step.

📸 **Screenshot 10**

```text
screenshots/10-attach-target-group.png
```

---

# Step 11: Review Configuration

Verify:

* Name
* Scheme
* Listeners
* Security Group
* VPC
* Subnets
* Target Group

Click **Create Load Balancer**.

📸 **Screenshot 11**

```text
screenshots/11-review-create.png
```

---

# Step 12: Wait Until Status Becomes Active

After creation:

Status:

```text
Active
```

📸 **Screenshot 12**

```text
screenshots/12-alb-active.png
```

---

# Step 13: Verify Healthy Targets

Navigate to:

**Target Groups → Targets**

Both EC2 instances should display:

```text
Healthy
```

📸 **Screenshot 13**

```text
screenshots/13-healthy-targets.png
```

---

# Step 14: Copy the DNS Name

Open:

**Load Balancer → Description**

Example:

```text
my-alb-123456789.ap-south-1.elb.amazonaws.com
```

📸 **Screenshot 14**

```text
screenshots/14-dns-name.png
```

---

# Step 15: Test the Load Balancer

Open the DNS name in a web browser:

```text
http://my-alb-123456789.ap-south-1.elb.amazonaws.com
```

Refresh multiple times to observe requests being served by different backend instances (if using round-robin and unique page content).

📸 **Screenshot 15**

```text
screenshots/15-browser-output.png
```

---

# Complete Workflow

```text
Launch EC2 Instances
        │
        ▼
Install Apache
        │
        ▼
Create Target Group
        │
        ▼
Register EC2 Instances
        │
        ▼
Create Application Load Balancer
        │
        ▼
Configure Security Group
        │
        ▼
Attach Target Group
        │
        ▼
Create ALB
        │
        ▼
Verify Health Checks
        │
        ▼
Copy DNS Name
        │
        ▼
Test in Browser
```

---

# Common Troubleshooting

| Problem                 | Possible Cause                  | Solution                            |
| ----------------------- | ------------------------------- | ----------------------------------- |
| Target Unhealthy        | Apache/Nginx not running        | Start the web server                |
| Health Check Failed     | Wrong health check path         | Verify the path (e.g., `/`)         |
| Timeout                 | Security Group blocking traffic | Allow HTTP (80)                     |
| 503 Service Unavailable | No healthy targets              | Check target health                 |
| DNS Not Working         | ALB still provisioning          | Wait until the status is **Active** |

---

# Best Practices

* Deploy instances across at least **two Availability Zones**.
* Use **HTTPS** with AWS Certificate Manager (ACM) in production.
* Enable **Cross-Zone Load Balancing**.
* Configure meaningful health check paths.
* Integrate with **Auto Scaling Groups**.
* Protect internet-facing ALBs with **AWS WAF** and **AWS Shield**.
* Monitor ALB metrics using **Amazon CloudWatch**.

---

# Conclusion

Creating an Application Load Balancer enables applications to distribute incoming traffic efficiently across multiple backend servers. By combining **Target Groups**, **Health Checks**, and **Security Groups**, ALB provides a highly available, scalable, and fault-tolerant architecture. Integrating ALB with Auto Scaling and CloudWatch further enhances performance and operational efficiency.

---


