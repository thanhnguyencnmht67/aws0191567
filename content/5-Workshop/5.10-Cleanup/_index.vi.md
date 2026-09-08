---
title: "Dọn dẹp tài nguyên"
date: 2026-09-07
weight: 10
chapter: false
pre: "<b> 4.10. </b>"
---

# 4.10. Dọn dẹp tài nguyên

## Tổng quan

Sau khi triển khai và kiểm thử thành công ứng dụng Warehouse Inventory Management, các tài nguyên AWS đã tạo trong workshop nên được xóa để tránh phát sinh chi phí không cần thiết.

Phần này hướng dẫn bạn xóa toàn bộ hạ tầng đã triển khai theo đúng thứ tự.

---

## Các bước dọn dẹp

Các tài nguyên AWS cần được xóa theo trình tự sau:

1. Amazon ECS Service
2. Amazon ECS Cluster
3. Amazon ECR Repository
4. Amazon S3 Bucket
5. Application Load Balancer
6. Target Group
7. Amazon CloudWatch Alarm




---

## 1. Xóa Amazon ECS Service

Truy cập:

**Amazon ECS → Clusters → inventory-cluster → Services**

Chọn:

- inventory-service

Nhấn:

**Delete Service**

Đợi trạng thái của Service chuyển sang **Inactive**.


---

## 2. Xóa Amazon ECS Cluster

Truy cập:

**Amazon ECS → Clusters**

Chọn:

- inventory-cluster

Nhấn:

**Delete Cluster**



---

## 3. Xóa Amazon ECR Repository

Truy cập:

**Amazon ECR → Private Repositories**

Chọn:

- inventory-app

Nhấn:

**Delete**

Xác nhận xóa Repository.


---

## 4. Xóa Amazon S3 Bucket

Truy cập:

**Amazon S3**

Chọn:

- inventory-uploads

Làm rỗng Bucket.

Sau đó xóa Bucket.


---

## 5. Xóa Application Load Balancer

Truy cập:

**EC2 → Load Balancers**

Chọn:

- inventory-alb

Nhấn:

**Delete**


---

## 6. Xóa Target Group

Truy cập:

**EC2 → Target Groups**

Chọn:

- inventory-tg

Nhấn:

**Delete**


---

## 7. Xóa Amazon CloudWatch Alarm

Truy cập:

**Amazon CloudWatch → Alarms**

Chọn:

- inventory-service-cpu-alarm

Nhấn:

**Delete**


---


---

## Kết quả

Sau khi hoàn thành tất cả các bước trên:

- Amazon ECS Service đã được xóa.
- Amazon ECS Cluster đã được xóa.
- Amazon ECR Repository đã được xóa.
- Amazon S3 Bucket đã được xóa.
- Application Load Balancer đã được xóa.
- Target Group đã được xóa.
- Amazon CloudWatch Alarm đã được xóa.


Toàn bộ tài nguyên AWS được tạo trong workshop đã được dọn dẹp thành công, giúp tránh phát sinh các chi phí không cần thiết.