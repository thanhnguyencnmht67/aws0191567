---
title : "Cấu hình AWS Secrets Manager"
date: 2026-09-07
weight : 3
chapter : false
pre : " <b> 4.5.3. </b> "
---

## Cấu hình AWS Secrets Manager

Trong phần này, bạn sẽ sử dụng **AWS Secrets Manager** để lưu trữ an toàn các thông tin cấu hình nhạy cảm và biến môi trường của ứng dụng **Warehouse Inventory Management**.

Việc này giúp bảo vệ chuỗi kết nối cơ sở dữ liệu và thông tin xác thực, tránh việc lưu trực tiếp (hardcode) vào mã nguồn hoặc Dockerfile.

---

## 1. Tạo Secret mới

Truy cập:

**AWS Console → Secrets Manager → Store a new secret**

Chọn loại Secret:
- **Secret type:** Other type of secret
- **Key/value pairs:** Nhập các biến cấu hình ứng dụng:

| Key | Value mẫu | Mô tả |
| :--- | :--- | :--- |
| PORT | 80 | Cổng ứng dụng lắng nghe |
| MONGODB_URI | mongodb+srv://inventory_admin:<password>@cluster0... | Chuỗi kết nối MongoDB Atlas |
| AWS_REGION | ap-southeast-1 | Region triển khai dịch vụ |
| S3_BUCKET_NAME | inventory0191567-097040011859-ap-southeast-1-an | Tên S3 Bucket lưu trữ hình ảnh |
| SESSION_SECRET | WarehouseSecretKey2026!@# | Chuỗi khóa bí mật cho phiên làm việc |


Chọn **Next**.

---

## 2. Cấu hình tên và lưu trữ Secret

- **Secret name:** inventory-app-secrets
- **Description:** Environment variables for Warehouse Inventory Management
- **Automatic rotation:** Giữ mặc định Disable automatic rotation.

Xem lại toàn bộ thông tin và chọn **Store**.


---

## 3. Lấy Secret ARN

Sau khi khởi tạo thành công, truy cập vào chi tiết Secret inventory-app-secrets và sao chép mã **Secret ARN**:

```text
arn:aws:secretsmanager:ap-southeast-1:097040011859:secret:inventory-app-secrets-V2pD55