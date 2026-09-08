---
title : "Build Docker Image"
date: 2026-09-07
weight : 1
chapter : false
pre : " <b> 4.6.1. </b> "
---

## Build Docker Image

Trong phần này, bạn sẽ chuẩn bị mã nguồn, cấu hình Dockerfile, tệp loại trừ .dockerignore và tiến hành build Docker Image cho ứng dụng Warehouse Inventory Management trực tiếp trên môi trường **AWS CloudShell**.

Sử dụng AWS CloudShell giúp tận dụng môi trường điện toán đám mây tích hợp sẵn Docker engine, đảm bảo quá trình build image tương thích hoàn toàn với hạ tầng Linux x86_64 của Amazon ECS Fargate.

Tạo tệp .dockerignore

Tại thư mục gốc của dự án, tạo một tệp mang tên **.dockerignore** để loại bỏ các tệp không cần thiết trước khi đóng gói:

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

![Dockerfile](/images/5-Workshop/5.6-Containerization/5.6.1.png)

---


## Build Docker Image trên AWS Cloudshell

Truy cập vào AWS Management Console, bấm vào biểu tượng **CloudShell** ở thanh điều hướng trên cùng (góc phải hoặc góc trái dưới).

Tải toàn bộ mã nguồn dự án lên **CloudShell** hoặc giải nén thư mục dự án vào thư mục làm việc.

Di chuyển vào thư mục dự án và tiến hành build Docker Image:

```bash
docker build -t inventory-app .
```

Trong quá trình build, hệ thống sẽ thực hiện các bước sau:

1. Kéo base image Node.js 20 Alpine.
2. Thiết lập thư mục làm việc /app.
3. Cài đặt các dependencies thông qua npm install.
4. Đóng gói toàn bộ mã nguồn thành Docker Image độc lập.


Để kiểm tra Docker Image vừa tạo, chạy lệnh:

```bash
docker images
```

Xác nhận Image mang tên inventory-app hiển thị với tag **latest**.

---

## Kết quả mong đợi

Sau khi hoàn thành phần này, bạn sẽ có:

- Tệp .dockerignore và Dockerfile chuẩn hóa cho ứng dụng quản lý kho.
- Docker Image mang tên inventory-app được build thành công trên AWS CloudShell.
- Image sẵn sàng để gắn thẻ (tag) và đẩy (push) lên kho lưu trữ Amazon ECR ở bài tiếp theo.