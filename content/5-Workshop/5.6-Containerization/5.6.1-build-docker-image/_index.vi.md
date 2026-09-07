---
title : "Build Docker Image"
date : 2026-01-01
weight : 1
chapter : false
pre : " <b> 5.6.1. </b> "
---

## Build Docker Image

Trong phần này, bạn sẽ tạo Dockerfile, tệp loại trừ .dockerignore và build Docker Image cho ứng dụng Warehouse Inventory Management.

Docker giúp đóng gói toàn bộ mã nguồn cùng các thư viện phụ thuộc vào một container độc lập, đảm bảo môi trường chạy nhất quán tuyệt đối giữa máy phát triển cá nhân và hạ tầng đám mây Amazon ECS Fargate.

Tạo tệp .dockerignore

Tại thư mục gốc của dự án, tạo một tệp mang tên **.dockerignore** để tránh việc copy các thư mục nặng, file cấu hình nhạy cảm hoặc file tạm vào container image:

```text
node_modules
npm-debug.log
.env
.git
.gitignore
README.md
```

---

## Tạo Dockerfile

Mở thư mục dự án và tạo tệp **Dockerfile** tại thư mục gốc của dự án.

Dockerfile được sử dụng trong dự án như sau.

```dockerfile
FROM node:20-alpine

# Thư mục làm việc bên trong container
WORKDIR /app

# Sao chép file cấu hình phụ thuộc trước để tận dụng Docker Cache
COPY package*.json ./

# Cài đặt các thư viện phụ thuộc
RUN npm install

# Sao chép toàn bộ mã nguồn ứng dụng
COPY . .

# Mở cổng 80 cho ứng dụng web
EXPOSE 80

# Lệnh khởi chạy ứng dụng
CMD ["npm", "start"]
```

Lưu Dockerfile sau khi hoàn tất cấu hình.

![Dockerfile](/images/5-Workshop/5.6-Containerization/dockerfile.png)

---


## Build Docker Image

Sau khi tạo Dockerfile, mở Terminal tại thư mục gốc của dự án và thực hiện build Docker Image.

Chạy lệnh sau:

```bash
docker build -t inventory-app .
```

Trong quá trình build, Docker sẽ thực hiện các bước sau:

1. Tải base image Node.js 20 Alpine từ Docker Hub nếu chưa có trên máy.
2. Thiết lập thư mục làm việc /app bên trong container.
3. Cài đặt các thư viện của ứng dụng bằng lệnh **npm install**.
4. Sao chép toàn bộ mã nguồn của dự án vào container (bỏ qua các file trong .dockerignore).
5. Đóng gói ứng dụng thành một Docker Image hoàn chỉnh.


Để kiểm tra Docker Image vừa tạo, chạy lệnh:

```bash
docker images
```

Lệnh này sẽ hiển thị danh sách Docker Image trên máy. Xác nhận Docker Image vừa build xuất hiện với tag **latest**.

---

## Kết quả mong đợi

Sau khi hoàn thành phần này, bạn sẽ có:

- Tệp .dockerignore và Dockerfile chuẩn hóa cho ứng dụng quản lý kho.
- Docker Image mang tên inventory-app được build thành công trên máy local.
- Container Image sẵn sàng để gắn tag và tải lên Amazon Elastic Container Registry (Amazon ECR) ở phần tiếp theo.