---
title: "Tuần 6 - AWS Database Services"
weight: 6
chapter: false
pre: "<b> 1.6. </b>"
---

**Tuần:** 2025-10-13 đến 2025-10-17  
**Trạng thái:** "Hoàn thành"  

---

## Tổng quan tuần 6

Tuần này tập trung vào hệ sinh thái cơ sở dữ liệu trên AWS: từ dịch vụ quan hệ managed, NoSQL chuyên dụng, bộ nhớ đệm in-memory cho tới data warehouse phân tích.

### Nội dung chính

- Database Fundamentals (RDBMS, NoSQL, OLTP vs OLAP)
- Amazon RDS & Aurora
- Amazon Redshift
- Amazon ElastiCache
- AWS Database Migration Service (DMS)

### Labs thực hành

- Lab 05: Amazon RDS & EC2 Integration
- Lab 43: AWS Database Migration Service (DMS)

**Ngày 26**-Các Khái niệm Cơ bản về Cơ sở Dữ liệu

1. RDBMS (Relational Database Management System)	Cơ sở dữ liệu quan hệ (ví dụ: MySQL, PostgreSQL). Dữ liệu được tổ chức thành các bảng, có ràng buộc và giao dịch (ACID).
2. NoSQL (Not Only SQL)	Cơ sở dữ liệu phi quan hệ (ví dụ: DynamoDB, MongoDB). Dữ liệu linh hoạt, không cần lược đồ cứng.
3. OLTP (Online Transaction Processing)	Xử lý giao dịch trực tuyến. Tập trung vào các giao dịch nhỏ, nhanh (INSERT, UPDATE, DELETE).
4. OLAP (Online Analytical Processing)	Xử lý phân tích trực tuyến. Tập trung vào các truy vấn phức tạp, tổng hợp lượng dữ liệu lớn.

**Ngày 27**-Amazon Redshift
1. Bản chất: Dịch vụ Kho dữ liệu (Data Warehouse) dựa trên đám mây, được tối ưu hóa cho OLAP (phân tích).
2. Chức năng: Cho phép thực hiện các truy vấn phức tạp và phân tích dữ liệu trên quy mô Petabyte, sử dụng kiến trúc Columnar Storage (lưu trữ cột) và xử lý song song (MPP - Massively Parallel Processing) để tăng tốc độ truy vấn.

**Ngày 28**- Amazon ElastiCache
1. Bản chất: Dịch vụ caching trong bộ nhớ (In-Memory Caching) được quản lý hoàn toàn.
2. Chức năng: Giúp tăng tốc độ ứng dụng bằng cách giảm tải cho cơ sở dữ liệu và lưu trữ các truy vấn thường xuyên hoặc dữ liệu phiên (session data) vào bộ nhớ RAM.
3. Các Engine hỗ trợ:Redis: Hỗ trợ cấu trúc dữ liệu phong phú, bền vững, sao chép và xếp hàng (queuing). Memcached: Đơn giản, tốc độ cao, thường dùng để lưu trữ đối tượng đơn giản (object caching).

**Ngày 29**-Amazon RDS & Aurora

Amazon RDS (Relational Database Service) là dịch vụ quản lý các cơ sở dữ liệu quan hệ truyền thống trên AWS. Nó xử lý việc vá lỗi, sao lưu, quản lý lỗi và mở rộng quy mô.

1. Các Engine hỗ trợ: PostgreSQL, MySQL, MariaDB, Oracle, SQL Server.
2. Amazon Aurora: Là một engine DB quan hệ độc quyền của AWS, tương thích với MySQL và PostgreSQL. Aurora cung cấp hiệu suất cao hơn (gấp 5 lần MySQL, 3 lần PostgreSQL) và độ sẵn sàng cao hơn với chi phí thấp hơn các DB thương mại.

**Ngày 30**-AWS Database Migration Service (DMS)
1. Chức năng: Một công cụ cho phép di chuyển cơ sở dữ liệu (cả quan hệ và NoSQL) từ On-premises sang AWS, giữa các dịch vụ AWS, hoặc giữa các loại engine khác nhau (ví dụ: từ Oracle sang Aurora PostgreSQL).
2. Tính năng chính: Hỗ trợ di chuyển liên tục (Continuous Replication) (Zero Downtime Migration) để giảm thiểu thời gian ngừng hoạt động trong quá trình chuyển đổi.