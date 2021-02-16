# [<Udemy Ultimate AWS Certified Solutions Architect Associate 2021>]([https://www.udemy.com/course/aws-certified-solutions-architect-associate-saa-c02/](https://www.udemy.com/course/aws-certified-solutions-architect-associate-saa-c02/)) Summary

## Section 1: Introduction - AWS Certified Solutions Architect Associate

### 1. Course Learning Contest

### 2. Course Introduction - AWS Certified Solutions Architect Associate

### 3. PLEASE READ: Lectures you can skip if you took a course from me before

### 4. Creating and AWS Account

### 5. AWS Account Activation Troubleshooting

### 6. AWS Budget Setup

### 7. Important Message

### 8. About your instructor

### 9. How to read an AWS Bill

## Section 2: Code & Slides Download

### 10. Slides and Code Download

## Section 3: AWS Fundamentals: IAM & EC2

### 11. AWS Fundamentals - Section Introduction

### 12. AWS Regions and AZs

- AWS Availability Zones
    - Each Region has many availability zones (usually 3, min is 2, max is 6). Example:
        - ap-southeast-2a
        - ap-southeast-2b
        - ap-southeast-2c
    - Each availability zone (AZ) is one or more discrete data centers with redundant power, networking, and connectivity
    - They're separate from each other, so that they're isolated from disasters
    - They're connected with high bandwidth, ultra-low latency networking

### 13. IAM Introduction

- IAM Introduction
    - IAM (Identity and Access Management)
    - Your whole AWS security is there:
        - Users
        - Groups
        - Roles
    - Root account should never be used (and shared)
    - Users must be created with proper permissions
    - IAM is at the center of AWS
    - Policies are written in JSON (JavaScript Object Notation)
    - IAM has a global view
    - MFA (Multi Factor Authentication) can be setup
    - IAM has predefined "managed policies"
    - It's best to give users the minimal amount of permissions they need to perform their job (least privilege principles)
- IAM Federation
    - Big enterprises usually integrate their own repository of users with IAM
    - This way, one can login into AWS using their company credentials
    - Identity Federation uses the SAML standard (Active Directory)
- IAM 101 Brain Dump
    - One IAM User per PHYSICAL PERSON
    - One IAM Role per Application
    - IAM credentials should NEVER BE SHARED
    - Never, ever, ever, ever, write IAM credentials in code. EVER
    - And even less, NEVER EVER EVER COMMIT YOUR IAM credentials
    - Never use the ROOT account except for initial setup
    - Never use ROOT IAM Credentials

### 14. IAM Hands On

### 15. About the EC2 Console Changes

### 16. EC2 Introduction

- What is EC2?
    - EC2 is one of most popular of AWS offering
    - It mainly consists in the capability of:
        - Renting virtual machines (EC2)
        - Storing data on virtual drives (EBS)
        - Distributing load across machines (ELB)
        - Scaling the services using an auto-scaling group (ASG)
    - Knowing EC2 is fundamental to understand how the Cloud works
- 

### 17. SSH Overview

### 18. How to SSH using Linux or Mac

- What is SSH?

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7ab86d2c-4701-48ac-b627-7e5034077f78/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7ab86d2c-4701-48ac-b627-7e5034077f78/Untitled.png)

### 19. How to SSH using Windows

### 20. How to SSH using Windows 10

### 21 SSH Troubleshooting

### 22. EC2 Instance connect

### 23. Introduction to Security Groups

- Introduction

### 24. Security Groups Deep Dive

- Deeper Dive

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5a5a204a-fd81-40f9-abd0-eb36ec3969d4/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5a5a204a-fd81-40f9-abd0-eb36ec3969d4/Untitled.png)

- Security Group is like a firewall outside your EC2 Instance

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0022c063-626f-4ec8-b420-1bf1e39a69f1/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0022c063-626f-4ec8-b420-1bf1e39a69f1/Untitled.png)

- Security Groups Good to know
    - Can be attached to multiple instances
    - Locked down to a region / VPC combination
    - Does live "outside" the EC2 - if traffic is blocked the EC2 instance won't see it
    - It's good to maintain one separate security group for SSH access
    - If your application is not accessible (time out), then it's a security group issue
    - If your application gives a "connection refused" error, then it's an application error or it's not launched
    - All inbound traffic is blocked by default
    - All outbound traffic is authorised by default
- Referencing other security groups Diagram

### 25. Private vs Public vs Elastic IP

