---
title : "Hạ tầng mạng"
date: 2026-09-07
weight : 4
chapter : false
pre : " <b> 4.4. </b> "
---

### Mục tiêu

Xây dựng hạ tầng mạng cơ bản, an toàn và tối ưu chi phí trên nền tảng AWS để triển khai ứng dụng Warehouse Inventory Management.

---

## 1. Tổng quan

Hạ tầng mạng là nền tảng cốt lõi giúp các tài nguyên trên AWS giao tiếp với nhau và kết nối ra Internet. Trong chương này, bạn sẽ khởi tạo một Amazon Virtual Private Cloud (VPC) cùng các thành phần mạng thiết yếu.

Kiến trúc mạng tinh gọn bao gồm:
- Amazon VPC: Môi trường mạng ảo cô lập logic dành riêng cho hệ thống.
- Public Subnets: Chứa Application Load Balancer (ALB) và các Task ECS Fargate.
- Internet Gateway (IGW): Cho phép các tài nguyên trong VPC kết nối ra Internet để người dùng truy cập và để ứng dụng giao tiếp với MongoDB Atlas.
- Route Table: Định tuyến lưu lượng mạng đi qua Internet Gateway (0.0.0.0/0 igw).
- Security Groups: Thiết lập tường lửa ảo kiểm soát lưu lượng truy cập an toàn cho ALB và ECS Task.

---

---

## 3. Nội dung thực hành

Thực hiện lần lượt các bước cấu hình:

- **4.4.1 Tạo VPC và các Public Subnet**
- **4.4.2 Cấu hình Internet Gateway và Route Table**
- **4.4.3 Thiết lập Security Group cho Application Load Balancer (ALB) và Amazon ECS**
---

## 4. Kết quả mong đợi

Sau khi hoàn thành chương này, bạn sẽ có:

- Một Virtual Private Cloud (VPC) được khởi tạo thành công với dải mạng CIDR quy định.
- Các Public Subnet được phân bổ đều trên các Availability Zone (AZs).
- Internet Gateway được liên kết trực tiếp với VPC và cấu hình Route Table chính xác.
- Bộ Security Group được cấu hình chuẩn: ALB mở cổng 80 cho công chúng, ECS Security Group chỉ nhận traffic chuyển tiếp từ ALB.
- Toàn bộ hạ tầng mạng sẵn sàng cho bước tạo Application Load Balancer và triển khai Container.
