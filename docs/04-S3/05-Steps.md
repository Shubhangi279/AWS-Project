# Amazon S3 — Step-by-Step Setup Guide (With Screenshots)

---

## Introduction

**Amazon Simple Storage Service (S3)** is an object storage service provided by **Amazon Web Services** used to store and retrieve unlimited data securely from anywhere.

---

# Step 1 — Login to AWS Console

1. Open AWS Console
2. Enter credentials
3. Login successfully

<img width="1889" height="907" alt="Screenshot 2026-04-12 154330" src="https://github.com/user-attachments/assets/2510a731-a3de-4131-9013-fe4c8efcc9ea" />

---

# Step 2 — Open Amazon S3 Service

1. Go to search bar
2. Type **S3**
3. Click **Amazon S3**

<img width="1911" height="916" alt="image" src="https://github.com/user-attachments/assets/0401e353-e1de-4172-a084-434b4470e84b" />

---

# Step 3 — Create S3 Bucket

1. Click **Create bucket**
2. Enter bucket name
   Example:

```
my-first-s3-bucket
```

3. Select Region
   Example: Asia Pacific (Mumbai)
4. Keep default settings
5. Click **Create bucket**

<img width="1912" height="907" alt="image" src="https://github.com/user-attachments/assets/27787971-c13b-497e-81ee-1fc422c98264" />

 ---

# Step 4 — Bucket Created Successfully

You will see your bucket listed.

<img width="1912" height="902" alt="image" src="https://github.com/user-attachments/assets/31451321-3cbc-4b11-ba2b-15c1525ead98" />

---

# Step 5 — Upload Object (File)

1. Open created bucket
2. Click **Upload**
3. Click **Add files**
4. Select file
5. Click **Upload**

<img width="1915" height="910" alt="image" src="https://github.com/user-attachments/assets/1101de24-ec35-4919-86e2-f3a1c275a741" />

---

# Step 6 — View Uploaded Object

Your file appears inside bucket.

Example:

```
index.html
image.png
document.pdf
```
<img width="1913" height="907" alt="image" src="https://github.com/user-attachments/assets/5e3dbf85-87c9-4cf5-9b58-6514858db445" />

---

# Step 7 — Enable Versioning

1. Open **Properties**
2. Scroll to **Bucket Versioning**
3. Click **Edit**
4. Select **Enable**
5. Save changes

<img width="1910" height="900" alt="image" src="https://github.com/user-attachments/assets/836e5fbd-72f1-4eb0-9548-631883160bf5" />

---

# Step 8 — Make Object Public (Optional)

For testing / website hosting only.

1. Select object
2. Click **Actions**
3. Choose **Make public**

📸 **Screenshot**

```
(Add Screenshot Here)
Public Access Enabled
```

---

# Step 9 — Enable Static Website Hosting

1. Go to **Properties**
2. Scroll to **Static Website Hosting**
3. Enable hosting
4. Enter:

```
index.html
```

<img width="1913" height="897" alt="image" src="https://github.com/user-attachments/assets/809368bb-035b-4ccf-9074-1b321cf7096d" />

---

# Step 10 — Access Website URL

AWS generates website endpoint URL.



---

# Final Workflow

```
Login → Open S3 → Create Bucket → Upload Object → Enable Versioning → Host Website
```

---
