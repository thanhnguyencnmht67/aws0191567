---
title : "Cấu hình Security Group"
date : 2026-01-01
weight : 3
chapter : false
pre : " <b> 5.4.3. </b> "
---

## Cấu hình Security Group

Security Group đóng vai trò như một tường lửa ảo kiểm soát lưu lượng truy cập vào và ra cho các tài nguyên trong VPC. 

Trong phần này, bạn sẽ cấu hình 2 Security Group theo nguyên tắc đặc quyền tối thiểu (Least Privilege):
1. **ALB Security Group:** Mở cổng 80 cho phép người dùng Internet truy cập vào Load Balancer.
2. **ECS Task Security Group:** Chỉ cho phép nhận lưu lượng từ ALB chuyển tiếp vào cổng 80, chặn hoàn toàn truy cập trực tiếp từ bên ngoài Internet.

---

## 1. Tạo Security Group cho Application Load Balancer

Truy cập:

**AWS Console → VPC (hoặc EC2) → Security Groups → Create security group**

Cấu hình thông tin cơ bản:

| Thuộc tính | Giá trị |
| :--- | :--- |
| **Security group name** | inventory-alb-sg |
| **Description** | Security group for Inventory ALB public access |
| **VPC** | inventory-vpc |

### Quy tắc chiều vào (Inbound Rules)

| Type | Port Range | Source | Description |
| :--- | :--- | :--- | :--- |
| HTTP | 80 | 0.0.0.0/0 | Cho phép lưu lượng HTTP từ Internet |

### Quy tắc chiều ra (Outbound Rules)

Giữ nguyên mặc định: All traffic tới 0.0.0.0/0.

Bấm **Create security group**.

![ALB Security Group](/images/5-Workshop/5.4-Networking/alb-sg.png)

---

## 2. Tạo Security Group cho Amazon ECS Tasks

Truy cập:

**AWS Console → Security Groups → Create security group**

Cấu hình thông tin cơ bản:

| Thuộc tính | Giá trị |
| :--- | :--- |
| **Security group name** | inventory-ecs-sg |
| **Description** | Security group for ECS tasks only from ALB |
| **VPC** | inventory-vpc |

### Quy tắc chiều vào (Inbound Rules)

| Type | Port Range | Source | Description |
| :--- | :--- | :--- | :--- |
| HTTP | 80 | inventory-alb-sg | Chỉ nhận lưu lượng chuyển tiếp từ ALB |

### Quy tắc chiều ra (Outbound Rules)

Giữ nguyên mặc định: All traffic tới 0.0.0.0/0 (đảm bảo container tải được Docker Image từ ECR và kết nối tới MongoDB Atlas).

Bấm **Create security group**.

![ECS Security Group](/images/5-Workshop/5.4-Networking/ecs-sg.png)

---

## Kết quả mong đợi

Sau khi hoàn thành phần này, bạn sẽ có:
 **inventory-alb-sg** quản lý lưu lượng công cộng của Application Load Balancer.
 **inventory-ecs-sg** bảo vệ các container ECS Fargate, chỉ mở kết nối từ ALB.
 Toàn bộ hạ tầng mạng (VPC, Subnet, Route Table, IGW, Security Groups) đã sẵn sàng để chuyển sang bước đóng gói Docker và triển khai container.