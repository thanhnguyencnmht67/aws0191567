---
title : "Cấu hình mạng"
date: 2026-09-07
weight : 2
chapter : false
pre : " <b> 4.4.2. </b> "
---

## Cấu hình mạng

Sau khi tạo Virtual Private Cloud (VPC), bước tiếp theo là cấu hình các thành phần mạng cần thiết để các dịch vụ có thể kết nối ra Internet và giao tiếp với MongoDB Atlas.

Trong phần này, bạn sẽ tạo 2 Public Subnet trên 2 Availability Zones (AZs) khác nhau, gắn Internet Gateway và cấu hình Route Table để định tuyến lưu lượng mạng.

---

## Tạo Public Subnet

Truy cập:

**AWS Console → VPC → Subnets → Create subnet**

Tại mục **VPC ID**, chọn inventor-vpc


Điền thông tin tạo 2 Subnet:

| Name | Availability Zone | IPv4 CIDR |
|------|-------------------|------------|
| public-subnet-a | ap-southeast-1a | 10.0.1.0/24 |
| public-subnet-b | ap-southeast-1b | 10.0.2.0/24 |

Bật tính năng tự cấp Public IP cho cả 2 Subnet:

Chọn **inventory-public-subnet-a → Action → Edit Subnet setting → Tích chọn Enable auto - assign public IPv4 address → save**

Lặp lại thao tác trên cho **inventory-public-subnet-b**.


---

## Cấu hình Internet Gateway

Internet Gateway cho phép các tài nguyên bên trong VPC kết nối ra mạng Internet công cộng.

Truy cập:

**AWS Console → VPC → Internet Gateways → Create internet gateway**

Cấu hình:

| Thuộc tính | Giá trị |
|------------|----------|
| Name | inventory-igw |

Sau khi tạo:

- Chọn **Attach to VPC**
- Chọn **inventory-vpc**

Kiểm tra trạng thái Internet Gateway là **Attached**.


---



## Cấu hình Route Table

Route Table quy định đường đi của các gói tin mạng từ Subnet ra Internet Gateway để ứng dụng kết nối ra Internet và giao tiếp với MongoDB Atlas.

Truy cập:

**AWS Console → VPC → Route Tables → Create route table**

Tạo Route Table:

| Thuộc tính | Giá trị |
|------------|---------|
| Tên (Name) | inventory-public-rt |
| VPC | inventory-vpc |

Bấm **Create route table**.

---

### Cấu hình Tuyến đường (Routes)

Chọn inventory-public-rt, tại tab **Routes** ở phía dưới chọn **Edit routes** và thêm đường truyền ra Internet Gateway:

| Destination | Target |
|-------------|--------|
| 0.0.0.0/0 | inventory-igw (Internet Gateway) |

Bấm **Save changes**.


---

### Liên kết Subnet (Subnet Associations)

Tại tab **Subnet associations**, chọn **Edit subnet associations**, tích chọn cả 2 Public Subnet để áp dụng bảng định tuyến:

- inventory-public-subnet-a
- inventory-public-subnet-b

Bấm **Save associations**.

---



## Kết quả mong đợi

Sau khi hoàn thành phần này, bạn sẽ có:

- 2 Public Subnet nằm trên 2 Availability Zones khác nhau (ap-southeast-1a và ap-southeast-1b) đã bật tự động cấp IP công cộng.
- Một Internet Gateway (inventory-igw) được liên kết thành công với inventory-vpc.
- Một Public Route Table (inventory-public-rt) định tuyến toàn bộ lưu lượng 0.0.0.0/0 qua Internet Gateway và áp dụng cho cả 2 Subnet.
- Hạ tầng mạng sẵn sàng để cấu hình Security Group ở phần tiếp theo.