---
title : "Triển khai ứng dụng lên Amazon ECS"
date: 2026-09-07
weight : 2
chapter : false
pre : " <b> 4.7.2. </b> "
---

## Triển khai ứng dụng lên Amazon ECS

Trong phần này, sẽ tiến hành khởi tạo Amazon ECS Cluster, cấu hình Task Definition cho ứng dụng Warehouse Inventory Management, triển khai ECS Service hoạt động trên nền tảng Serverless AWS Fargate và liên kết trực tiếp với Application Load Balancer đã tạo ở bài trước.

---

## 1. Khởi tạo Amazon ECS Cluster

1. Truy cập: **AWS Management Console → Amazon Elastic Container Service → Clusters → Create cluster**.
2. Thiết lập thông số cụm:
   - **Cluster name**: inventory-cluster
   - **Infrastructure**: Tích chọn **AWS Fargate (serverless)**
   - **Monitoring**: Tùy chọn kích hoạt Container Insights (hoặc giữ mặc định)
3. Nhấn **Create** để hoàn tất tạo Cluster.


---

## 2. Cấu hình ECS Task Definition

Truy cập: **Amazon ECS → Task definitions → Create new task definition**.

### Cấu hình chung của Task:

| Thuộc tính | Giá trị |
| :--- | :--- |
| **Task definition family** | inventory-task |
| **Launch type** | AWS Fargate |
| **Operating system/Architecture** | Linux/X86_64 |
| **Task size - CPU** | 0.5 vCPU (hoặc 1 vCPU) |
| **Task size - Memory** | 1 GB (hoặc 2 GB) |
| **Task execution role** | ecsTaskExecutionRole |
| **Task role** | ecsTaskRole (hoặc để trống nếu ứng dụng không gọi trực tiếp AWS SDK) |

### Cấu hình Container:

Tại mục **Container - 1**:

| Thuộc tính | Giá trị |
| :--- | :--- |
| **Container name** | inventory-app |
| **Image URI** | 097040011859.dkr.ecr.ap-southeast-1.amazonaws.com/inventory-app:latest |
| **Essential container** | Yes |
| **Port mappings** | Port 80, Protocol TCP, App protocol HTTP |

### Cấu hình Biến môi trường (Environment variables):

Khai báo các biến môi trường kết nối cơ sở dữ liệu DocumentDB:
- **PORT**: 80 (Type: Value)
- **MONGODB_URI**: Nạp chuỗi kết nối DocumentDB hoặc nạp an toàn thông qua **ValueFrom** với Secret ARN từ **AWS Secrets Manager**.

Nhấn **Create** ở cuối trang để hoàn thành cấu hình Task Definition.


---

## 3. Tạo ECS Service và Cấu hình Mạng

Truy cập: **Amazon ECS → Clusters → inventory-cluster → tab Services → Create**.

### Cấu hình Deployment:

| Thuộc tính | Giá trị |
| :--- | :--- |
| **Existing cluster** | inventory-cluster |
| **Compute options** | Launch type |
| **Launch type** | FARGATE |
| **Application type** | Service |
| **Family** | inventory-task |
| **Revision** | Latest (phiên bản mới nhất) |
| **Service name** | inventory-service |
| **Desired tasks** | 1 |

### Cấu hình Networking:

| Thuộc tính | Giá trị |
| :--- | :--- |
| **VPC** | Chọn VPC của workshop (vpc-0f8f91f2107b86bec) |
| **Subnets** | Chọn các Subnet được phân bổ cho ứng dụng |
| **Security group** | Chọn Security Group của ECS cho phép nhận Inbound traffic từ ALB trên Port 80 |
| **Public IP** | Bật Enabled (nếu đặt ở Public Subnet) hoặc Disabled (nếu đặt ở Private Subnet có NAT Gateway) |

### Cấu hình Load Balancing:

| Thuộc tính | Giá trị |
| :--- | :--- |
| **Load balancer type** | Application Load Balancer |
| **Load balancer** | Chọn **inventory-alb** |
| **Container to load balance** | inventory-app 80:80 |
| **Target group** | Chọn **Use an existing target group** - **inventory-tg** |

Nhấn **Create** để hệ thống bắt đầu khởi chạy Service.


---

## 4. Kiểm tra triển khai và Xác minh hoạt động

1. **Kiểm tra trạng thái Service & Task:**
   - Trong giao diện **Amazon ECS → Clusters → inventory-cluster → Services → inventory-service**, xác nhận trạng thái Deployment hoàn tất và mục **Running tasks** đạt số lượng bằng **Desired tasks** (1/1).
   - Tại tab **Tasks**, xác nhận Task có trạng thái **RUNNING**.

2. **Kiểm tra trạng thái Target Group:**
   - Truy cập **EC2 → Target Groups → inventory-tg**.
   - Tại tab **Targets**, xác nhận địa chỉ IP của container hiển thị Health status là **Healthy**.

3. **Truy cập ứng dụng:**
   - Mở trình duyệt web và dán địa chỉ **DNS name** của Application Load Balancer:
   
   ```text
   [http://inventory-alb-1446126155.ap-southeast-1.elb.amazonaws.com](http://inventory-alb-1446126155.ap-southeast-1.elb.amazonaws.com)
   ```

## Kết quả mong đợi
Sau khi hoàn thành phần này, sẽ có:

Một Amazon ECS Cluster mang tên inventory-cluster vận hành hoàn toàn ở chế độ Serverless Fargate.

Task Definition cấu hình chuẩn xác với Container Image từ Amazon ECR và nạp bảo mật cấu hình DocumentDB.

ECS Service tự động đăng ký và duy trì container chạy ổn định phía sau Application Load Balancer.

Ứng dụng Warehouse Inventory Management được triển khai thành công, sẵn sàng phục vụ người dùng qua mạng Internet.