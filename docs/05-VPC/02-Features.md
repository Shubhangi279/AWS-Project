# Features of Amazon VPC

Amazon Virtual Private Cloud (VPC) provides a secure and customizable networking environment for AWS resources. It offers several features that help organizations build scalable, reliable, and highly secure cloud infrastructures.

---

## 1. Logical Isolation

![Image](https://images.openai.com/static-rsc-4/R-qd33tzad1oBPFlN2FTyP0FLN2YJ8AhvDWvSIiaKS4n-Tc8QLnlcxMOqTh_5-uHZCYtlf0bcjSBbzHamXgJQnOWBsHCcyOT1W8MQsOdDYvb_uwoN7Oui3cLgSJoKpbLNb55JPB6_X5kBx4bzs7oVAw42OAUKgt4YpGU-BP99V8chgYo_42g_hNhpykGVHMr?purpose=fullsize)


A VPC creates a **logically isolated network** within the AWS Cloud. Resources inside one VPC are separated from resources in other VPCs unless you explicitly connect them using services such as **VPC Peering** or **Transit Gateway**.

**Benefits**

* Improved security
* Network isolation
* Better resource management

---

## 2. Custom IP Address Range (CIDR Block)

![Image](https://images.openai.com/static-rsc-4/iy3SwrAOYuqaNyKA_pBNhXx8uJi9cC6-KtNCeI-0SOfbVrbWPIfVw7ZgkZukqPZpPFRp-x7rXVpd17QmHZOocasytD7JGaVQTcNlOhQqNYxzD11SR53CsWTCOT7aNJXbRl5_W_Py9M59HIXF6RznIuR7esqdGbwS4oky-Y3P4luGRowPofqn03PZinbd69t0?purpose=fullsize)


When creating a VPC, you define its IP address range using **CIDR (Classless Inter-Domain Routing)** notation.

**Example**

```text
VPC CIDR : 10.0.0.0/16

Public Subnet : 10.0.1.0/24

Private Subnet : 10.0.2.0/24
```

This provides flexibility in designing your network.

---

## 3. Public and Private Subnets

![Image](https://images.openai.com/static-rsc-4/5lafimV2cxgorfI2Dw0fjyVhc37Wg5uue4P4BMrihemnRVGujZEo5J3sw6Tj4roL7wZTvXT54XxozS5otUNiOpqe848oI_udkW8RUFHxC-MLkvu47vkTTWoe99p1q-upxg0rYtV066F17jdjntqWuq4_z-uwo83wox_RfvZQQQJmc9E0vwT6mw0QnmCsS2Zg?purpose=fullsize)


A VPC can be divided into multiple **subnets**.

### Public Subnet

* Connected to the Internet Gateway
* Hosts web servers and load balancers
* Accessible from the internet

### Private Subnet

* No direct internet access
* Hosts databases and application servers
* More secure

---

## 4. Internet Connectivity

![Image](https://images.openai.com/static-rsc-4/E4l-ir239UM9PgK1LCCp3p2gHpv9ma6bTtiUA7z5aAMhD-_DuEDz8IUXi7yBF7l-EMe1UXkcws7jUOC68A5W35fl_Ob4kElwd04inkXRqBXUgPdysTJE3ST7wRqMhaDvr3RToQyok_N0RKUrrlgPBLHi5iEPDdiQoKtkoB187dhPLZPmA_1PbuHtaxDVudD7?purpose=fullsize)


Amazon VPC provides internet access using an **Internet Gateway (IGW)**.

Features:

* Incoming internet traffic
* Outgoing internet traffic
* Public IP support

---

## 5. NAT Gateway

![Image](https://images.openai.com/static-rsc-4/Bi1Kjzo73alETw9eCBNmG2n7_cWBF6m95-UJ-nulzEqfnMkTTglAnVonefHBZfmmmIoLHm5GPNapIu-bXO3Sc_4kYctCjN5pmHkIuV1mGxls_5Xqt4qvj8dCb-nDyQBT7olEA5JZHsLjk4cqgFkHFBB8554Y3xNstf7XpzpB8PHCNQ5CSYf62XX1cIzwTI1w?purpose=fullsize)


A NAT Gateway enables resources in **private subnets** to access the internet for software updates or package downloads while preventing unsolicited inbound connections.

**Example**

* Install software updates
* Download packages
* Access AWS services

---

## 6. Route Tables

![Image](https://images.openai.com/static-rsc-4/zczD20ish5OAlkaSYkVgZnpbEXjKXd63MS3VpcjYRpj1iZphiDIJ-3dGJAxRx32TwiDNC4pLyDTrw00dwYA_YqwryLXuvRlpVYChAJiG3_35ebL4N731_cgzhRvYcZOhoqkxo2hyBUcbDeaxY2WUzf5L_NO_3S1ZbkL_9Q9tZzGm5b7cg32tvpn3XZbwfvzG?purpose=fullsize)



Route Tables define how traffic travels within the VPC.

Example:

| Destination | Target           |
| ----------- | ---------------- |
| 10.0.0.0/16 | Local            |
| 0.0.0.0/0   | Internet Gateway |

---

## 7. Security Groups

![Image](https://images.openai.com/static-rsc-4/6zC3ZOqlZd1MefwgaO1sU2R0dDX0FsDmxv8z-bx8j6ffngW-bgyCIVnn2Lv7yJWXCkCHPCzVaU-3ye2O5kv8oJ42z3uF0d1cbt0XkxgfRnQOZIeQybyc10IIQAkRq4OnWqxloXEbUrsjn8A72vsouGMGNmRrbKghkOsuyAlap7ZUY47wOxti3IS6z94O4W3u?purpose=fullsize)



Security Groups act as **virtual firewalls** at the instance level.

Features:

* Stateful
* Instance-level security
* Allow rules only
* Controls inbound and outbound traffic

Example:

| Protocol | Port |
| -------- | ---- |
| SSH      | 22   |
| HTTP     | 80   |
| HTTPS    | 443  |

---

## 8. Network ACL (NACL)

![Image](https://images.openai.com/static-rsc-4/2UymMHnq5SPevqfTdzAVTp4zTHu2Pwbf2TKSBWurP-9cItDRw8n7FiKBDSDGNbE9_7kxbPcp8H4ap1ruXJDHKIzlu6HwYflAZrTsbzbbpe_kYXQEW02Hw6eDWZeb8XMtwmsCEF5GqC-sVoUVLCgC8kAumvf97Lz_5vCzLMZXA-MwNMVQD9AKls-8ZdZLaCRX?purpose=fullsize)


Network ACLs provide **subnet-level security**.

Features:

* Stateless
* Allow and Deny rules
* Additional security layer

---

## 9. Elastic IP Address

![Image](https://images.openai.com/static-rsc-4/fm2LGhvlvkupP71V-AFQljyaqEKYGzzD2JoJlLjG-Wy0qrKHb8tdj3FcKLF5nGslzlspZZh_pVXPCZkuF6H5LmgEazOYB5Rymxb1885aAoHVPUwvUCOzNAHfmqvlGpptVfsmOU3Vx2NQXJy3hcgGkcVqls6TMgQvF7rzvcY-Q3H41sT_qJXLfTxkS4fNXmij?purpose=fullsize)


Elastic IP is a **static public IPv4 address** that can be associated with an EC2 instance.

Advantages:

* Static public IP
* Easy reassignment
* High availability

---

## 10. VPC Peering

![Image](https://images.openai.com/static-rsc-4/lJlBllmgG2LlH5dS5vKA91ba3DByZ59QM9am47r-QwnSZuWtg20EJhjGfuPaynGmtAJnpTCnwnINKNW8t7yQaAv6dQ1thf8P6eQUPcbPv-b0ROSa0GKB9wdnwzAnklezHwREowWqZ7BmxVfR1D16yD1tuSjNj75Xl1YqtFOAu1lcIC_SA-ml28Us35Z3SJfz?purpose=fullsize)



VPC Peering allows two VPCs to communicate privately using AWS's internal network.

Use Cases:

* Multi-account environments
* Development and Production connectivity
* Cross-region communication

---

## 11. VPN Connectivity

![Image](https://images.openai.com/static-rsc-4/tULTlVjO3-CHFiaJxn_0IPpqPgDYdQR0Qi4nMDH5lOMeFAJVVvMcPtB8MznbanB-ByDx3pecID_hKlyWkkk6uh0ZPimyLc0SCgqjRsZ1yjMJPYQfyYhNGdUk012BMRI3TpSP_bPloRLtDhpSvv7FtDPrvjoGMND5pXF31mzviDTkdBH4xk8WgeQR4YSNWvjS?purpose=fullsize)



Amazon VPC supports secure communication between your on-premises network and AWS using **Site-to-Site VPN**.

Benefits:

* Encrypted communication
* Hybrid cloud architecture
* Secure remote access

---

## 12. VPC Endpoints

![Image](https://images.openai.com/static-rsc-4/0RyehO1zixF6f3yNZruNJaQXp12uDqPEJS9dTDtePggRtPom12mVUpBIONo8rooW9OkBBV82cxDgxTUK4-5Wl9FM0y7rRsv1mWEguv2yArrWN9Gb_rJLrmbdNahcz6OC7jC2rBHxXS1XZ9dXqvwlnDcW2iddDz8Boq6sBG5EB9xJmka3nAfepfkMYQSbd5DW?purpose=fullsize)


VPC Endpoints allow private communication with supported AWS services without using the public internet.

Supported Services:

* Amazon S3
* Amazon DynamoDB
* Amazon SNS
* Amazon SQS

---

## 13. High Availability

Amazon VPC spans multiple **Availability Zones (AZs)**, allowing applications to remain available even if one AZ experiences a failure.

Benefits:

* Fault tolerance
* Disaster recovery
* Improved uptime

---

## 14. Scalability

You can easily expand your VPC by:

* Adding new subnets
* Launching more EC2 instances
* Connecting additional AWS services
* Integrating with Auto Scaling and Load Balancers

---

## 15. Monitoring and Logging

Amazon VPC integrates with:

* Amazon CloudWatch
* VPC Flow Logs
* AWS CloudTrail

These services help monitor network traffic, troubleshoot connectivity issues, and improve security.

---

# Summary

Amazon VPC offers a secure, scalable, and customizable networking environment for AWS resources. Features such as logical isolation, customizable IP addressing, public and private subnets, internet connectivity, security controls, VPN support, and seamless integration with AWS services make VPC the foundation of cloud networking in AWS. It enables organizations to design highly available and secure infrastructures tailored to their application requirements.



