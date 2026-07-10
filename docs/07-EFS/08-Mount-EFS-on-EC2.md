# Mount Amazon EFS on Amazon EC2

## Overview

After creating an Amazon Elastic File System (EFS), the next step is to mount it on an Amazon EC2 instance. Mounting allows the EC2 instance to access the EFS file system as if it were a local directory. Since EFS is a shared network file system, multiple EC2 instances can mount the same file system simultaneously using the **NFSv4 protocol**, enabling centralized and consistent data storage.

This practical demonstrates how to mount an EFS file system on an Amazon Linux EC2 instance and verify that it is working correctly.

---

# Amazon EFS Mounting Architecture

![Image](https://images.openai.com/static-rsc-4/SinBr_RRNiVOKnG6R5oExCoAMDqkLfUPCMzCB7Nq4a22Ct_z3mDwq0F-mU2O63iXZQ0BEY6bAAB9WJjT_QYOZnUTh8TaykFcfFcU1_DAxIuRsCADkDRqTfBazLljioMlDDFBviwMA1MWzdYZCOIac-QnhCbjhdJ5HhCprjjMfbCBeGiJDCiW-Vhl5JvZpZZz?purpose=fullsize)

---

# Prerequisites

Before mounting Amazon EFS, ensure you have:

* AWS Account
* Amazon EFS File System (Status: **Available**)
* Amazon EC2 Instance (Amazon Linux 2 or Amazon Linux 2023)
* EC2 and EFS in the same VPC
* Security Group allowing **TCP Port 2049 (NFS)**
* SSH access to the EC2 instance

---

# Step 1: Launch an EC2 Instance

1. Open the **Amazon EC2 Console**.
2. Click **Launch Instance**.
3. Select **Amazon Linux 2 AMI**.
4. Choose **t2.micro** (Free Tier eligible).
5. Select the same **VPC** where the EFS file system exists.
6. Launch the instance.

📸 **Screenshot 1**

```text
screenshots/11-ec2-launch.png
```

Capture:

* EC2 Launch page
* Instance Name
* AMI
* Instance Type
* VPC

---

# Step 2: Connect to the EC2 Instance

Connect using SSH.

```bash
ssh -i MyKey.pem ec2-user@<Public-IP>
```

Example:

```bash
ssh -i aws-key.pem ec2-user@13.233.xxx.xxx
```

📸 **Screenshot 2**

```text
screenshots/12-connect-ec2.png
```

Capture:

* Successful SSH login terminal

---

# Step 3: Update the System

```bash
sudo yum update -y
```

📸 **Screenshot 3**

```text
screenshots/13-system-update.png
```

Capture:

* Terminal showing update completion

---

# Step 4: Install Amazon EFS Utilities

Install the required package.

```bash
sudo yum install amazon-efs-utils -y
```

Verify installation.

```bash
rpm -q amazon-efs-utils
```

Expected Output:

```text
amazon-efs-utils-2.x.x
```

📸 **Screenshot 4**

```text
screenshots/14-install-efs-utils.png
```

Capture:

* Installation completed successfully

---

# Step 5: Create a Mount Directory

Create a directory where the EFS file system will be mounted.

```bash
sudo mkdir /mnt/efs
```

Verify:

```bash
ls /mnt
```

Expected Output:

```text
efs
```

📸 **Screenshot 5**

```text
screenshots/15-create-mount-directory.png
```

---

# Step 6: Copy the EFS DNS Name

Go to:

**Amazon EFS → Your File System → Attach**

Copy the DNS name.

Example:

```text
fs-0123456789abcdef0.efs.ap-south-1.amazonaws.com
```

📸 **Screenshot 6**

```text
screenshots/16-copy-dns-name.png
```

Capture:

* Attach page showing the mount command and DNS name

---

# Step 7: Mount the File System

Run:

```bash
sudo mount -t efs fs-0123456789abcdef0:/ /mnt/efs
```

Replace the File System ID with your own.

Alternatively:

```bash
sudo mount -t nfs4 \
fs-0123456789abcdef0.efs.ap-south-1.amazonaws.com:/ \
/mnt/efs
```

📸 **Screenshot 7**

```text
screenshots/17-mount-command.png
```

Capture:

* Successful mount command

---

# Step 8: Verify the Mount

Check mounted file systems.

```bash
df -h
```

Example Output:

```text
Filesystem      Size Used Avail Use% Mounted on
127.0.0.1:/     8.0E    0  8.0E   0% /mnt/efs
```

📸 **Screenshot 8**

```text
screenshots/18-df-output.png
```

---

# Step 9: Create a Test File

Navigate to the mounted directory.

```bash
cd /mnt/efs
```

Create a file.

```bash
echo "Amazon EFS Working Successfully" > test.txt
```

Verify:

```bash
cat test.txt
```

Expected Output:

```text
Amazon EFS Working Successfully
```

📸 **Screenshot 9**

```text
screenshots/19-create-test-file.png
```

---

# Step 10: Verify from Another EC2 Instance

Launch another EC2 instance.

Mount the same EFS.

Navigate to:

```bash
cd /mnt/efs
```

Display the file.

```bash
cat test.txt
```

Expected Output:

```text
Amazon EFS Working Successfully
```

This confirms that Amazon EFS is shared across multiple EC2 instances.

📸 **Screenshot 10**

```text
screenshots/20-second-ec2-verification.png
```

---

# Mounting Workflow

```text
          User
            │
            ▼
      SSH into EC2
            │
            ▼
 Install amazon-efs-utils
            │
            ▼
 Create Mount Directory
            │
            ▼
 Copy EFS DNS Name
            │
            ▼
 Mount Amazon EFS
            │
            ▼
 Verify using df -h
            │
            ▼
 Create Test File
            │
            ▼
 Access Same File from Another EC2
```

---

# Common Troubleshooting

| Problem                 | Cause                           | Solution                               |
| ----------------------- | ------------------------------- | -------------------------------------- |
| Mount failed            | Wrong DNS name                  | Verify File System ID                  |
| Connection timed out    | Port 2049 blocked               | Update Security Group                  |
| Permission denied       | Incorrect IAM or Security Group | Verify permissions                     |
| Mount command not found | EFS utilities missing           | Install `amazon-efs-utils`             |
| DNS resolution failed   | Different VPC                   | Ensure EC2 and EFS are in the same VPC |

---

# Best Practices

* Create **Mount Targets** in every Availability Zone.
* Allow only trusted Security Groups to access **TCP Port 2049**.
* Use **Amazon EFS Mount Helper (`amazon-efs-utils`)** for simplified mounting.
* Enable **encryption in transit** using TLS.
* Configure automatic mounting in `/etc/fstab` for persistence after reboot.
* Monitor usage with **Amazon CloudWatch**.
* Enable **AWS Backup** for regular backups.

---

# Conclusion

Mounting Amazon EFS on Amazon EC2 enables applications to use scalable and shared network storage without managing storage servers. Once mounted, the EFS file system behaves like a local directory, allowing multiple EC2 instances to access the same files concurrently. This architecture is ideal for web applications, content management systems, machine learning workloads, and shared development environments.

---

# 📂 Screenshots Folder

```text
screenshots/
├── 11-ec2-launch.png
├── 12-connect-ec2.png
├── 13-system-update.png
├── 14-install-efs-utils.png
├── 15-create-mount-directory.png
├── 16-copy-dns-name.png
├── 17-mount-command.png
├── 18-df-output.png
├── 19-create-test-file.png
└── 20-second-ec2-verification.png
```

---


