---
title : "Triển khai ứng dụng"
date: 2026-09-07
weight : 7
chapter : false
pre : " <b> 4.7. </b> "
---

### Mục tiêu

Triển khai ứng dụng Warehouse Inventory Management lên Amazon Elastic Container Service (Amazon ECS) sử dụng nền tảng điện toán không máy chủ AWS Fargate.

---

## 1. Tổng quan

Trong chương này, bạn sẽ triển khai Container Image đã đóng gói trên Amazon ECR lên dịch vụ điều phối Amazon Elastic Container Service (Amazon ECS):

- **Amazon ECS & AWS Fargate**: Quản lý vòng đời của các container ứng dụng trên môi trường serverless, tự động cấp phát tài nguyên mà không cần quản lý hay bảo trì máy chủ EC2 bên dưới.
- **Task Definition**: Bản thiết kế chi tiết (blueprint) định nghĩa mức tài nguyên (vCPU, Memory), Container Image URI từ Amazon ECR, cổng mạng (Port 80) và các biến môi trường kết nối cơ sở dữ liệu DocumentDB thông qua AWS Secrets Manager.
- **ECS Service**: Duy trì số lượng Task mong muốn, tự động khôi phục Task khi có sự cố và tích hợp định tuyến mạng với VPC.
---

**4.7.1 Cấu hình Load Balancer** (Khởi tạo Target Group dạng IP và thiết lập Application Load Balancer để tiếp nhận lưu lượng HTTP từ Internet)
- **4.7.2 Triển khai ứng dụng lên Amazon ECS** (Khởi tạo ECS Cluster, cấu hình Task Definition nạp biến môi trường DocumentDB, triển khai ECS Service trên AWS Fargate và kiểm tra trạng thái hoạt động thực tế của ứng dụng)
---

## 3. Kết quả mong đợi

Sau khi hoàn thành chương này, bạn sẽ có:

- Một Amazon ECS Cluster mang tên inventory-cluster hoạt động ổn định.
- Task Definition được cấu hình chuẩn xác với IAM Role và Image URI từ Amazon ECR.
- ECS Service chạy trên AWS Fargate duy trì ứng dụng ở trạng thái Running.
- Ứng dụng quản lý kho được triển khai thành công, sẵn sàng tích hợp với Application Load Balancer ở Chương 4.8.