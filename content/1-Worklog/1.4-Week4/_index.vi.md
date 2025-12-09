---
title: "Tuần 4 - Dịch vụ Lưu trữ trên AWS"
weight: 4
chapter: false
pre: "<b> 1.4. </b>"
---

**Tuần:** 2025-09-29 đến 2025-10-03  
**Trạng thái:** "Hoàn thành"  

---

## Tổng quan tuần 4

Tuần này tập trung vào các dịch vụ lưu trữ của AWS, từ S3 cho tới giải pháp hybrid và chiến lược DR.

### Nội dung chính

- Amazon S3 và các lớp lưu trữ.  
- S3 Static Website Hosting.  
- S3 Glacier cho lưu trữ dài hạn.  
- AWS Snow Family.  
- AWS Storage Gateway.  
- Chiến lược Disaster Recovery.  
- AWS Backup.

### Labs thực hành

- Lab 13: AWS Backup.  
- Lab 14: AWS VM Import/Export.  
- Lab 24: AWS Storage Gateway.  
- Lab 25: Amazon FSx.  
- Lab 57: Amazon S3 & CloudFront.


**Ngày 16**

Amazon S3 là dịch vụ lưu trữ đối tượng (Object Storage) cung cấp khả năng mở rộng không giới hạn, độ bền cao và tính sẵn sàng cao. Dữ liệu được lưu trữ dưới dạng đối tượng (Object) bên trong các Bucket (thùng chứa).

**Ngày 17**-S3 Static Website Hosting
1. Chức năng: S3 có thể được sử dụng để lưu trữ các website tĩnh (HTML, CSS, JavaScript, hình ảnh) mà không cần máy chủ web EC2.
2. Lợi ích: Cực kỳ đơn giản, chi phí thấp và có khả năng mở rộng theo yêu cầu lưu lượng truy cập toàn cầu một cách tự động.

**Ngày 18**-S3 Glacier là các lớp lưu trữ được thiết kế đặc biệt cho việc lưu trữ dữ liệu dài hạn (Archival), nơi chi phí thấp là ưu tiên hàng đầu và thời gian truy xuất có thể chấp nhận được là vài phút hoặc vài giờ.

**Ngày 19**-AWS Snow Family

Dịch vụ vật lý để di chuyển lượng dữ liệu lớn vào hoặc ra khỏi AWS, đặc biệt khi mạng Internet có băng thông thấp hoặc chi phí cao.
1. Snowcone: Thiết bị di động nhỏ nhất, dùng để thu thập, xử lý dữ liệu (Edge Compute) và chuyển dữ liệu.
2. Snowball Edge: Thiết bị cỡ vali, dùng để di chuyển hàng Petabyte dữ liệu và hỗ trợ Edge Computing (máy tính tại biên).
3. Snowmobile: Một chiếc xe tải vận chuyển dữ liệu siêu lớn (Exabyte-scale) cho việc di chuyển dữ liệu lớn nhất.

**Ngày 20**-AWS Storage Gateway

Dịch vụ Hybrid Cloud (Đám mây lai) cho phép kết nối cơ sở hạ tầng On-premises của bạn với lưu trữ đám mây AWS.
1. Hoạt động: Cài đặt một máy ảo (VM) tại chỗ, hoạt động như một cổng kết nối để lưu trữ dữ liệu một cách liền mạch lên S3 hoặc EBS.
2. Các loại Gateway chính: File Gateway (chia sẻ tệp tin qua SMB/NFS), Volume Gateway (lưu trữ khối ảo), và Tape Gateway (thay thế thư viện băng từ vật lý).