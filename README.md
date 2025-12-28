# aws-3tier-highly-available-architecture
Highly Available 3-Tier Web Application Architecture on AWS

**Project Overview :**
This project demonstrates the design and implementation of a highly available, scalable, and secure 3-tier web application architecture on Amazon Web Services (AWS).
The objective of this project is to understand how real-world production applications are architected on AWS by following industry best practices related to networking, security, scalability, and fault tolerance.

**The architecture is logically divided into three layers:** 
1. Presentation Layer
2. Application Layer
3. Database Layer

**Architecture Overview:**

![AWS 3-Tier Architecture Diagram](Project_overview.png)


  **Traffic Flow:**
1. User sends request to the application URL  
2. Request reaches the **Application Load Balancer (ALB)**  
3. ALB distributes traffic to **EC2 instances** in an **Auto Scaling Group**  
4. EC2 instances process requests and communicate with **Amazon RDS (Multi-AZ)**  
5. Static content is served from **Amazon S3** via **CloudFront**




**AWS Services Used :**

- Amazon VPC
- Public and Private Subnets
- Internet Gateway
- NAT Gateway
- Route Tables
- Security Groups
- Application Load Balancer (ALB)
- Auto Scaling Group (ASG)
- Amazon EC2
- Amazon RDS (Multi-AZ)
- Amazon S3
- IAM Roles
- Amazon CloudWatch
- Amazon CloudFront


**Step-by-Step Implementation :**

****Step 1:** Create a Custom VPC**
- Created a dedicated VPC with a private IP range (CIDR block).
- Enabled DNS resolution and DNS hostnames.
 
**Purpose:**
Provides network isolation and full control over traffic flow.

****Step 2:** Create Public and Private Subnets**
- Public subnets for the Load Balancer.
- Private subnets for EC2 instances and the database.
- Subnets distributed across multiple Availability Zones.
 
**Purpose:**
Improves fault tolerance and availability.

**Step 3: Configure Internet Gateway and NAT Gateway**
- Internet Gateway attached to the VPC for public access.
- NAT Gateway configured to allow private instances outbound internet access.

**Purpose:**
Keeps backend resources private while allowing required updates.

**Step 4: Configure Route Tables**

- Public route table routes traffic to the Internet Gateway.
- Private route table routes outbound traffic via NAT Gateway.

**Step 5: Configure Security Groups**

- Load Balancer Security Group: allows HTTP/HTTPS from the internet.
- Application Security Group: allows traffic only from the Load Balancer.
- Database Security Group: allows traffic only from application instances.

**Security Principle:**
Least privilege access.

**Step 6: Launch EC2 Instances**

- EC2 instances launched in private subnets.
- IAM roles attached instead of access keys.
- Application dependencies installed on instances.

**Step 7: Configure Application Load Balancer**

- Application Load Balancer created in public subnets.
- Target group configured with EC2 instances.
- Health checks enabled.

**Purpose:**
Distributes traffic and ensures only healthy instances receive requests.

**Step 8: Configure Auto Scaling Group**

- Auto Scaling Group created for EC2 instances.
- Defined minimum, desired, and maximum capacity.
- Enabled automatic instance replacement.

**Purpose:**
Provides scalability and self-healing.

**Step 9: Setup Amazon RDS (Multi-AZ)**

- RDS instance deployed in private subnets.
- Multi-AZ enabled for high availability.
- Database access restricted using Security Groups.

**Step 10: Configure Amazon S3 and CloudFront**

- Static content stored in Amazon S3.
- CloudFront used as a Content Delivery Network (CDN).
- Improved global performance and reduced latency.

 **Step 11: Enable Monitoring with CloudWatch**

- Enabled monitoring for EC2, ALB, and RDS.
- Tracked metrics such as CPU utilization and health checks.

**Security Best Practices Implemented:**

- IAM roles instead of hard-coded credentials
- Private subnets for application and database layers
- Least-privilege security groups
- No public access to database layer

**Key Learnings:**

- Designing real-world AWS architectures
- High availability and fault tolerance concepts
- Secure networking using VPC
- Load balancing and auto scaling
- Monitoring and observability


**Notes:**

* This project was implemented as a hands-on learning exercise.
* No sensitive information, access keys, or credentials are stored in this repository.
