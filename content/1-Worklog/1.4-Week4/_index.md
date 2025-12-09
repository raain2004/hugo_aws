---
title: "Week 4 - AWS Storage Services"
weight: 4
chapter: false
pre: "<b> 1.4. </b>"
---

**Week:** 2025-09-29 to 2025-10-03  
**Status:** "Done"  

---

## Week 4 Overview

This week deep-dived into AWS storage services, ranging from S3 object storage to hybrid storage integrations.

### Key Topics

- Amazon S3 and storage classes
- S3 static website hosting
- S3 Glacier for archival workloads
- AWS Snow Family
- AWS Storage Gateway
- Disaster Recovery strategies
- AWS Backup

### Hands-on Labs

- Lab 13: AWS Backup
- Lab 14: AWS VM Import/Export
- Lab 24: AWS Storage Gateway
- Lab 25: Amazon FSx
- Lab 57: Amazon S3 & CloudFront

**Day 16**

Amazon S3 is an Object Storage service that provides unlimited scalability, high durability, and high availability. Data is stored as Objects inside Buckets.

**Day 17**-S3 Static Website Hosting
1. Function: S3 can be used to host static websites (HTML, CSS, JavaScript, images) without the need for EC2 web servers.

2. Benefits: Extremely simple, low cost, and the ability to automatically scale to global traffic demands.

**Day 18**-S3 Glacier are storage classes specifically designed for long-term data storage (Archival), where low cost is the top priority and acceptable retrieval times are minutes or hours.

**Day 19**-AWS Snow Family

A physical service for moving large amounts of data into or out of AWS, especially when the Internet is low bandwidth or high cost.

1. Snowcone: The smallest mobile device, used for data collection, processing (Edge Compute) and data transfer.

2. Snowball Edge: A suitcase-sized device, used to move Petabytes of data and support Edge Computing.

3. Snowmobile: An Exabyte-scale data truck for the largest data movements.

**Day 20**-AWS Storage Gateway

A Hybrid Cloud service that allows you to connect your On-premises infrastructure to AWS cloud storage.

1. Operational: Install a virtual machine (VM) on-premises, which acts as a gateway to seamlessly store data to S3 or EBS.

2. Main Gateway types: File Gateway (file sharing via SMB/NFS), Volume Gateway (virtual block storage), and Tape Gateway (replaces physical tape library).