---
title : "Cấu hình MongoDB Atlas"
date: 2026-09-07
weight : 1
chapter : false
pre : " <b> 4.5.1. </b> "
---

## Cấu hình MongoDB Atlas

Trong phần này, bạn sẽ cấu hình MongoDB Atlas để làm cơ sở dữ liệu NoSQL đám mây cho ứng dụng **Warehouse Inventory Management**.

MongoDB Atlas chịu trách nhiệm lưu trữ các đối tượng dữ liệu như: thông tin sản phẩm, danh mục hàng hóa, số lượng tồn kho và lịch sử các phiếu nhập/xuất kho.

---

## 1. Tạo Database Cluster

1. Đăng nhập vào [MongoDB Atlas Console](https://cloud.mongodb.com/).
2. Truy cập: **Deployment → Database**.
3. Chọn gói **M0 (Free Tier)**, chọn nhà cung cấp **AWS** và vùng **Singapore (ap-southeast-1)** để tối ưu hóa độ trễ kết nối từ VPC.
4. Đặt tên Cluster (ví dụ: Cluster0 hoặc InventoryCluster) và bấm **Create Deployment**.
5. Sau khi tạo xong, kiểm tra trạng thái của Cluster hiển thị **Available (hoặc Active)**.

![MongoDB Cluster](/images/5-Workshop/5.5-Application-Services/5.5.1.png)

---

## 2. Tạo Database User

Truy cập:

**Security → Database Access → Add New Database User**

Cấu hình tài khoản truy cập:

| Thuộc tính | Giá trị cấu hình | Mô tả |
| :--- | :--- | :--- |
| **Authentication Method** | Password | Xác thực bằng tài khoản/mật khẩu |
| **Username** | inventory_admin | Tên người dùng cơ sở dữ liệu |
| **Password** | *(Tự tạo mật khẩu an toàn)* | Lưu lại để dùng trong connection string |
| **Database User Privileges** | Read and write to any database *(hoặc Built-in Role)* | Cấp quyền đọc/ghi dữ liệu kho |

Bấm **Add User** để hoàn tất.

![Database User](/images/5-Workshop/5.5-Application-Services/5.5.1.2.png)

---

## 3. Cấu hình Network Access

Truy cập:

**Security → Network Access → Add IP Address**

Để cho phép các container chạy trên AWS ECS Fargate và máy phát triển local có thể kết nối được:

| Thuộc tính | Giá trị | Ghi chú |
| :--- | :--- | :--- |
| **Access List Entry** | 0.0.0.0/0 | *Allow Access from Anywhere* (hoặc gán dải Public IP của ECS) |
| **Comment** | Allow ECS tasks and Local dev | Ghi chú mục đích |

Bấm **Confirm** và đợi IP chuyển sang trạng thái **Active**.

---

## 4. Lấy Chuỗi kết nối (Connection String)

1. Tại màn hình **Database Deployments**, bấm nút **Connect** ở Cluster của bạn.
2. Chọn phương thức kết nối: **Drivers** (Node.js).
3. Sao chép định dạng chuỗi kết nối MongoDB:

```text
mongodb+srv://inventory_admin:<password>@cluster0.xxxxx.mongodb.net/warehouse_db?retryWrites=true&w=majority