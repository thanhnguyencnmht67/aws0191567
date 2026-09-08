---
title : "Kiểm thử"
date: 2026-09-07
weight : 9
chapter : false
pre : " <b> 4.9. </b> "
---

# 4.9. Kiểm thử

Phần này trình bày quá trình kiểm thử và xác thực hoạt động thực tế của hệ thống **Warehouse Inventory Management** sau khi được triển khai hoàn chỉnh trên hạ tầng AWS. Đồng thời minh họa các giao diện nghiệp vụ chính của ứng dụng và giải thích cách từng chức năng tương tác với hạ tầng đám mây bao gồm: **Amazon ECS (Fargate)**, **Application Load Balancer (ALB)**, **MongoDB / DocumentDB**, **Amazon ECR** và **Amazon CloudWatch**.

---
## Demo Video
Xem video trình diễn đầy đủ của hệ thống tại đây:

**YouTube:** https://www.youtube.com/watch?v=rQFgAupfTeA

# 1. Giao diện và Luồng nghiệp vụ Quản lý Kho

Ứng dụng được thiết kế dưới dạng Single Page Application (SPA) trực quan, tích hợp toàn bộ bảng điều khiển thống kê, form nhập hàng và bảng quản trị trên cùng một giao diện điều hành.


## A. Trang chủ & Bảng điều khiển thống kê

Trang chủ là trung tâm giám sát tình trạng tồn kho theo thời gian thực. Hệ thống hiển thị 3 chỉ số chính ở đầu trang:
- **Tổng danh mục hàng hóa**: Số lượng loại mặt hàng hiện có.
- **Tổng số lượng tồn kho**: Tổng số đơn vị sản phẩm đang lưu trữ trong kho.
- **Mặt hàng cần nhập thêm**: Tự động cảnh báo màu vàng khi số lượng tồn của một mặt hàng giảm xuống dưới mức an toàn.

### Tích hợp hạ tầng

Ứng dụng Node.js Express được đóng gói trong container chạy trên **Amazon ECS Fargate** và được định tuyến truy cập từ Internet thông qua **Application Load Balancer (ALB)**. Toàn bộ số liệu thống kê được tính toán và truy vấn trực tiếp từ cơ sở dữ liệu **MongoDB Atlas**.

---

## Luồng dữ liệu

Người dùng truy cập qua DNS của Load Balancer: http://inventory-alb-1446126155.ap-southeast-1.elb.amazonaws.com

↓

Application Load Balancer tiếp nhận yêu cầu và phân phối tới ECS Task trong Target Group.

↓

Container trên ECS Fargate thực hiện truy vấn MongoDB Atlas.

↓

Giao diện hiển thị các thẻ thống kê tổng quan và bảng danh mục hàng hóa.

<br>

---
### Thêm Mặt Hàng Vào Kho & Tải ảnh lên Amazon S3

Quản trị viên có thể thêm mặt hàng mới bằng cách nhập: **Mã SKU**, **Tên Sản Phẩm**, **Số Lượng Ban Đầu** và đính kèm **Hình Ảnh Minh Họa**.

### Tích hợp hạ tầng

- **Lưu trữ hình ảnh**: Tệp ảnh tải lên được gửi qua backend Node.js, sử dụng AWS SDK để tải trực tiếp lên **Amazon S3 Bucket** (inventory0191567-097040011859-ap-southeast-1-an).
- **Lưu trữ thông tin**: Đường dẫn ảnh công khai trên S3 cùng thông tin SKU, tên hàng và số lượng tồn được lưu trữ đồng bộ vào **MongoDB Atlas**.
- **IAM Task Role**: Container sử dụng quyền từ ecsTaskExecutionRole (được cấp policy AmazonS3FullAccess) để thực thi tác vụ ghi tệp vào S3 một cách an toàn.

---

## Thao Tác Nhập / Xuất Kho Nhanh

Tại bảng **Danh Sách Mặt Hàng Trong Kho**, hệ thống cung cấp 2 nút thao tác nhanh cho từng dòng sản phẩm:
- **Nhập (+1)**: Tăng số lượng tồn kho của mặt hàng lên 1 đơn vị.
- **Xuất (-1)**: Giảm số lượng tồn kho của mặt hàng đi 1 đơn vị. Khi số lượng giảm về mức , thẻ cảnh báo mặt hàng cần nhập thêm sẽ tự động kích hoạt.

### Tích hợp hạ tầng

Khi người dùng bấm nút Nhập hoặc Xuất, một request HTTP POST/PUT được gửi qua ALB tới ECS. Container cập nhật trực tiếp trường số lượng trong MongoDB Atlas và làm mới lại số liệu trên giao diện ngay lập tức mà không cần tải lại trang.

---

---

# Các dịch vụ AWS được sử dụng

Trong quá trình kiểm thử ứng dụng, nền tảng đã tích hợp các dịch vụ AWS sau:

| Dịch vụ AWS | Mục đích |
|-------------|----------|
| Amazon ECS Fargate | Lưu trữ và chạy ứng dụng Node.js Express |
| Amazon ECR | Lưu trữ Docker Image |
| Application Load Balancer (ALB) | Tiếp nhận lưu lượng HTTP từ Internet qua cổng 80 và cân bằng tải tới các ECS Tasks. |
| Target Group (IP Type) | Đăng ký địa chỉ IP nội bộ của các container Fargate và thực hiện Health Check định kỳ. |
| Amazon S3 | Lưu trữ hình ảnh sản phẩm được người dùng tải lên |
| MongoDB Atlas | Cơ sở dữ liệu NoSQL đám mây lưu trữ thông tin mặt hàng, số lượng tồn kho và đường dẫn ảnh. |
| Amazon CloudWatch Logs | Thu thập và lưu trữ toàn bộ nhật ký runtime của container |
| Amazon CloudWatch Alarms | Giám sát chỉ số CPU Utilization của ECS Service và kích hoạt cảnh báo khi vượt ngưỡng 80%. |
| AWS IAM | Quản lý Task Execution Role và Task Role cấp quyền kéo ECR, ghi CloudWatch Logs và truy cập S3. |

Việc toàn bộ các chức năng thống kê, thêm mặt hàng, tải ảnh lên S3 và tăng/giảm tồn kho hoạt động mượt mà qua DNS của ALB chứng minh hệ thống **Warehouse Inventory Management** đã được triển khai hoàn chỉnh và vận hành ổn định trên nền tảng AWS.