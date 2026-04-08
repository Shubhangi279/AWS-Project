# Amazon EC2 Instance Lifecycle

An **EC2 Instance Lifecycle** describes the different states an instance goes through — from creation to termination — inside **Amazon Web Services**.

Understanding lifecycle states helps you:

✅ Manage servers efficiently
✅ Reduce AWS costs
✅ Control application availability
✅ Avoid accidental data loss

---

## EC2 Instance Lifecycle Diagram

![Image](https://media.licdn.com/dms/image/v2/D5622AQFyymmwBh4GKA/feedshare-shrink_2048_1536/feedshare-shrink_2048_1536/0/1719149036830?e=2147483647\&t=hgZ5ewqLHtA0qoy9mBa4671PWHeAQb_jVsT8311GDd4\&v=beta)

---

# EC2 Lifecycle States

---

## 1️⃣ Pending State

**What happens:**

* Instance is launching
* AWS allocates resources (CPU, RAM, Network)
* Operating system boots

Instance is **not yet usable**

**Billing:** Not charged

---

## 2️⃣ Running State

**What happens:**

* Instance becomes active
* Applications start running
* Users can connect via SSH/RDP

This is the **working state**.

**Billing:** Charged

---

## 3️⃣ Stopping State

Occurs when you stop the instance.

**Actions performed:**

* OS shutdown begins
* Compute resources released
* EBS volume preserved

Temporary shutdown phase.

**Billing:** Compute charges stop

---

## 4️⃣ Stopped State

**What happens:**

* Instance is powered off
* Data stored safely on EBS
* Instance can be restarted anytime

Good for saving costs.

**Billing:**

* No compute charge
* Storage charges apply

---

## 5️⃣ Rebooting (Special Transition)

Reboot restarts the instance without stopping it.

* Same physical host
* No data loss
* Quick restart

**Billing:** Continues

---

## 6️⃣ Shutting-down State

Triggered when instance is terminated.

**Process:**

* AWS releases resources
* Instance prepares for deletion

---

## 7️⃣ Terminated State

Final lifecycle stage.

Instance permanently deleted
Cannot be restarted

**Important:**
Root volume may also be deleted depending on settings.

**Billing:** Stops completely

---

# 🔄 Lifecycle Flow Summary

```
Launch
   ↓
Pending
   ↓
Running
   ↓        ↓
Stop     Terminate
 ↓            ↓
Stopping   Shutting-down
 ↓            ↓
Stopped     Terminated
```

---

# Billing Behavior by State

| State      | Billing      |
| ---------- | ------------ |
| Pending    | No           |
| Running    | Yes          |
| Stopping   | No           |
| Stopped    | Storage Only |
| Rebooting  | Yes          |
| Terminated | No           |

---

# Important Notes

✅ Stopping ≠ Terminating
✅ Stopped instances can restart
✅ Terminated instances are permanent
✅ Billing mainly occurs in **Running state**

---

# Why Lifecycle Knowledge Matters

* Prevent unnecessary AWS charges
* Improve cloud cost optimization
* Ensure proper server management
* Essential for AWS certification exams

---
