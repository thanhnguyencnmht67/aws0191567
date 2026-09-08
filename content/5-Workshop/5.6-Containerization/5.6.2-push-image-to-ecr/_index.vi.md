---
title : "Đẩy Image lên Amazon ECR"
date: 2026-09-07
weight : 2
chapter : false
pre : " <b> 4.6.2. </b> "
---

## Đẩy Image lên Amazon ECR

Trong phần này, sẽ khởi tạo Private Repository trên dịch vụ Amazon Elastic Container Registry (Amazon ECR), xác thực Docker client với AWS và tải (push) Container Image của ứng dụng Warehouse Inventory Management lên kho lưu trữ đám mây.

Amazon ECR tích hợp chặt chẽ với AWS IAM và Amazon ECS, cho phép quản trị quyền truy cập chi tiết và tự động quét lỗ hổng bảo mật mỗi khi có image mới được đẩy lên.
---

## Tạo Amazon ECR Repository

Bạn có thể tạo kho lưu trữ trực tiếp bằng lệnh AWS CLI ngay trên cửa sổ AWS CloudShell:

```bash
aws ecr create-repository \
  --repository-name inventory-app \
  --region ap-southeast-1 \
  --image-scanning-configuration scanOnPush=true
  ```

Hoặc cấu hình Repository qua giao diện **AWS management Console**:
Điều hướng đến **Amazon ECR → Private repositories → Create repository** 

| Thuộc tính | Giá trị |
|------------|----------|
| Visibility settings | Private |
| Repository name | inventory-app |
| Tag immutability | Disabled |
| Scan on push | Enabled |
| KMS encryption | AES-256 |


Chọn **Create repository**.

![Create Repository](/images/5-Workshop/5.6-Containerization/5.6.2.1.png)

---

## Đăng nhập Docker vào Amazon ECR

Trên cửa sổ AWS CloudShell, lấy mã xác thực tạm thời thông qua AWS CLI và đăng nhập Docker Client vào ECR Registry:

```bash
aws ecr get-login-password --region ap-southeast-1 | docker login --username AWS --password-stdin 097040011859.dkr.ecr.ap-southeast-1.amazonaws.com
```

Sau khi xác thực thành công, sẽ hiển thị:

```text
Login Succeeded
```

---

## Tag Docker Image

Gắn thẻ Image cục bộ khớp với định danh URI của kho lưu trữ Amazon ECR:

```bash
docker tag inventory-app:latest <account-id>.dkr.ecr.ap-southeast-1.amazonaws.com/inventory-app:latest

```

 kiểm tra lại danh sách image để xác nhận tag mới đã được gắn chính xác:

```bash
docker images
```
---

## Đẩy Docker Image lên Amazon ECR

Thực hiện lệnh tải container image lên kho chứa ECR:

```bash
docker push <account-id>.dkr.ecr.ap-southeast-1.amazonaws.com/inventory-app:latest
```

Quá trình đẩy diễn ra tuần tự từng lớp (layers) của image lên Amazon ECR và kết thúc khi toàn bộ các layer hiển thị trạng thái Pushed.

---

## Kiểm tra Repository trên ECR Console

Truy cập:

**AWS Console → Amazon ECR → Private repositories**

Chọn repository **inventory-app**.

Xác nhận Docker Image hiển thị với tag latest, kích thước nén khoảng 60-70 MB và trạng thái quét an toàn không có cảnh báo nghiêm trọng.

![Repository Images](/images/5-Workshop/5.6-Containerization/5.6.2.1.png)

---

## Kết quả mong đợi

Sau khi hoàn thành phần này, bạn sẽ có:

- Một Amazon ECR Private Repository mang tên inventory-app được khởi tạo thành công tại Region Singapore (ap-southeast-1).
- Phiên làm việc Docker được xác thực bảo mật với kho lưu trữ ECR.
- Container Image của ứng dụng quản lý kho được đóng gói, gắn tag và lưu trữ an toàn trên đám mây.
- Image sẵn sàng phục vụ cho việc tạo ECS Task Definition và triển khai dịch vụ trên Amazon ECS Fargate ở Chương 4.7.