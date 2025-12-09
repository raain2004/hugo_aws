---
title: "Week 2 - AWS Networking Services"
weight: 2
chapter: false
pre: "<b> 1.2. </b>"
---

**Week:** 2025-09-15 to 2025-09-19  
**Status:** "Done"  

---

## Week 2 Overview

This week focused on AWS networking services, spanning foundational VPC concepts through enterprise-grade connectivity patterns.

### Key Topics

- Amazon VPC and subnet design
- Security Groups and NACLs
- Internet Gateway and NAT Gateway
- VPC Peering and Transit Gateway
- Elastic Load Balancing (ALB, NLB, GWLB)

### Hands-on Labs

- Lab 03: Amazon VPC & Networking Basics
- Lab 10: Hybrid DNS (Route 53 Resolver)
- Lab 19: VPC Peering
- Lab 20: AWS Transit Gateway

**Day 6**-Amazon VPC (Virtual Private Cloud): Virtualizes an isolated logical data center on the AWS platform. You have complete control over this virtual network environment, including IP address ranges, Subnet configuration, routing tables, and gateways.

Subnet: A partition of the VPC. A subnet is associated with a specific Availability Zone (AZ).

1. Public Subnet: Contains resources that need to access the Internet (e.g., web servers), using an Internet Gateway to connect.

2. Private Subnet: Contains internal resources (e.g., databases), not directly accessing the Internet.

**Day 7**

Security Group (SG): Acts as an Instance/Network Interface level traffic filter.

Network ACL (NACL): Acts as a Subnet level firewall that protects all resources within that Subnet.

**Day 8**

Internet Gateway (IGW): Allows resources in the Public Subnet to connect to the Internet (Provides outbound and inbound connections). Attached to a VPC

NAT Gateway (Network Address Translation) Allows resources in the Private Subnet to connect to the Internet (e.g., to download patches), but prevents inbound connections from the Internet. Placed in a Public Subnet

**Day 9**

VPC Peering: Sets up a network connection between two VPCs so they can communicate with each other using private IP addresses. Note: Only works in a one-to-one (1-1) and non-transitive manner – if VPC A is peering with B, and B is peering with C, A and C cannot communicate directly.

AWS Transit Gateway: A central network router. Allows multiple VPCs and on-premises networks to be easily connected and transitive. Ideal for large and complex networks.

**Day 10**-Elastic Load Balancing (ELB): A service that distributes traffic to multiple targets (such as EC2 Instances) to increase application availability, scalability, and fault tolerance.