- Private vs Public IP (IPv4)
    - Networking has two sorts of IPs. IPv4 and IPv6
        - IPv4: 1.160.10.240
        - IPv6: 3ffe: 1900:4545:3:200:f8ff:fe21:67cf
    - In this course, we will only be using IPv4
    - IPv4 is still the most common format used online
    - IPv6 is newer and solves problems for the Internet of Things (IoT)
    - IPv4 allows for 3.7 billion different addresses in the public space
    - IPv4: [0-255].[0-255].[0-255].[0-255]
- Private vs Public IP (IPv4) Examples
- Fundamental Differences
    - Public IP:
        - Public IP means the machine can be identified on the internet (WWW)
        - Must be unique across the whole web (not two machines can have the same public IP)
        - Can be geo-located easily
    - Private IP:
        - Private IP means the machine can only be identified on a private network only
        - The IP must be unique across the private network
        - BUT two different private networks (two companies) can have the same IPs
        - Machines connect to WWW using an internet gateway (a proxy)
        - Only a specified range of IPs can be used as private IP
- Elastic IPs
    - When you stop and then start an EC2 instance, it can change its public IP
    - If you need to have a fixed public IP for your instance, you need and Elastic IP
    - An Elastic IP is a public IPv4 IP you own as long as you don't delete it
    - You can attach it too one instance at a time
    - With an Elastic IP address, you can mask the failure of an instance of or software by rapidly remapping the address to another instance in your account
    - You can only have 5 Elastic IP in your account (you can ask AWS to increase that)
    - Overall, try to avoid using Elastic IP
        - They often reflect poor architectural decisions
        - Instead, use a random public IP and register a DNS name to it
        - Or as we'll see later, use a Load Balancer and don't use a public IP
- In AWS EC2 - Hands On
    - By default, your EC2 machine comes with:
        - A private IP for the internal AWS Network
        - A public IP, for the WWW
    - When we are doing SSH into our EC2 machines
        - We can't use a private IP, because we are not in the same network
        - We can only use the public IP
    - If your machine is stopped and then started
        - **the public IP can change**

### 26. Private vs Public vs Elastic IP Hands On

### 27. Install Apache on EC2

### 28. EC2 User Data

- EC2 User Data
    - It is possible to bootstrap our instances using an **EC2 User data** script
    - **bootstrapping** means launching commands when a machine starts
    - That script is **only run once** at the instance **first start**
    - EC2 user data is used to automate boot tasks such as:
        - Installing updates
        - Installing software
        - Downloading common files from the internet
        - Anything you can think of
    - The EC2 User Data Script runs with the root user
- EC2 User Data Hands On
    - We want to make sure that this EC2 instance has an Apache HTTP server installed on it - to display a simple web page
    - For it, we are going to write a user-data script
    - This script will be executed at the first boot of the instance

### Quiz 1: IAM & EC2 Mid Way Quiz

### 29. EC2 Instances Launch Types

- Types
    - On Demand Instances: short workload, predictable pricing
    - Reserved: (MINIMUM 1 year)
        - Reserved Instances: long workloads
        - Convertible Reserved Instances: long workloads with flexible instances
        - Scheduled Reserved Instances: example - every Thursday between 3 and 6 pm
    - Spot Instances: short workloads, for cheap, can lose instances (less reliable)
    - Dedicated Instances: no other customers will share your hardware
    - Dedicated Hosts: book an entire physical server, control instance placement
- EC2 On Demand
    - Pay for what you use (billing per second, after the first minute)
    - Has the highest cost but no upfront payment
    - No long term commitment
    - Recommended for short-term and un-interrupted workloads, where you can't predict how the application will behave
- EC2 Reserved Instances
    - Up to 75% discount compared to On-demand
    - Pay upfront for what you use with long term commitment
    - Reservation period can be 1 or 3 years
    - Reserve a specific instance type
    - Recommended for steady state usage applications (think database)
    - Convertible Reserved Instance
        - can change the EC2 instance type
        - Up to 54% discount
    - Scheduled Reserved Instances
        - launch within time window you reserve
        - When you require a fraction of day / week / month
- EC2 Spot Instances
    - Can get a discount of up to 90% compared to On-demand
    - Instances that you can "lose" at any point of time if your max price is less than the current spot price
    - The MOST cost-efficient instances in AWS
    - Useful for workloads that are resilient to failure
        - Batch jobs
        - Data analysis
        - Image processing
        - ...
    - Not great for critical jobs or databases
    - Great combo: Reserved Instances for baseline + On-Demand & Spot for peaks
- EC2 Dedicated Hosts
    - Physical dedicated EC2 server for your use
    - Full control of EC2 instance placement
    - Visibility into the underlying sockets / physical cores or the hardware
    - Allocated for your account for a 3 year period reservation
    - More expensive
    - Useful for software that have complicated licensing model (BYOL - Bring Your Own License)
    - Or for companies that have strong regulatory or compliance needs
