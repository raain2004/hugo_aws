---
title: "Week 5 - AWS Security & Identity"
weight: 5
chapter: false
pre: "<b> 1.5. </b>"
---

**Week:** 2025-10-06 to 2025-10-10  
**Status:** "Done"  

---

## Week 5 Overview

This week concentrated on AWS security and identity management foundations.

### Key Topics

- Shared Responsibility Model
- AWS IAM (Users, Groups, Roles, Policies)
- Amazon Cognito
- AWS Organizations & SCPs
- AWS Identity Center (SSO)
- AWS KMS
- AWS Security Hub

### Hands-on Labs

- Lab 18: AWS Security Hub
- Lab 22: AWS Lambda Automation with Slack
- Lab 27: AWS Resource Groups & Tagging
- Lab 28: IAM Cross-Region Role & Policy
- Lab 30: IAM Restriction Policy
- Lab 33: AWS KMS & CloudTrail Integration
- Lab 44: IAM Advanced Role Control
- Lab 48: IAM Access Keys & Roles

**Day 21**-AWS IAM (Identity and Access Management)

A service that allows you to securely manage access to AWS services and resources.

1. Users: Represents a specific person or application. Each User can have individual credentials (Console and/or Access Keys).
2. Groups: A collection of Users. Assign permissions (Policies) to a Group to apply to all Users in it, making management easier.
3. Roles: A collection of access permissions that you can assign to AWS entities (such as EC2 Instances, Lambda Functions) or external users/federated logins (Federated Users). Roles are the preferred mechanism for providing secure, temporary permissions.
4. Policies: A document (in JSON format) that defines who (Principal) is allowed to perform what Action on what Resource (Resource) and under what Conditions (Condition).

**Day 22**-Amazon Cognito

A service that helps manage user identity and authentication for web and mobile applications.

1. User Pools: Provides user registration, login, and profile management for your applications. Supports multi-factor authentication (MFA).
2. Identity Pools: Allows application users to access AWS services (e.g., S3, DynamoDB) by exchanging Cognito credentials with temporary IAM Roles.

**Day 23**- AWS Organizations & SCPs

1. AWS Organizations: A centralized management service that allows you to aggregate and manage multiple AWS accounts under a single organization. Helps optimize billing, security, and compliance.

2. SCPs (Service Control Policies): Policies applied at the Organization (or Organizational Unit - OU) level to set maximum permission limits for all Users and Roles in the accounts under that OU. SCPs are a secure "filter" that cannot be bypassed.

**Day 24**- AWS Identity Center (SSO)

-AWS Identity Center (formerly AWS Single Sign-On - SSO): Single sign-on (SSO) access management service so users can centrally access all their AWS accounts and other cloud applications (e.g., Office 365, Salesforce) with just one set of credentials.

**Day 25**-AWS KMS (Key Management Service)

1. Function: Managed service to create and control encryption keys (Encryption Keys) used to encrypt data.

2. Highly Secure: KMS is designed so that no one, not even AWS, can extract the master KMS keys (CMKs - Customer Master Keys) in clear text. It integrates deeply with most AWS services (S3, EBS, RDS, etc.).