---
title: "Tuần 3 - Dịch vụ Compute trên AWS"
weight: 3
chapter: false
pre: "<b> 1.3. </b>"
---

**Tuần:** 2025-09-22 đến 2025-09-26  
**Trạng thái:** "Hoàn thành"  

---

## Tổng quan tuần 3

Tuần này tập trung vào các dịch vụ Compute của AWS, đặc biệt là Amazon EC2 và những dịch vụ bổ trợ.

### Nội dung chính

- Amazon EC2 và các loại instance.  
- AMI và chiến lược sao lưu.  
- EBS và Instance Store.  
- EC2 Auto Scaling.  
- Lựa chọn mô hình giá cho EC2.  
- Amazon Lightsail, EFS, FSx.

### Labs thực hành

- Lab 01: AWS Account & IAM Setup.  
- Lab 07: AWS Budgets & Cost Management.  
- Lab 09: AWS Support Plans.


**Ngày 11**-Amazon EC2 (Elastic Compute Cloud) cung cấp khả năng tính toán có thể thay đổi kích thước trong đám mây – về cơ bản là máy chủ ảo (Virtual Machines).

AWS phân loại các Instance thành nhiều nhóm để phù hợp với các nhu cầu công việc khác nhau. Các loại chính:
1. T (Burstable): Ví dụ: T3, T4g. Tốt nhất cho các ứng dụng có mức sử dụng CPU thấp nhưng có lúc tăng đột biến (ví dụ: máy chủ dev/test, website lưu lượng thấp).
2. M (General Purpose): Ví dụ: M5, M6i. Cân bằng giữa CPU, Bộ nhớ (RAM) và Tài nguyên Mạng. Phù hợp cho hầu hết các ứng dụng phổ thông.
3. C (Compute Optimized): Ví dụ: C5, C6i. Tối ưu hóa cho các ứng dụng cần hiệu suất CPU cao, như tính toán hiệu năng cao (HPC), máy chủ game, và xử lý video.
4. R (Memory Optimized): Ví dụ: R5, R6i. Tối ưu hóa cho các ứng dụng cần bộ nhớ RAM lớn, như cơ sở dữ liệu hiệu năng cao, phân tích Big Data trong bộ nhớ.
5. I (Storage Optimized): Ví dụ: I3, I4i. Tối ưu hóa cho các tác vụ cần I/O tốc độ cao và dung lượng lưu trữ cục bộ lớn (ví dụ: cơ sở dữ liệu NoSQL).

**Ngày 12**-AMI và Chiến lược Sao lưu

1. AMI (Amazon Machine Image): Là một mẫu ảo hóa (template) chứa cấu hình phần mềm cần thiết để khởi chạy Instance EC2. AMI bao gồm hệ điều hành, máy chủ ứng dụng và ứng dụng của bạn. AMI cho phép bạn khởi chạy nhiều Instance giống hệt nhau một cách nhanh chóng.

2. Chiến lược Sao lưu (Backup Strategy): Sử dụng Snapshots EBS (xem bên dưới) để tạo bản sao lưu điểm-thời-gian (point-in-time) của các ổ đĩa EBS. Chiến lược này cần được tự động hóa (ví dụ: sử dụng AWS Backup hoặc Amazon Data Lifecycle Manager) và lưu trữ ngoại vi (Off-site storage) để đảm bảo dữ liệu luôn có thể phục hồi.

**Ngày 13**-EC2 Auto Scaling (ASG) là dịch vụ tự động điều chỉnh số lượng EC2 Instance để đáp ứng nhu cầu lưu lượng truy cập.

1. Chức năng: Tự động khởi chạy thêm Instance khi nhu cầu tăng (Scale Out) và chấm dứt Instance khi nhu cầu giảm (Scale In).
2. Lợi ích: Đảm bảo hiệu suất ứng dụng ổn định và tối ưu chi phí bằng cách chỉ trả tiền cho tài nguyên bạn thực sự cần.
3. Cấu hình: Cần định nghĩa Minimum (tối thiểu), Desired (mong muốn) và Maximum (tối đa) số lượng Instance.

**Ngày 14**-Lựa chọn Mô hình Giá cho EC2

1. On-Demand	Trả tiền theo giờ/giây, không cần cam kết trước.	Tải công việc ngắn hạn, không thường xuyên, khó dự đoán.
2. Savings Plans	Cam kết sử dụng một mức chi tiêu cố định (ví dụ: $10/giờ) trong 1 hoặc 3 năm để được giảm giá sâu so với On-Demand.	Tải công việc ổn định, liên tục.
3. Reserved Instances (RI)	Cam kết sử dụng một loại Instance cụ thể trong 1 hoặc 3 năm.	Tải công việc ổn định, liên tục (thay thế dần bởi Savings Plans).
4. Spot Instances	Đấu giá vào khả năng tính toán dư thừa của AWS, có thể giảm giá đến 90%. AWS có thể thu hồi Instance bất cứ lúc nào.	Công việc không quan trọng, chịu lỗi tốt (ví dụ: xử lý hàng loạt, tính toán).


**Ngày 15**-Các Dịch vụ Tính toán và Lưu trữ Khác
1. Amazon Lightsail: Dịch vụ cung cấp máy chủ ảo (VPS), cơ sở dữ liệu, và mạng đơn giản, giá cố định hàng tháng. Lý tưởng cho người dùng mới hoặc các dự án nhỏ, đơn giản.
2. Amazon EFS (Elastic File System): Dịch vụ lưu trữ tệp tin có thể mở rộng theo yêu cầu (Elastic), được truy cập đồng thời bởi nhiều EC2 Instance trên nhiều AZ. (Dùng giao thức NFS).
3. Amazon FSx: Cung cấp các hệ thống tệp tin của bên thứ ba được quản lý đầy đủ trên AWS.