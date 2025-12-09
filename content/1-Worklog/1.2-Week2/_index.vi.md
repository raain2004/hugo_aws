---
title: "Tuần 2 - Dịch vụ Mạng trên AWS"
weight: 2
chapter: false
pre: "<b> 1.2. </b>"
---

**Tuần:** 2025-09-15 đến 2025-09-19  
**Trạng thái:** "Hoàn thành"  

---

## Tổng quan tuần 2

Tuần này đào sâu các dịch vụ mạng của AWS, từ VPC cơ bản đến giải pháp kết nối nâng cao và cân bằng tải.

### Nội dung chính

- Amazon VPC và Subnet.  
- Security Group và Network ACL.  
- Internet Gateway, NAT Gateway.  
- VPC Peering và AWS Transit Gateway.  
- Elastic Load Balancing (ALB, NLB, GWLB).

### Labs thực hành

- Lab 03: Amazon VPC & Networking Basics.  
- Lab 10: Hybrid DNS (Route 53 Resolver).  
- Lab 19: VPC Peering.  
- Lab 20: AWS Transit Gateway.

**Ngày 6**-Amazon VPC (Virtual Private Cloud): Ảo hóa một trung tâm dữ liệu logic cô lập trên nền tảng AWS. Bạn hoàn toàn kiểm soát môi trường mạng ảo này, bao gồm dải địa chỉ IP, cấu hình Subnet, bảng định tuyến và cổng mạng (gateways).

Subnet: Là một phân vùng của VPC. Subnet được liên kết với một Availability Zone (AZ) cụ thể.

1. Public Subnet: Chứa các tài nguyên cần truy cập Internet (ví dụ: máy chủ web), sử dụng Internet Gateway để kết nối.

2. Private Subnet: Chứa các tài nguyên nội bộ (ví dụ: cơ sở dữ liệu), không trực tiếp truy cập Internet.

**Ngày 7**

Security Group (SG): Hoạt động như một bộ lọc lưu lượng truy cập cấp Instance/Mạng giao diện.

Network ACL (NACL): Hoạt động như một lớp tường lửa cấp Subnet bảo vệ tất cả tài nguyên bên trong Subnet đó.

**Ngày 8**

Internet Gateway (IGW): Cho phép các tài nguyên trong Public Subnet kết nối với Internet (Cung cấp đường đi ra ngoài và nhận kết nối vào). Gắn vào VPC

NAT Gateway (Network Address Translation)	Cho phép các tài nguyên trong Private Subnet kết nối ra Internet (ví dụ: để tải bản vá), nhưng ngăn chặn kết nối đi vào từ Internet.	Đặt trong Public Subnet

**Ngày 9**

VPC Peering: Thiết lập kết nối mạng giữa hai VPC để chúng có thể giao tiếp với nhau bằng địa chỉ IP riêng. Lưu ý: Chỉ hoạt động theo kiểu One-to-One (1-1) và không chuyển tiếp (non-transitive) – nếu VPC A peering với B, và B peering với C, thì A và C không thể giao tiếp trực tiếp.

AWS Transit Gateway: Một bộ định tuyến mạng trung tâm. Cho phép kết nối nhiều VPC và mạng On-premises một cách dễ dàng và có khả năng chuyển tiếp (transitive). Lý tưởng cho các mạng có quy mô lớn và phức tạp.

**Ngày 10**-Elastic Load Balancing (ELB):Dịch vụ phân phối lưu lượng truy cập đến nhiều mục tiêu (như EC2 Instances) để tăng tính sẵn sàng, khả năng mở rộng và chịu lỗi cho ứng dụng.