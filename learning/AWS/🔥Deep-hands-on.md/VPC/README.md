
<img width="2752" height="1536" alt="VPC" src="https://github.com/user-attachments/assets/f0dfcdc3-f5aa-4ddd-8175-313036aa5b92" />


# AWS VPC — MUST KNOW FOR YOUR PROJECT

For your **production-grade EKS project**, don't learn every VPC feature. These are the things you **must understand before building the networking**.

## 🔥 1. VPC Fundamentals ⭐⭐⭐⭐⭐

Understand:

```text
VPC
CIDR
Subnet
Route Table
Internet Gateway
NAT Gateway
Security Group
Network ACL
Availability Zone
```

Core mental model:

```text
AWS Region
   |
   +--- AZ-a
   |     |
   |   Subnets
   |
   +--- AZ-b
   |     |
   |   Subnets
   |
   +--- AZ-c
         |
       Subnets
```

---

# 2. CIDR + IP Addressing ⭐⭐⭐⭐⭐

You MUST understand CIDR properly.

Example:

```text
VPC
10.0.0.0/16
```

Then divide it:

```text
Public Subnets
10.0.1.0/24
10.0.2.0/24
10.0.3.0/24

Private Subnets
10.0.11.0/24
10.0.12.0/24
10.0.13.0/24

Database Subnets
10.0.21.0/24
10.0.22.0/24
10.0.23.0/24
```

Understand:

```text
/16
/20
/24
```

and:

```text
Network address
Usable IPs
Broadcast concept
Subnet sizing
```

For EKS, **IP planning matters a lot**.

---

# 3. Public vs Private Subnet ⭐⭐⭐⭐⭐

This is absolutely mandatory.

### Public subnet

Has a route:

```text
0.0.0.0/0
      ↓
Internet Gateway
```

### Private subnet

Typically:

```text
0.0.0.0/0
      ↓
NAT Gateway
```

Conceptually:

```text
Internet
   |
   v
Internet Gateway
   |
Public Subnet
   |
   +---- ALB
   |
   v
Private Subnet
   |
   +---- EKS Nodes
   +---- Applications
```

---

# 4. Internet Gateway ⭐⭐⭐⭐⭐

Understand:

```text
VPC
 ↓
Internet Gateway
 ↓
Internet
```

But remember:

> **Attaching an Internet Gateway does not automatically make a subnet public.**

The subnet's route table must point internet traffic to the IGW.

---

# 5. NAT Gateway ⭐⭐⭐⭐⭐

This is critical for private EKS nodes.

Understand:

```text
Private Subnet
      |
      v
NAT Gateway
      |
      v
Internet Gateway
      |
      v
Internet
```

Purpose:

> Private resources can make outbound internet connections without accepting unsolicited inbound internet traffic.

Example:

```text
EKS Node
 ↓
Pull package/image/update
 ↓
NAT Gateway
 ↓
Internet
```

### Production concept

For HA:

```text
AZ-a → NAT Gateway-a
AZ-b → NAT Gateway-b
AZ-c → NAT Gateway-c
```

Don't design your production network around a single NAT Gateway without understanding the availability/cost tradeoff.

---

# 6. Route Tables ⭐⭐⭐⭐⭐

You MUST understand routing.

Example public:

```text
Destination        Target

10.0.0.0/16        local
0.0.0.0/0          igw
```

Private:

```text
Destination        Target

10.0.0.0/16        local
0.0.0.0/0          nat
```

Database:

```text
Destination        Target

10.0.0.0/16        local
```

Understand:

```text
Subnet
   ↓
Route Table
   ↓
Where does traffic go?
```

---

# 7. Security Groups ⭐⭐⭐⭐⭐

Extremely important.

Understand:

```text
Security Group
=
Stateful firewall
```

Example:

```text
ALB SG
 ↓
EKS Node SG
 ↓
Application
```

Typical rule:

```text
Internet
 ↓
ALB :443
```

Then:

```text
ALB
 ↓
Node/Application port
```

And:

```text
Application
 ↓
RDS :5432
```

Production mindset:

> Don't allow `0.0.0.0/0` everywhere.

Prefer:

```text
ALB SG → App SG
App SG → DB SG
```

---

# 8. Stateful Security Groups ⭐⭐⭐⭐⭐

Know this difference:

```text
Security Group
= Stateful
```

If inbound traffic is allowed, the response traffic is automatically allowed.

This is different from NACLs.

---

# 9. Network ACL ⭐⭐⭐

You don't need to go extremely deep initially, but understand:

```text
NACL
=
Subnet-level firewall
```

Important difference:

```text
Security Group → ENI/resource level
NACL            → Subnet level
```

NACLs are **stateless**.

For your project, know how they work and when they matter; don't spend most of your revision time here.

---

# 10. Availability Zones ⭐⭐⭐⭐⭐

Your EKS project should be Multi-AZ.

Understand:

```text
Region: ap-south-1

AZ-a
AZ-b
AZ-c
```

Then:

```text
VPC
 |
 +--- AZ-a
 |     +--- Public
 |     +--- Private
 |     +--- Database
 |
 +--- AZ-b
 |     +--- Public
 |     +--- Private
 |     +--- Database
 |
 +--- AZ-c
       +--- Public
       +--- Private
       +--- Database
```

This gives you the foundation for HA.

---

# 11. VPC DNS ⭐⭐⭐⭐

