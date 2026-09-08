---
title : "Tổng quan Workshop"
date: 2026-09-07
weight : 1
chapter : false
pre : " <b> 4.1. </b> "
---

### Mục tiêu

Workshop này hướng dẫn triển khai ứng dụng Warehouse Inventory Management trên nền tảng AWS bằng cách sử dụng kiến trúc Cloud-Native, các dịch vụ được quản lý (Managed Services), triển khai container và lưu trữ đám mây. Sau khi hoàn thành workshop, bạn sẽ có thể triển khai một ứng dụng web quản lý kho hàng hoàn chỉnh với khả năng mở rộng, tính sẵn sàng cao và bảo mật.

---

## 1. Giới thiệu bài toán và giải pháp

**Warehouse Inventory Management** là một ứng dụng web cho phép người dùng quản lý danh mục hàng hóa, theo dõi tồn kho và cập nhật số lượng nhập/xuất kho theo thời gian thực. Hệ thống hỗ trợ các chức năng như thêm mới mặt hàng theo mã SKU, tải lên hình ảnh sản phẩm, cập nhật tăng giảm số lượng tồn kho và hiển thị danh sách kho hàng trực quan.

Thay vì triển khai ứng dụng trên một máy chủ truyền thống, workshop này áp dụng kiến trúc Cloud-Native trên AWS. Ứng dụng được đóng gói bằng **Docker** và triển khai trên **Amazon ECS Fargate**, hình ảnh sản phẩm được lưu trữ trên **Amazon S3**, trong khi dữ liệu được lưu trữ trên **MongoDB Atlas**.

Để tăng cường tính bảo mật và khả năng quản lý, các thông tin nhạy cảm (chuỗi kết nối Database) được lưu trong **AWS Secrets Manager**. Đồng thời, **Application Load Balancer**, được sử dụng để phân phối lưu lượng truy cập qua giao thức HTTP cổng 80.**Docker image** được lưu trữ và quản lý trực tiếp thông qua **Amazon ECR**và hệ thống được giám sát thông qua **Amazon CloudWatch**.

---

## 2. Kiến trúc hệ thống

Kiến trúc của hệ thống bao gồm các thành phần chính sau:

- Người dùng (Client)
- Cân bằng tải
- Hạ tầng mạng
- Ứng dụng chạy trên Container
- Dịch vụ lưu trữ
- Quản lý Docker Image
- Bảo mật và giám sát

**Hình 1 – Kiến trúc hệ thống Warehouse Inventory Management**

![Kiến trúc hệ thống](/images/5-Workshop/5.1-Workshop-overview/diagram.png)

---

## 3. Quy trình hoạt động của hệ thống

Luồng xử lý chính của hệ thống diễn ra theo các bước sau:

1. Người dùng truy cập website thông qua địa chỉ DNS công khai của **Application Load Balancer (ALB)**.

2. Mọi yêu cầu từ người dùng được chuyển trực tiếp qua cổng HTTP:80 đến **Application Load Balancer (ALB)**

3. ALB phân phối lưu lượng truy cập đến các container đang chạy trên **Amazon ECS Fargate.**.

4. Ứng dụng Node.js xử lý nghiệp vụ và giao tiếp với **MongoDB Atlas** để lưu trữ cũng như truy xuất dữ liệu.

5. Hình ảnh sản phẩm được tải lên và lưu trữ trên **Amazon S3**.

6. Các thông tin cấu hình nhạy cảm như chuỗi kết nối cơ sở dữ liệu được lấy từ **AWS Secrets Manager**.

7. Nhật ký hoạt động (Logs) và các chỉ số hệ thống (Metrics) được gửi đến **Amazon CloudWatch** để phục vụ việc giám sát và xử lý sự cố.

8. Xây dựng Docker Image từ máy cá nhân,đẩy lên **Amazon ECR** và triển khai phiên bản mới lên **Amazon ECS**.

---

## 4. Các dịch vụ được sử dụng

Workshop sử dụng các dịch vụ AWS sau:

### Hạ tầng mạng

- Amazon VPC
- Public Subnet
- Internet Gateway
- Security Groups

### Dịch vụ tính toán

- Amazon ECS Fargate
- Application Load Balancer

### Lưu trữ

- Amazon S3
- MongoDB Atlas

### Container

- Docker
- Amazon Elastic Container Registry (Amazon ECR)

### Bảo mật

- AWS IAM
- AWS Secrets Manager


### Giám sát

- Amazon CloudWatch

---

## 5. Kết quả đạt được

Sau khi hoàn thành workshop, bạn sẽ có thể:

- Triển khai ứng dụng Node.js dưới dạng container trên Amazon ECS Fargate.
- Xây dựng hạ tầng mạng bằng Amazon VPC và Internet Gateway.
- Kết nối và sử dụng MongoDB Atlas làm cơ sở dữ liệu.
- Lưu trữ hình ảnh sản phẩm trên Amazon S3.
- Bảo vệ thông tin cấu hình bằng AWS Secrets Manager.
- Cấu hình phân phối lưu lượng truy cập với Application Load Balancer (ALB).
- Đóng gói Docker Image và quản lý phiên bản trên Amazon ECR
- Giám sát hoạt động và log của ứng dụng thông qua Amazon CloudWatch.
- Xóa toàn bộ tài nguyên AWS sau khi hoàn thành workshop để tránh phát sinh chi phí.