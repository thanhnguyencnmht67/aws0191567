---
title : "Đóng gói ứng dụng"
date : 2026-01-01
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

### Mục tiêu

Đóng gói ứng dụng Warehouse Inventory Management thành Docker Container và đẩy container image lên Amazon Elastic Container Registry (Amazon ECR) để chuẩn bị cho việc triển khai trên Amazon ECS Fargate.

---

## 1. Tổng quan

Trong chương này, bạn sẽ thực hiện quy trình đóng gói ứng dụng web quản lý kho hàng thành một Container Image hoàn chỉnh:
- Dockerfile và .dockerignore: Định nghĩa môi trường thực thi chuẩn (Node.js LTS, dependencies, source code) và loại bỏ các file thừa để tối ưu dung lượng image.
- Docker Build: Xây dựng và kiểm tra container image ở môi trường local.
- Amazon ECR: Khởi tạo private repository, xác thực AWS CLI và tải (push) image lên registry bảo mật của AWS.

Sau khi hoàn tất, Container Image lưu trữ trên Amazon ECR sẽ đóng vai trò là artifact chính để Amazon ECS Fargate kéo về và chạy tác vụ (Tasks).

---

## 2. Nội dung thực hành

Thực hiện lần lượt các phần sau:

- 5.6.1 Tạo Dockerfile và .dockerignore (Định nghĩa quy trình build container)
- 5.6.2 Khởi tạo Private Repository trên Amazon ECR (Tạo kho lưu trữ trên AWS Console)
- 5.6.3 Build và Đẩy Docker Image lên Amazon ECR (Xác thực CLI, build image kiến trúc amd64 và push lên ECR)

---

## 3. Kết quả mong đợi

Sau khi hoàn thành chương này, bạn sẽ có:

- File Dockerfile và .dockerignore chuẩn hóa cho ứng dụng quản lý kho.
- Một Amazon ECR Private Repository mang tên inventory-app.
- Docker Container Image được build thành công tương thích kiến trúc linux/amd64.
- Image được gắn tag và lưu trữ an toàn trên Amazon ECR, sẵn sàng phục vụ cấu hình ECS Task Definition ở Chương 5.7.