Understand:

```text
enable_dns_support
enable_dns_hostnames
```

Why DNS matters:

```text
EKS
RDS
AWS services
Internal applications
Service discovery
```

Your VPC should have working DNS.

---

# 12. VPC Endpoints ⭐⭐⭐⭐⭐

Very important for production EKS.

Understand:

```text
Private subnet
      |
      v
VPC Endpoint
      |
      v
AWS Service
```

Examples:

```text
S3
ECR
STS
Secrets Manager
CloudWatch
SSM
```

Instead of:

```text
Private subnet
 ↓
NAT
 ↓
Internet
 ↓
AWS service
```

you can use appropriate VPC endpoints to keep AWS-service traffic private and reduce NAT dependency/cost.

For EKS, understand why endpoints can matter for:

```text
ECR image pulls
STS
Secrets Manager
S3
SSM
```

---

# 13. EKS Networking ⭐⭐⭐⭐⭐⭐⭐

This is the **most important VPC area for your project**.

Understand:

```text
VPC
 ↓
Subnets
 ↓
EKS
 ↓
VPC CNI
 ↓
Pod IPs
```

AWS VPC CNI means pods receive IP addresses from the VPC networking environment.

Therefore:

> **Your VPC CIDR and subnet sizing directly affect EKS pod capacity.**

This is why random CIDR planning is dangerous.

---

# 14. EKS Public vs Private Subnets ⭐⭐⭐⭐⭐

Your production architecture should understand:

```text
Internet
   ↓
ALB
   ↓
Private EKS workloads
```

Typical design:

```text
             Internet
                 |
                 v
          Public Subnets
                 |
                ALB
                 |
                 v
          Private Subnets
                 |
             EKS Nodes
                 |
                Pods
```

Database:

```text
Pods
 ↓
Private application subnets
 ↓
Database subnets
 ↓
Aurora PostgreSQL
```

---

# 15. Load Balancer Networking ⭐⭐⭐⭐⭐

Understand:

```text
Internet
 ↓
ALB
 ↓
Target
 ↓
EKS
```

Your public subnets are where internet-facing load balancers can live.

Your application workloads should generally remain private.

---

# 16. Database Subnets ⭐⭐⭐⭐⭐

For Aurora/RDS:

```text
Database Subnet Group
       |
       +--- AZ-a
       +--- AZ-b
       +--- AZ-c
```

Database should not be directly exposed to the internet.

Typical:

```text
Internet
   X
   |
   v
ALB
   |
   v
Application
   |
   v
Aurora
```

---

# 17. Security Group Architecture ⭐⭐⭐⭐⭐

For your project, understand this pattern:

```text
Internet
   |
   v
[ ALB SG ]
   |
   v
[ EKS/App SG ]
   |
   +--------> [ Redis SG ]
   |
   +--------> [ Aurora SG ]
```

Don't think:

```text
Everything
 ↓
0.0.0.0/0
```

Think:

```text
Who needs to talk to whom?
What port?
Why?
```

---

# 18. VPC Flow Logs ⭐⭐⭐⭐

Production troubleshooting:

```text
Traffic
 ↓
VPC Flow Logs
 ↓
Network investigation
```

Useful for understanding rejected/accepted network flows.

Especially useful when:

```text
Pod → RDS
Pod → Redis
ALB → Pod
```

isn't working.

---

# 19. Terraform VPC ⭐⭐⭐⭐⭐

Since your project uses Terraform, understand these concepts:

```text
aws_vpc
aws_subnet
aws_route_table
aws_route_table_association
aws_internet_gateway
aws_nat_gateway
aws_eip
aws_security_group
aws_network_acl
aws_vpc_endpoint
```

And especially understand the relationships:

```text
VPC
 ↓
Subnets
 ↓
Route Tables
 ↓
IGW / NAT
 ↓
Security Groups
 ↓
EKS
```

Don't just copy a VPC module.

You should know **why every resource exists**.

---

# 🚨 Your VPC Core

For your project, memorize this architecture:

```text
                         AWS REGION
                             |
                           VPC
                        10.0.0.0/16
                             |
          +------------------+------------------+
          |                  |                  |
         AZ-A               AZ-B               AZ-C
          |                  |                  |
     +----+----+        +----+----+        +----+----+
     |    |    |        |    |    |        |    |    |
   Public App  DB      Public App  DB      Public App  DB
     |    |    |        |    |    |        |    |    |
     |    |    |        |    |    |        |    |    |
    ALB  EKS Aurora    ALB  EKS Aurora    ALB  EKS Aurora
     |
    IGW

Private outbound:
EKS → NAT Gateway → IGW → Internet

Private AWS access:
EKS → VPC Endpoint → AWS Services
```

## 🔥 Absolute MUST-KNOW

If you only revise **10 VPC things** for this project:

1. **VPC + CIDR**
2. **Subnet + CIDR planning**
3. **Public vs Private subnet**
4. **Route Tables**
5. **Internet Gateway**
6. **NAT Gateway**
7. **Security Groups**
8. **Multi-AZ architecture**
9. **EKS VPC CNI / Pod networking**
10. **VPC Endpoints**

And for your actual project, the deepest areas should be:

**CIDR planning → Public/Private subnet design → Routing → SG architecture → NAT → EKS VPC CNI → Multi-AZ → VPC Endpoints.**
