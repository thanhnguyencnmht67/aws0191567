---
title : "Cấu hình Amazon S3"
date : 2026-01-01
weight : 2
chapter : false
pre : " <b> 5.5.2. </b> "
---

## Cấu hình Amazon S3

Trong phần này, bạn sẽ tạo một **Amazon S3 Bucket** để lưu trữ hình ảnh sản phẩm, chứng từ và các tài liệu đính kèm cho ứng dụng **Warehouse Inventory Management**.

Amazon S3 cung cấp dịch vụ lưu trữ đối tượng có độ bền cao, tính sẵn sàng lớn và khả năng mở rộng linh hoạt.

---

## 1. Tạo S3 Bucket

Truy cập:

**AWS Console → S3 → Buckets → Create bucket**

Cấu hình các thông số sau:

| Thuộc tính | Giá trị cấu hình | Mô tả |
| :--- | :--- | :--- |
| **AWS Region** | ap-southeast-1 (Singapore) | Cùng khu vực với VPC và ECS |
| **Bucket name** | inventory-warehouse-media-<tên-của-bạn> | Tên duy nhất trên toàn cầu |
| **Object Ownership** | ACLs disabled (recommended) | Sử dụng IAM & Bucket Policy quản lý quyền |
| **Block Public Access** | *Bỏ chọn* Block all public access | Cho phép truy cập đọc ảnh từ trình duyệt |
| **Default Encryption** | SSE-S3 | Mã hóa dữ liệu lưu trữ phía máy chủ |

Xác nhận cảnh báo công khai và chọn **Create bucket**.

![Create S3 Bucket](/images/5-Workshop/5.5-Application-Services/create-s3-bucket.png)

---

## 2. Cấu hình Bucket Policy

Để người dùng bên ngoài có thể xem trực tiếp hình ảnh hàng tồn kho trên giao diện web, cần cấu hình chính sách đọc công khai (s3:GetObject).

Truy cập:

**Chọn Bucket vừa tạo → tab Permissions → Bucket policy → Edit**

Dán đoạn chính sách phân quyền sau (thay inventory0191567-097040011859-ap-southeast-1-an bằng tên Bucket thật của bạn):

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::inventory0191567-097040011859-ap-southeast-1-an/*"
        }
    ]
}