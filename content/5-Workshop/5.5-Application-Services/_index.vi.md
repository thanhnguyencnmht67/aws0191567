---
title : "Dịch vụ ứng dụng"
date : 2026-01-01
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

### Mục tiêu

Cấu hình các dịch vụ dữ liệu và lưu trữ cốt lõi cần thiết cho hệ thống **Warehouse Inventory Management**.

---

## 1. Tổng quan

Trong chương này, bạn sẽ cấu hình các dịch vụ dữ liệu và bảo mật bên ngoài phục vụ cho ứng dụng chạy trên Amazon ECS Fargate.

Ứng dụng quản lý kho sử dụng:
 **MongoDB Atlas:** Cơ sở dữ liệu NoSQL lưu trữ thông tin sản phẩm, số lượng tồn kho, đơn nhập/xuất và danh mục hàng hóa.
 **Amazon S3:** Lưu trữ hình ảnh sản phẩm, chứng từ và tài liệu kho đính kèm.
 **AWS Secrets Manager:** Quản lý an toàn các biến môi trường nhạy cảm (MONGODB_URI, S3 credentials, Session Secret) mà không cần hardcode vào mã nguồn.

Sau khi hoàn tất, ứng dụng sẽ có đầy đủ các dịch vụ lưu trữ và bảo mật sẵn sàng để kết nối khi container khởi chạy.

---

## 2. Nội dung thực hành

Thực hiện lần lượt các phần sau:

 **5.5.1 Cấu hình MongoDB Atlas** (Khởi tạo Cluster, Database User và Network Access)
 **5.5.2 Cấu hình Amazon S3** (Tạo S3 Bucket lưu trữ hình ảnh hàng tồn kho)
 **5.5.3 Cấu hình AWS Secrets Manager** (Lưu trữ chuỗi kết nối và thông tin bảo mật)

---

## 3. Kết quả mong đợi

Sau khi hoàn thành chương này, bạn sẽ có:

 Cluster **MongoDB Atlas** hoạt động, đã cấp quyền truy cập từ VPC/Container.
 S3 Bucket được khởi tạo với cấu hình phân quyền phù hợp để upload/view ảnh sản phẩm.
 Một Secret hoàn chỉnh trong **AWS Secrets Manager** chứa toàn bộ biến môi trường của ứng dụng.
 Nền tảng dịch vụ sẵn sàng cho việc đóng gói Docker và cấu hình ECS Task Definition.