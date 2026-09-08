---
title : "Chuẩn bị dự án"
date: 2026-09-07
weight : 3
chapter : false
pre : " <b> 4.3. </b> "
---

## Chuẩn bị dự án

Chuẩn bị đầy đủ mã nguồn ứng dụng Warehouse Inventory Management, cài đặt các thư viện phụ thuộc, cấu hình biến môi trường và chạy thử nghiệm thành công trên môi trường máy cục bộ trước khi đóng gói thành Docker Image để đưa lên AWS.

---

## Tải mã nguồn dự án

Mở Terminal trên máy tính cá nhân và điều hướng đến thư mục làm việc của dự án:

```bash
cd quanlkhohang
```

---

## Cài đặt thư viện

Cài đặt tất cả các thư viện cần thiết cho dự án.

```bash
npm install
```

Đợi quá trình cài đặt hoàn tất.

---

## Cấu hình biến môi trường

Tạo tệp `.env` tại thư mục gốc của dự án và điền đầy đủ các thông tin kết nối dịch vụ:



```text
PORT=80
MONGODB_URI=mongodb+srv://admin:yVepZ1pl3497hw1m@cluster0.mjcduo5.mongodb.net/inventory?retryWrites=true&w=majority
AWS_REGION=ap-southeast-1
S3_BUCKET_NAME=inventory-app-media-2026


```
Khởi động ứng dụng bằng lệnh

```text
node server.js
```

Sau khi Terminal hiển thị thông báo kết nối thành công:

```text
Inventory App running on port 80
Connected to MongoDB Atlas
```

Mở trình duyệt web và truy cập địa chỉ:

```text
http://localhost
```


---

## Kết quả mong đợi

Sau khi hoàn thành phần này, bạn sẽ:

- Thiết lập hoàn chỉnh cấu trúc mã nguồn ứng dụng Warehouse Inventory Management.
- Cài đặt đầy đủ các gói thư viện phụ thuộc (node_modules).
- Cấu hình chính xác tệp biến môi trường .env kết nối với MongoDB Atlas và Amazon S3.
- Chạy thành công ứng dụng trên môi trường cục bộ và kiểm tra đầy đủ các tính năng nhập/xuất kho cùng hiển thị giao diện.