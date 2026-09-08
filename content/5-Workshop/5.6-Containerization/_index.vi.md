---
title : "Đóng gói ứng dụng"
date: 2026-09-07
weight : 6
chapter : false
pre : " <b> 4.6. </b> "
---

### Mục tiêu

Đóng gói ứng dụng Warehouse Inventory Management thành Docker Container và đẩy container image lên Amazon Elastic Container Registry (Amazon ECR) để chuẩn bị cho việc triển khai trên Amazon ECS Fargate.

---

## 1. Tổng quan

Trong chương này, bạn sẽ thực hiện quy trình đóng gói ứng dụng web quản lý kho hàng thành một Container Image hoàn chỉnh:
- Dockerfile và .dockerignore: Định nghĩa môi trường thực thi chuẩn (Node.js LTS, dependencies, source code) và loại bỏ các file thừa để tối ưu dung lượng image.
- Docker Build trên AWS CloudShell: Tận dụng môi trường điện toán đám mây tích hợp sẵn Docker engine để xây dựng và kiểm tra container image tương thích hạ tầng Linux x86_64.
- Amazon ECR: Khởi tạo private repository, xác thực AWS CLI và tải (push) image lên registry bảo mật của AWS.

Sau khi hoàn tất, Container Image lưu trữ trên Amazon ECR sẽ đóng vai trò là artifact chính để Amazon ECS Fargate kéo về và chạy tác vụ (Tasks).

---

## 2. Nội dung thực hành

Thực hiện lần lượt các phần sau:

- 4.6.1 Build Docker Image (Tạo Dockerfile, .dockerignore và build image trên AWS CloudShell)
- 4.6.2 Khởi tạo ECR Repository và Đẩy Image (Khởi tạo kho chứa Amazon ECR, xác thực Docker CLI, gắn tag và push image lên ECR)

---

## 3. Kết quả mong đợi

Sau khi hoàn thành chương này, bạn sẽ có:

- File Dockerfile và .dockerignore chuẩn hóa cho ứng dụng quản lý kho.
- Một Amazon ECR Private Repository mang tên inventory-app.
- Docker Container Image được build thành công tương thích kiến trúc linux/amd64 trên AWS CloudShell.
- Image được gắn tag và lưu trữ an toàn trên Amazon ECR, sẵn sàng phục vụ cấu hình ECS Task Definition ở Chương 4.7.