---
title: "Week 3 - AWS Compute Services"
weight: 3
chapter: false
pre: "<b> 1.3. </b>"
---

**Week:** 2025-09-22 to 2025-09-26  
**Status:** "Done"  

---

## Week 3 Overview

This week highlighted AWS compute services, especially Amazon EC2 and supporting capabilities for scaling, storage, and pricing.

### Key Topics

- Amazon EC2 and instance families
- AMIs and backup strategies
- EBS volumes vs. Instance Store
- EC2 Auto Scaling patterns
- EC2 pricing models
- Amazon Lightsail, EFS, and FSx

### Hands-on Labs

- Lab 01: AWS Account & IAM Setup
- Lab 07: AWS Budgets & Cost Management
- Lab 09: AWS Support Plans

**Day 11**-Amazon EC2 (Elastic Compute Cloud) provides scalable computing in the cloud – essentially Virtual Machines.

AWS classifies instances into several groups to suit different workload needs. Main types:
1. T (Burstable): E.g., T3, T4g. Best for applications with low CPU usage but occasional spikes (e.g., dev/test servers, low-traffic websites).
2. M (General Purpose): E.g., M5, M6i. Balances CPU, Memory (RAM), and Network Resources. Suitable for most general-purpose applications.
3. C (Compute Optimized): E.g., C5, C6i. Optimized for applications that require high CPU performance, such as high-performance computing (HPC), gaming servers, and video processing.
4. R (Memory Optimized): Eg: R5, R6i. Optimized for applications that require large RAM, such as high-performance databases, in-memory Big Data analytics.

5. I (Storage Optimized): Eg: I3, I4i. Optimized for tasks that require high-speed I/O and large local storage (e.g., NoSQL databases).

**Day 12**-AMI and Backup Strategy

1. AMI (Amazon Machine Image): Is a virtualization template (template) that contains the software configuration needed to launch an EC2 Instance. AMI includes the operating system, application server, and your application. AMI allows you to launch multiple identical Instances quickly.

2. Backup Strategy: Use EBS Snapshots (see below) to create point-in-time backups of EBS volumes. This strategy should be automated (e.g., using AWS Backup or Amazon Data Lifecycle Manager) and stored off-site to ensure data is always recoverable.

**Day 13** - EC2 Auto Scaling (ASG) is a service that automatically adjusts the number of EC2 instances to meet traffic demands.

1. Function: Automatically launch additional instances when demand increases (Scale Out) and terminate instances when demand decreases (Scale In).
2. Benefits: Ensure consistent application performance and optimize costs by paying only for the resources you actually need.
3. Configuration: Define Minimum, Desired, and Maximum number of instances.

**Day 14**-EC2 Pricing Model Selection

1. On-Demand Pay per hour/second, no upfront commitment. Short-term, infrequent, unpredictable workloads.

2. Savings Plans Commit to a fixed spend (e.g., $10/hour) for 1 or 3 years to get a deep discount compared to On-Demand. Stable, persistent workloads.

3. Reserved Instances (RI) Commit to a specific Instance type for 1 or 3 years. Stable, persistent workloads (gradually replaced by Savings Plans).

4. Spot Instances Bid on AWS's excess compute capacity, which can offer discounts of up to 90%. AWS can reclaim Instances at any time. Non-critical, fault-tolerant workloads (e.g., batch processing, compute).

**Day 15**-Other Compute and Storage Services
1. Amazon Lightsail: Simple, fixed-price monthly provisioning of virtual servers (VPS), databases, and networking. Ideal for new users or small, simple projects.
2. Amazon EFS (Elastic File System): Scalable, on-demand file storage service (Elastic), accessed concurrently by multiple EC2 Instances across multiple AZs. (Using NFS protocol).
3. Amazon FSx: Provides fully managed third-party file systems on AWS.