- EC2 Dedicated Instances
    - Instances running on hardware that's dedicated to you
    - May share hardware with other instances in the same account
    - No control over instance placement (can move hardware after Stop / Start)

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7c978055-7c04-4b78-839c-e90ee9a66b61/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7c978055-7c04-4b78-839c-e90ee9a66b61/Untitled.png)

### 30. Spot Instances & Spot Fleet

- EC2 Spot Instance Requests
    - Can get a discount of up to 90% compared to Ondemand
    - Define max spot price and get the instance while current spot price < max
        - The hourly spot price varies based on offer and capacity
        - If the current spot price > your max price you can choose to stop or terminate your instance with a 2 minute grace period
    - Other stratrgy: Spot Block
        - "Block" spot instance during a specified time frame (1 to 6 hours) without interruptions
        - In rare situations, the instance may be reclaimed
    - Used for batch jobs, data analysis, or workloads that are resilient to failures
    - Not great for critical jobs or databases
- How to terminate Spot Instances?

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6d11375f-b3ed-4d7f-a664-9634333857d8/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6d11375f-b3ed-4d7f-a664-9634333857d8/Untitled.png)

- Spot Fleets
    - Spot Fleets = set of Spot Instances + (optinal) On-Demand Instances
    - The Spot Fleet will try to meet the target capacity with price constraints
        - Define possible launch pools: instance type (m5.large), OS, Availability Zone
        - Can have multiple launch pools, so that the fleet can choose
        - Spot Fleet stops launching instances when reaching capacity or max cost
    - Strategies to allocate Spot Instance
        - lowestPrice: from the pool with the lowest price (cost optimization, short workload)
        - diversified: distributed across all pool (great for availability, long workloads)
        - capacityOptimized: pool with the optimal capacity for the number of instances
    - Spot Fleets allow us to automatically request Spot Instances with the lowest price

### 31. EC2 Instance Launch Types Hands On

### 32. EC2 Instance Types Deep Dive

### 33. EC2 AMIs

### 34. EC2 AMI Hands On

### 35. Cross Account AMI Copy

### 36. EC2 Placement Groups

### 37. Elastic Network Interfaces (ENI) with Hands On

### 38. ENI - Extra Reading

### 39. EC2 Hibernate

### 40. EC2 Hibernate - Hands On

### 41. EC2 for the Solution Architect

### Quiz 2: EC2 Final Quiz

## Section 4: High Availability and Scalability: ELB & ASG

### 42. High Availability and Scalability

### 43. Elastic Load Balancing (ELB) Overview

### 44. About the Gateway Load Balancer

### 45. Classic Load Balancer (CLB) with Hands On

### 46. Application Load Balancer (ALB) with Hands On

### 47. Network Load Balancer (NLB) with Hands On

### 48. Elastic Load Balancer - Stickiness

### 49. Elastic Load Balancer - Cross Zone Load Balancing

### 50. Elastic Load Balancer - SSL Certificates

### 51. Elastic Load Balancer - Connection Draining

### 52. Auto Scaling Groups (ASG) Overview

### 53. Auto Scaling Groups Hands On

### 54. Auto Scaling Groups - Scaling Policies

### 55. Auto Scaling Groups - for Solutions Architects

### Quiz 3: Fundamentals 2 Quiz

## Section 5: EC2 Storage - EBS & EFS

## Section 6: AWS Fundamentals: RDS + Aurora + ElastiCache

## Section 7: Route 53

## Section 8: Classic Solutions Architecture Discussions

## Section 9: Amazon S3 Introduction

## Section 10: AWS CLI, SDK, IAM Roles & Policies

## Section 11: Advanced Amazon S3 & Athena

## Section 12: CloudFront & AWS Global Accelerator

## Section 13: AWS Storage Extras

## Section 14: Decoupling applications: SQS, SNS, Kinesis, Active MQ

## Section 15: Serverless Overviews from a Solution Architect Perspective

## Section 16: Serverless Solution Architecture Discussions

## Section 17: Databases in AWS

## Section 18: AWS Monitoring & Audit: CloudWatch, CoulTrail & Config

## Section 19: Identity and Access Management (IAM) - Advanced

## Section 20: AWS Security & Encryption: KMS, SSM, Parameter Store, CloudHSM, Shield, WAF

## Section 21: Networking - VPC

## Section 22: Disaster Recovery & Migrations

## Section 23: More Solutions Architectures

## Section 24: Other Services

## Section 25: WhitePapers and Architectures - AWS Certified Solution Architect Associate

## Section 26: Preparing for the Exam + Practice Exam - AWS Certified Solutions Architect Assoc

## Section 27: Congratulations - AWS Certified Solutions Architect Associate