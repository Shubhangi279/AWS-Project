## Amazon S3 — Buckets & Objects

---

## What is an S3 Bucket?

An **S3 Bucket** is a container used to store data in **Amazon Web Services**.

Think of a bucket like a **main folder in the cloud** where all files are stored.

### Bucket Characteristics

* Bucket name must be **globally unique**
* Created in a specific AWS Region
* Stores unlimited files (objects)
* Used to organize data

---

## What are S3 Objects?

An **Object** is the actual data stored inside a bucket.

Each object contains:

* File (Image, Video, PDF, Backup, Logs)
* Metadata (information about file)
* Unique Object Key (file name/path)

### Example Structure

```
Bucket: my-website-bucket
   ├── index.html
   ├── images/logo.png
   ├── videos/demo.mp4
   └── backup.zip
```

---

## Bucket & Object Relationship

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/ed65b7fb-d9e4-4b29-8009-0ecae328f2d8" />


---

## How Buckets and Objects Work

1. Create an S3 Bucket
2. Upload files (Objects)
3. Store data securely
4. Access files using URL or API

```
User → Upload → Bucket → Object Stored
```

---

## Key Difference

| Feature  | Bucket            | Object           |
|----------|-------------------|------------------|
| Meaning  | Storage container | Actual file      |
| Example  | Folder            | File             |
| Limit    | Unlimited objects | Single data item |
| Contains | Objects           | Data + Metadata  |

---

## Real-World Example

* Bucket → **Google Drive Folder**
* Object → **Files inside folder**

---
