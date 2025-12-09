---
title: "Week 1 - Cloud Computing Fundamentals"
weight: 1
chapter: false
pre: "<b> 1.1. </b>"
---

**Week:** 2025-09-08 to 2025-09-12  
**Status:** "Done"  

---

## Week 1 Overview

This week covered cloud computing fundamentals, AWS global infrastructure, and the core management tooling offered by AWS.

### Key Topics

- Introduction to Cloud Computing and its benefits
- AWS Global Infrastructure (Regions, AZs, Edge Locations)
- AWS Management Tools (Console, CLI, SDK)
- Cost Optimization approaches and Support Plans
- AWS Well-Architected Framework pillars

### Hands-on Labs

- Lab 01: AWS Account & IAM Setup
- Lab 07: AWS Budgets & Cost Management
- Lab 09: AWS Support Plans

**Day 1**
-Clearly explain what Cloud Computing is: providing IT resources (such as computing power, storage, databases) on demand, usually over the internet, on a pay-as-you-go model. Core benefits:

-Cost Savings: Shift from capital expenditure (CAPEX) to operating expenditure (OPEX).

-Speed ​​and Agility: Deploy resources in minutes instead of weeks or months.

-Global Scale: Easily scale applications internationally.

**Day 2**- Learn about the massive physical structure that enables AWS to deliver reliable and high-performance services worldwide:

-Region: A distinct physical geographic area where AWS groups its Data Centers. Each Region is completely isolated from other Regions to ensure high fault tolerance.

-Availability Zone (AZ): One or more discrete Data Centers, with separate power, network and connectivity. Each Region has at least two AZs. AZs in the same Region are connected by low latency lines, allowing for building applications with high availability.

-Edge Location: Smaller data centers, used primarily by Amazon CloudFront (content delivery network - CDN) to store content (cache) near end users, helping to reduce latency.

**Day 3**-Introduce the main interfaces and tools for interacting and managing resources on AWS:

-AWS Management Console: Web-based graphical user interface (GUI), easy to use, ideal for beginners and manual management tasks.

-AWS Command Line Interface (CLI): Powerful command-line tools that enable task automation and service management through scripting.

-AWS Software Development Kits (SDKs): Libraries that allow developers to integrate AWS services into their applications using popular programming languages ​​(e.g., Python, Java, Node.js).

**Day 4**-Guide to managing and optimizing AWS spend to ensure the most efficient use of resources, including leveraging different payment models and cost management tools.

**Day 5**-Introduce a set of guiding principles that help cloud architects design and operate secure, high-performance, resilient, and cost-effective systems on AWS. The framework is divided into five main pillars:

1. Operational Excellence.

2. Security.

3. Reliability.

4. Performance Efficiency.

5. Cost Optimization.