---
title: "Week 6 - AWS Database Services"
weight: 6
chapter: false
pre: "<b> 1.6. </b>"
---

**Week:** 2025-10-13 to 2025-10-17  
**Status:** "Done"  

---

## Week 6 Overview

This week focused on the AWS database landscape, covering managed relational engines, purpose-built NoSQL stores, in-memory caching, and analytics data warehouses.

### Key Topics

- Database Fundamentals (RDBMS, NoSQL, OLTP vs OLAP)
- Amazon RDS & Aurora
- Amazon Redshift
- Amazon ElastiCache
- AWS Database Migration Service (DMS)

### Hands-on Labs

- Lab 05: Amazon RDS & EC2 Integration
- Lab 43: AWS Database Migration Service (DMS)

**Day 26**-Basic Concepts of Databases

1. RDBMS (Relational Database Management System) Relational database (e.g. MySQL, PostgreSQL). Data is organized into tables, with constraints and transactions (ACID).
2. NoSQL (Not Only SQL) Non-relational database (e.g. DynamoDB, MongoDB). Data is flexible, no need for a rigid schema.
3. OLTP (Online Transaction Processing) Online transaction processing. Focus on small, fast transactions (INSERT, UPDATE, DELETE).
4. OLAP (Online Analytical Processing) Online analytical processing. Focus on complex queries, synthesizing large amounts of data.

**Day 27**-Amazon Redshift
1. Nature: Cloud-based Data Warehouse service, optimized for OLAP (analytics).
2. Function: Enables complex queries and data analysis on a Petabyte scale, using Columnar Storage architecture and Massively Parallel Processing (MPP) to speed up queries.

**Day 28**- Amazon ElastiCache
1. Nature: Fully managed In-Memory Caching service.
2. Function: Helps speed up applications by offloading the database and storing frequent queries or session data in RAM.
3. Supported Engines:Redis: Supports rich, durable data structures, replication and queuing. Memcached: Simple, high-speed, often used for object caching.

**Day 29**-Amazon RDS & Aurora

Amazon RDS (Relational Database Service) is a service that manages traditional relational databases on AWS. It handles patching, backups, fault management, and scaling.

1. Supported Engines: PostgreSQL, MySQL, MariaDB, Oracle, SQL Server.
2. Amazon Aurora: Is an AWS-exclusive relational DB engine, compatible with MySQL and PostgreSQL. Aurora provides higher performance (5x MySQL, 3x PostgreSQL) and higher availability at a lower cost than commercial DBs.

**Day 30**-AWS Database Migration Service (DMS)
1. Function: A tool that allows you to migrate databases (both relational and NoSQL) from On-premises to AWS, between AWS services, or between different engine types (e.g., from Oracle to Aurora PostgreSQL).
2. Key Features: Supports Continuous Replication (Zero Downtime Migration) to minimize downtime during conversion.