---
title : "Cấu hình Load Balancer"
date: 2026-09-07
weight : 1
chapter : false
pre : " <b> 4.7.1. </b> "
---

## Cấu hình Load Balancer

Trong phần này, bạn sẽ cấu hình Application Load Balancer (ALB) và Target Group cho ứng dụng Warehouse Inventory Management.

Application Load Balancer đóng vai trò là điểm tiếp nhận duy nhất từ Internet (Single Point of Contact), phân phối lưu lượng truy cập HTTP từ người dùng đến các container ứng dụng đang chạy trên Amazon ECS Fargate thông qua cơ chế định tuyến địa chỉ IP (Target Group).

---

## Tạo Target Group

Truy cập:

**AWS Console → EC2 → Target Groups → Create target group**

Cấu hình Target Group theo các thông số sau.

| Thuộc tính | Giá trị |
| :--- | :--- |
| **Target type** | IP addresses (Bắt buộc cho ECS Fargate) |
| **Target group name** | inventory-tg |
| **Protocol** | HTTP |
| **Port** | 80 |
| **IP address type** | IPv4 |
| **VPC** | Chọn VPC của bài thực hành 
| **Protocol version** | HTTP1 |

Trong mục **Health checks**:
- **Health check protocol**: HTTP
- **Health check path**: /
- Giữ nguyên các thông số nâng cao mặc định.

Nhấn **Next**, tại bước **Register targets** không thêm bất kỳ IP thủ công nào (Amazon ECS Service sẽ tự động đăng ký các IP của container vào đây sau), nhấn **Create target group**.

![Create Target Group](/images/5-Workshop/5.7-Deploy-Application/5.7.1.1.png)

---

## Tạo Application Load Balancer

Truy cập:

**AWS Console → EC2 → Load Balancers → Create Load Balancer**

Chọn **Application Load Balancer** và cấu hình các thông số sau.

| Thuộc tính | Giá trị |
| :--- | :--- |
| **Load Balancer name** | inventory-alb |
| **Scheme** | Internet-facing |
| **IP address type** | IPv4 |
| **VPC** | Chọn cùng VPC với Target Group |
| **Mappings (Availability Zones)** | Chọn tối thiểu 2 Availability Zones và tích chọn các **Public Subnets** tương ứng |

**Cấu hình Security Groups:**
- Gỡ bỏ Security Group mặc định (default).
- Chọn Security Group dành cho ALB (ví dụ: inventory-alb-sg cho phép Inbound HTTP cổng 80 từ 0.0.0.0/0).

![Create Load Balancer](/images/5-Workshop/5.7-Deploy-Application/5.7.1.2.png)

---

## Cấu hình Listener

Cấu hình Listener mặc định cho Application Load Balancer.

| Thuộc tính | Giá trị |
| :--- | :--- |
| **Protocol** | HTTP |
| **Port** | 80 |
| **Default action** | Forward to **inventory-tg** |

Kiểm tra lại cấu hình và chọn **Create Load Balancer**.

![Configure Listener](/images/5-Workshop/5.7-Deploy-Application/5.7.1.3.png)

---

## Kiểm tra Load Balancer

Truy cập:

**AWS Console → EC2 → Load Balancers**

Mở Application Load Balancer và xác nhận:

1. Chọn Load Balancer **inventory-alb**.
2. Xác nhận trạng thái State chuyển sang **Active** (quá trình khởi tạo mất khoảng 1-2 phút).
3. Ghi nhận lại giá trị **DNS name** (có định dạng tương tự: inventory-alb-123456789.ap-southeast-1.elb.amazonaws.com) để dùng truy cập ứng dụng sau khi triển khai xong ECS.
4. Chuyển sang tab **Listeners** và xác nhận Listener HTTP:80 đang Forward sang Target Group inventory-tg.

![Load Balancer Listeners](/images/5-Workshop/5.7-Deploy-Application/5.7.1.4.png)

![Load Balancer Details](/images/5-Workshop/5.7-Deploy-Application/5.7.1.5.png)

---

## Kết quả mong đợi

Sau khi hoàn thành phần này, bạn sẽ có:

- Một Target Group được tạo.
- Một Application Load Balancer được cấu hình.
- Listener chuyển tiếp lưu lượng đến Target Group.
- Load Balancer sẵn sàng tích hợp với Amazon ECS.