---
title : "Điều kiện chuẩn bị"
date : 2026-01-01
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

### Mục tiêu

Đảm bảo người đọc có thể truy cập AWS Management Console, tạo tài khoản cơ sở dữ liệu MongoDB Atlas, chuẩn bị đầy đủ các công cụ phát triển cần thiết và thiết lập mã nguồn dự án Warehouse Inventory Management trước khi bắt đầu triển khai lên hạ tầng đám mây.

---

## 1. Công cụ cần chuẩn bị

Workshop này sử dụng **AWS Management Console (Web UI)** kết hợp **Terminal/ Command line** cơ bản để đóng gói container và quản lý các tài nguyên AWS.

Chuẩn bị các phần mềm và tài khoản sau:

- **Node.js (v18+)**: Dùng để chạy ứng dụng trên máy cục bộ.
- **Docker Desktop**: Dùng để xây dựng Docker Image.
- **AWS CLI (v2)**: Dùng để xác thực đăng nhập Docker với kho lưu trữ **Amazzon ECR** từ máy cá nhân.
- **MongoDB Compass**: Phần mềm giao diện trực quan dùng để kết nối và kiểm tra dữ liệu tồn kho.
- **Tài khoản MongoDB Atlas (Cloud)**: Dịch vụ cơ sở dữ liệu NoSQL đám mây (gói M0 Free Tier).
- **Visual Studio Code (hoặc IDE khác)**: Dùng để chỉnh sửa mã nguồn.

---

## 2. Các bước thực hiện

**Đăng nhập AWS Console:** Đăng nhập vào AWS Management Console và đảm bảo Region được chọn là **ap-southeast-1 (Singapore)**.

**Checkpoint:** Xác nhận Region đang sử dụng là **ap-southeast-1** trước khi tạo tài nguyên.

**Kiểm tra công cụ cục bộ:** Đảm bảo các phần mềm đã được cài đặt thành công.

```bash
node --version
npm --version
aws --version
docker --version
```

**Checkpoint:** Tất cả các lệnh đều trả về phiên bản hợp lệ.

---

## 3. Kết quả mong đợi

- Đăng nhập thành công vào AWS Management Console.
- Chuẩn bị đầy đủ môi trường phát triển.
- Hoàn thành các điều kiện chuẩn bị trước khi chuyển sang chương tiếp theo.