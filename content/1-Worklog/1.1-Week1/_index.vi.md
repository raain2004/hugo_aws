---
title: "Tuần 1 - Kiến thức Nền tảng Cloud Computing"
weight: 1
chapter: false
pre: "<b> 1.1. </b>"
---

**Tuần:** 2025-09-08 đến 2025-09-12  
**Trạng thái:** "Hoàn thành"  

---

## Tổng quan tuần 1

Tuần này tập trung củng cố những khái niệm cơ bản về Cloud Computing, hạ tầng AWS và các công cụ quản trị.

### Nội dung chính

- Giới thiệu Cloud Computing và lợi ích.
- AWS Global Infrastructure (Region, AZ, Edge Location).  
- Bộ công cụ quản lý AWS (Console, CLI, SDK).  
- Chiến lược tối ưu chi phí.  
- AWS Well-Architected Framework.

### Labs thực hành

- Lab 01: Thiết lập tài khoản AWS & IAM.  
- Lab 07: AWS Budgets & Cost Management.  
- Lab 09: AWS Support Plans.

**Ngày 1**
-Giải thích rõ ràng về Cloud Computing (Điện toán Đám mây) là gì: cung cấp các tài nguyên công nghệ thông tin (như sức mạnh tính toán, lưu trữ, cơ sở dữ liệu) theo nhu cầu, thường qua internet, với mô hình trả tiền theo mức sử dụng.Lợi ích cốt lõi:

-Giảm chi phí (Cost Savings): Chuyển từ chi phí vốn (CAPEX) sang chi phí hoạt động (OPEX).

-Tốc độ và Linh hoạt (Agility): Triển khai tài nguyên chỉ trong vài phút thay vì vài tuần hoặc tháng.

-Mở rộng quy mô toàn cầu (Global Scale): Dễ dàng mở rộng ứng dụng trên phạm vi quốc tế.

**Ngày 2**- Tìm hiểu về cấu trúc vật lý khổng lồ giúp AWS cung cấp dịch vụ một cách tin cậy và hiệu suất cao trên toàn thế giới:

-Region (Vùng): Một khu vực địa lý vật lý riêng biệt, nơi AWS gom nhóm các Trung tâm Dữ liệu. Mỗi Region được cô lập hoàn toàn với các Region khác để đảm bảo khả năng chịu lỗi cao (Fault Tolerance).

-Availability Zone (AZ - Vùng sẵn sàng): Là một hoặc nhiều Trung tâm Dữ liệu rời rạc, có nguồn điện, mạng và kết nối riêng biệt. Mỗi Region có tối thiểu hai AZ. Các AZ trong cùng Region được kết nối bằng đường truyền độ trễ thấp, cho phép xây dựng các ứng dụng có độ sẵn sàng cao (High Availability).

-Edge Location (Vị trí Biên): Các trung tâm dữ liệu nhỏ hơn, được sử dụng chủ yếu bởi Amazon CloudFront (mạng phân phối nội dung - CDN) để lưu trữ nội dung (cache) gần người dùng cuối, giúp giảm độ trễ (latency).

**Ngày 3**-Giới thiệu các giao diện và công cụ chính để tương tác và quản lý tài nguyên trên AWS:

-AWS Management Console: Giao diện người dùng đồ họa (GUI) nền web, dễ sử dụng, lý tưởng cho người mới bắt đầu và các tác vụ quản lý thủ công.

-AWS Command Line Interface (CLI): Công cụ dòng lệnh mạnh mẽ, cho phép tự động hóa tác vụ và quản lý dịch vụ thông qua script.

-AWS Software Development Kits (SDKs): Các thư viện cho phép các nhà phát triển tích hợp dịch vụ AWS vào ứng dụng của họ bằng các ngôn ngữ lập trình phổ biến (ví dụ: Python, Java, Node.js).

**Ngày 4**-Hướng dẫn cách quản lý và tối ưu chi tiêu trên AWS để đảm bảo sử dụng tài nguyên hiệu quả nhất, bao gồm việc tận dụng các mô hình thanh toán khác nhau và công cụ quản lý chi phí.

**Ngày 5**-Giới thiệu bộ nguyên tắc chỉ đạo giúp các kiến trúc sư đám mây thiết kế và vận hành các hệ thống trên AWS an toàn, hiệu suất cao, đàn hồi, và hiệu quả về chi phí. Khung này được chia thành năm trụ cột chính:

1. Excellence Vận hành (Operational Excellence).

2. Bảo mật (Security).

3. Độ tin cậy (Reliability).

4. Hiệu suất (Performance Efficiency).

5. Tối ưu chi phí (Cost Optimization).

