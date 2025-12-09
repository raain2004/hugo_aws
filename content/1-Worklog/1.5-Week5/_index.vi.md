---
title: "Tuần 5 - Bảo mật & Danh tính trên AWS"
weight: 5
chapter: false
pre: "<b> 1.5. </b>"
---

**Tuần:** 2025-10-06 đến 2025-10-10  
**Trạng thái:** "Hoàn thành"  

---

## Tổng quan tuần 5

Tuần này tập trung vào bảo mật và quản lý danh tính trên AWS.

### Nội dung chính

- Mô hình Trách nhiệm chia sẻ.  
- AWS IAM (Users, Groups, Roles, Policies).  
- Amazon Cognito.  
- AWS Organizations & SCPs.  
- AWS Identity Center (SSO).  
- AWS KMS.  
- AWS Security Hub.

### Labs thực hành

- Lab 18: AWS Security Hub.  
- Lab 22: AWS Lambda Automation with Slack.  
- Lab 27: AWS Resource Groups & Tagging.  
- Lab 28: IAM Cross-Region Role & Policy.  
- Lab 30: IAM Restriction Policy.  
- Lab 33: AWS KMS & CloudTrail Integration.  
- Lab 44: IAM Advanced Role Control.  
- Lab 48: IAM Access Keys & Roles.

**Ngày 21**-AWS IAM (Identity and Access Management)

Dịch vụ cho phép bạn quản lý quyền truy cập một cách an toàn vào các dịch vụ và tài nguyên AWS.

1. Users: Đại diện cho một người hoặc ứng dụng cụ thể. Mỗi User có thể có thông tin đăng nhập cá nhân (Console và/hoặc Khóa truy cập).
2. Groups: Tập hợp các Users. Gán quyền (Policies) cho Group để áp dụng cho tất cả Users trong đó, giúp quản lý dễ dàng hơn.
3. Roles: Một tập hợp các quyền truy cập mà bạn có thể gán cho các thực thể AWS (như EC2 Instance, Lambda Function) hoặc người dùng bên ngoài/đăng nhập liên kết (Federated Users). Roles là cơ chế ưa thích để cung cấp quyền tạm thời, an toàn.
4. Policies: Tài liệu (dưới dạng JSON) xác định Ai (Principal) được phép thực hiện Hành động gì (Action) trên Tài nguyên nào (Resource) và trong Điều kiện nào (Condition).

**Ngày 22**-Amazon Cognito

Dịch vụ giúp quản lý danh tính người dùng và xác thực cho các ứng dụng web và di động.

1. User Pools: Cung cấp chức năng đăng ký, đăng nhập và quản lý hồ sơ người dùng cho các ứng dụng của bạn. Hỗ trợ xác thực đa yếu tố (MFA).
2. Identity Pools: Cho phép người dùng ứng dụng truy cập vào các dịch vụ AWS (ví dụ: S3, DynamoDB) bằng cách trao đổi thông tin xác thực Cognito với IAM Role tạm thời.

**Ngày 23**- AWS Organizations & SCPs

1. AWS Organizations: Dịch vụ quản lý tập trung cho phép bạn tổng hợp và quản lý nhiều tài khoản AWS dưới một tổ chức thống nhất. Giúp tối ưu hóa thanh toán, bảo mật và tuân thủ.
2. SCPs (Service Control Policies): Các chính sách được áp dụng ở cấp độ Tổ chức (hoặc Đơn vị Tổ chức - OU) để đặt giới hạn quyền tối đa cho tất cả các Users và Roles trong các tài khoản thuộc OU đó. SCPs là một "bộ lọc" an toàn không thể bị vượt qua.

**Ngày 24**- AWS Identity Center (SSO)

-AWS Identity Center (trước đây là AWS Single Sign-On - SSO): Dịch vụ quản lý truy cập đăng nhập một lần (SSO) để người dùng có thể truy cập tập trung vào tất cả các tài khoản AWS của họ và các ứng dụng đám mây khác (ví dụ: Office 365, Salesforce) chỉ với một bộ thông tin đăng nhập.

**Ngày 25**-AWS KMS (Key Management Service)

1. Chức năng: Dịch vụ được quản lý để tạo và kiểm soát các khóa mã hóa (Encryption Keys) được sử dụng để mã hóa dữ liệu.
2. Bảo mật cao: KMS được thiết kế để không ai, kể cả AWS, có thể trích xuất các khóa KMS chính (CMKs - Customer Master Keys) ở dạng văn bản rõ ràng. Nó tích hợp sâu với hầu hết các dịch vụ AWS (S3, EBS, RDS, v.v.).