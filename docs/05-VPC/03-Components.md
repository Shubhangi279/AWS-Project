# Components of an Amazon VPC

Amazon VPC consists of several networking components that work together to provide a secure, scalable, and isolated cloud environment. Each component has a specific role in managing network connectivity, routing, and security.

---

# 1. VPC (Virtual Private Cloud)

A **Virtual Private Cloud (VPC)** is a logically isolated virtual network in AWS where you can launch cloud resources such as EC2 instances, RDS databases, and Load Balancers. It provides complete control over your network configuration, including IP addressing, subnets, routing, and security.

### Key Features

* Private virtual network
* Complete network control
* Secure environment
* Supports multiple Availability Zones

---

# 2. CIDR Block (Classless Inter-Domain Routing)

A **CIDR block** defines the IP address range of a VPC. Every VPC must have at least one IPv4 CIDR block.

### Example

```text
VPC CIDR : 10.0.0.0/16
```

This range provides **65,536 IP addresses**.

### Benefits

* Custom IP allocation
* Efficient address management
* Flexible subnet creation

---

# 3. Subnets

A **Subnet** is a subdivision of a VPC. It allows you to organize resources based on security and accessibility requirements.

## Public Subnet

A Public Subnet has a route to the Internet Gateway, allowing resources to communicate directly with the internet.

### Used for

* Web Servers
* Load Balancers
* Bastion Hosts

### Example

```text
10.0.1.0/24
```

---

## Private Subnet

A Private Subnet does not have direct internet access. It is mainly used for backend resources.

### Used for

* Databases
* Application Servers
* Internal Services

### Example

```text
10.0.2.0/24
```

---

# 4. Route Table

A **Route Table** contains a set of rules that determine where network traffic is directed.

### Example

| Destination | Target           |
| ----------- | ---------------- |
| 10.0.0.0/16 | Local            |
| 0.0.0.0/0   | Internet Gateway |

### Benefits

* Controls traffic flow
* Enables internet access
* Connects subnets

---

# 5. Internet Gateway (IGW)

An **Internet Gateway** is attached to a VPC to allow communication between resources in public subnets and the internet.

### Functions

* Enables inbound internet traffic
* Enables outbound internet traffic
* Supports public IPv4 addresses

### Used for

* Web Hosting
* Public APIs
* Internet-facing Applications

---

# 6. NAT Gateway

A **NAT (Network Address Translation) Gateway** enables resources in private subnets to access the internet without allowing inbound internet connections.

### Functions

* Software updates
* Package downloads
* Secure outbound communication

### Example

A database server in a private subnet downloads updates through the NAT Gateway but cannot be accessed directly from the internet.

---

# 7. Security Group

A **Security Group** acts as a virtual firewall for EC2 instances. It controls inbound and outbound traffic at the instance level.

### Characteristics

* Stateful
* Allow rules only
* Instance-level security

### Example Rules

| Protocol | Port | Source   |
| -------- | ---- | -------- |
| SSH      | 22   | Your IP  |
| HTTP     | 80   | Anywhere |
| HTTPS    | 443  | Anywhere |

---

# 8. Network ACL (NACL)

A **Network Access Control List (NACL)** provides an additional layer of security at the subnet level.

### Characteristics

* Stateless
* Supports Allow and Deny rules
* Applies to all resources within a subnet

---

# Difference Between Security Group and NACL

| Security Group                      | Network ACL                    |
| ----------------------------------- | ------------------------------ |
| Instance-level firewall             | Subnet-level firewall          |
| Stateful                            | Stateless                      |
| Supports Allow rules only           | Supports Allow and Deny rules  |
| Automatically allows return traffic | Requires explicit return rules |

---

# 9. Elastic IP (EIP)

An **Elastic IP** is a static public IPv4 address that can be associated with an EC2 instance.

### Benefits

* Static public IP
* Easy reassignment
* High availability

### Used for

* Production servers
* Web applications
* DNS mapping

---

# 10. VPC Peering

**VPC Peering** establishes a private connection between two VPCs, allowing them to communicate using private IP addresses.

### Benefits

* Secure communication
* Low latency
* No internet required

### Use Cases

* Development and Production environments
* Cross-account networking
* Cross-region communication

---

# 11. VPC Endpoint

A **VPC Endpoint** allows private communication between a VPC and supported AWS services without using the public internet.

### Supported Services

* Amazon S3
* Amazon DynamoDB
* Amazon SNS
* Amazon SQS

### Benefits

* Improved security
* Lower latency
* Reduced internet exposure

---

# 12. VPN Connection

A **Site-to-Site VPN** securely connects an on-premises data center to an AWS VPC using an encrypted IPsec tunnel.

### Benefits

* Secure communication
* Hybrid cloud connectivity
* Encrypted data transfer

---

# 13. Virtual Private Gateway (VGW)

A **Virtual Private Gateway** is attached to a VPC and serves as the AWS endpoint for VPN connections.

### Functions

* Terminates VPN tunnels
* Connects on-premises networks to AWS
* Supports hybrid cloud architectures

---

# 14. Customer Gateway (CGW)

A **Customer Gateway** represents your on-premises VPN device or router.

### Functions

* Connects to the Virtual Private Gateway
* Establishes secure VPN tunnels
* Enables hybrid networking

---

# 15. DHCP Options Set

A **DHCP Options Set** provides configuration information such as DNS servers, domain names, and NTP servers to instances in a VPC.

### Benefits

* Automatic network configuration
* Custom DNS settings
* Centralized management

---

# Components Overview Diagram

```text
                           Internet
                               │
                        Internet Gateway
                               │
         ┌─────────────────────┴──────────────────────┐
         │                 Amazon VPC                 │
         │               CIDR: 10.0.0.0/16            │
         │                                            │
         │  Public Subnet        Private Subnet       │
         │ ┌───────────────┐   ┌──────────────────┐   │
         │ │ EC2 Web Server│──▶│ App Server       │   │
         │ │ Load Balancer │   │ Amazon RDS       │   │
         │ └───────┬───────┘   └─────────┬────────┘   │
         │         │                     │            │
         │    NAT Gateway          Security Group     │
         │         │                     │            │
         │    Route Table         Network ACL         │
         └────────────────────────────────────────────┘
```

---

# Summary

The components of an Amazon VPC work together to create a secure, scalable, and highly available cloud network. Key components such as **CIDR blocks, subnets, route tables, Internet Gateways, NAT Gateways, Security Groups, Network ACLs, Elastic IPs, VPC Peering, VPC Endpoints, VPN connections, and gateways** enable organizations to design reliable networking architectures while maintaining security and performance.

This level of detail is ideal for a **GitHub portfolio**, **CDAC assignments**, and **AWS interview preparation**.

