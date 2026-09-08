---
title : "Giám sát hệ thống"
date: 2026-09-07
weight : 8
chapter : false
pre : " <b> 4.8. </b> "
---

### Mục tiêu

Giám sát trạng thái hoạt động, thu thập nhật ký (Logs) và theo dõi số liệu hiệu năng (Metrics) của ứng dụng Warehouse Inventory Management thông qua Amazon CloudWatch.

---

## 1. Tổng quan

Trong chương này, bạn sẽ sử dụng Amazon CloudWatch để quan sát sức khỏe và hiệu năng của hệ thống:

- **Amazon CloudWatch Logs**: Thu thập và phân tích nhật ký thực thi từ container ECS Fargate để theo dõi trạng thái khởi động, kết nối cơ sở dữ liệu và xử lý request.
- **Container Insights**: Giám sát mức độ tiêu thụ tài nguyên phần cứng (CPU, Memory, Network) của các task trong ECS Cluster.
- **Application Load Balancer Metrics**: Đánh giá lưu lượng truy cập, mã phản hồi HTTP và thời gian phản hồi của dịch vụ.
---



## 2. Nội dung thực hành

Thực hiện phần thực hành sau:

- **4.8.1 Giám sát Logs và Metrics với CloudWatch** (Kiểm tra Log Streams của container và theo dõi biểu đồ Container Insights/ALB)

---

## 3. Kết quả mong đợi

Sau khi hoàn thành chương này, bạn sẽ có:

- Nắm được cách truy xuất và kiểm tra nhật ký ứng dụng trong CloudWatch Logs.
- Giám sát được các chỉ số tài nguyên thực tế của ECS Task trên AWS Fargate.
- Đánh giá được lưu lượng và độ ổn định của hệ thống qua Load Balancer Metrics.