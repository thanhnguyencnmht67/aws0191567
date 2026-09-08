---
title: "Đề xuất dự án"
date: 2026-09-07
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Warehouse Inventory Management

## Hệ thống Quản lý Kho hàng Cloud-Native trên AWS

---

# 1. Tóm tắt

Warehouse Inventory Management là ứng dụng web trên nền tảng điện toán đám mây hỗ trợ doanh nghiệp quản lý danh mục sản phẩm, theo dõi số lượng tồn kho và lưu trữ chứng từ hình ảnh hàng hóa tập trung. Nền tảng cung cấp các chức năng cốt lõi bao gồm: cập nhật số lượng tồn, phân loại mặt hàng, tải lên hình ảnh sản phẩm lên kho lưu trữ đám mây và báo cáo thống kê, đồng thời ứng dụng các dịch vụ AWS được quản lý để đảm bảo tính sẵn sàng cao, bảo mật và tối ưu chi phí vận hành.

Ứng dụng được xây dựng bằng **Node.js**, **Express.js**, cơ sở dữ liệu **MongoDB Atlas** và công cụ hiển thị giao diện **EJS**. Ứng dụng được đóng gói hoàn chỉnh bằng **Docker** và triển khai dưới dạng serverless container trên **Amazon ECS Fargate** phía sau **Application Load Balancer (ALB)**. Docker Image được quản lý an toàn trong **Amazon ECR**, hình ảnh sản phẩm được tải trực tiếp lên **Amazon S3** thông qua IAM Task Role.

Môi trường triển khai tích hợp **Amazon VPC** để cô lập hạ tầng mạng, **AWS IAM** để kiểm soát phân quyền đặc quyền tối thiểu, và **Amazon CloudWatch** để theo dõi hiệu năng hệ thống (Metrics/Logs/Alarms). Kiến trúc này giúp doanh nghiệp loại bỏ gánh nặng quản lý máy chủ vật lý, hỗ trợ tự động mở rộng theo tải thực tế.

---

# 2. Vấn đề & Giải pháp

## Vấn đề hiện tại

- **Quản lý thủ công, phân mảnh**: Nhiều doanh nghiệp vừa và nhỏ vẫn quản lý kho bằng file bảng tính cục bộ hoặc phần mềm cài đặt tại chỗ, dẫn đến sai lệch số liệu tồn kho theo thời gian thực.
- **Lưu trữ dữ liệu và hình ảnh kém tin cậy**: Hình ảnh chứng từ và sản phẩm lưu trữ trên ổ đĩa máy chủ dễ bị thất lạc hoặc quá tải dung lượng khi số lượng mặt hàng tăng cao.
- **Khó khăn trong mở rộng & bảo trì**: Kiến trúc nguyên khối truyền thống khiến việc cập nhật ứng dụng gây gián đoạn hệ thống (downtime), chi phí bảo trì phần cứng cao.

## Giải pháp đề xuất

Phát triển hệ thống Quản lý Kho hàng theo mô hình Cloud-Native tận dụng tối đa các dịch vụ được quản lý (Managed Services) của AWS:

- **Lưu trữ dữ liệu**: Thông tin mặt hàng, số lượng và lịch sử giao dịch được lưu trữ trên cụm **MongoDB Atlas**.
- **Lưu trữ hình ảnh**: Tệp tin hình ảnh sản phẩm được đẩy trực tiếp lên **Amazon S3**, đảm bảo độ bền dữ liệu cao và truy xuất nhanh chóng.
- **Môi trường thực thi**: Ứng dụng chạy trên **Amazon ECS Fargate**, loại bỏ nhu cầu cấu hình và vá lỗi hệ điều hành máy chủ EC2.
- **Định tuyến & Cân bằng tải**: **Application Load Balancer (ALB)** phân phối lưu lượng truy cập Internet vào các container task thông qua Target Group dạng IP.

## Lợi ích mang lại

- Đơn giản hóa quy trình triển khai nhờ chuẩn hóa Docker Container.
- Tự động phân phối tải và đảm bảo tính sẵn sàng cao.
- Lưu trữ hình ảnh sản phẩm không giới hạn dung lượng với Amazon S3.
- Tiết kiệm chi phí vận hành nhờ mô hình Serverless Fargate (chỉ trả phí theo tài nguyên CPU/RAM thực dùng).
- Giám sát tình trạng hệ thống và cảnh báo quá tải tài nguyên liên tục qua Amazon CloudWatch.

---

# 3. Kiến trúc giải pháp

Hệ thống được thiết kế theo kiến trúc container cloud-native phân lớp hoàn chỉnh:

## Kiến trúc giải pháp

![Kiến trúc hệ thống](/images/2-Proposal/diagram.png)

## Các dịch vụ AWS sử dụng

- **Amazon VPC & Security Groups**: Phân chia mạng và thiết lập tường lửa bảo vệ container.
- **AWS IAM**: Cung cấp quyền hạn thực thi cho ECS Agent và cấp quyền ghi S3 cho Task.
- **Amazon ECS Fargate**: Môi trường Serverless chạy container ứng dụng.
- **Amazon ECR**: Kho lưu trữ các phiên bản Docker image.
- **Amazon S3**: Lưu trữ tập trung toàn bộ hình ảnh sản phẩm.
- **Application Load Balancer (ALB)**: Tiếp nhận và điều hướng lưu lượng truy cập từ người dùng.
- **Amazon CloudWatch**: Thu thập logs container, giám sát chỉ số CPU/Memory và kích hoạt cảnh báo Alarm.
- **MongoDB Atlas**: Cụm cơ sở dữ liệu NoSQL lưu trữ thông tin nghiệp vụ.

## Thiết kế thành phần kỹ thuật

### Frontend
- HTML5, CSS3, JavaScript
- EJS Template Engine

### Backend
- Node.js & Express.js
- AWS SDK for JavaScript v3 (Client-S3)
- Multer (Xử lý upload multipart/form-data)
- Mongoose (Kết nối MongoDB)

### Cơ sở dữ liệu & Lưu trữ
- **Database**: MongoDB Atlas
- **Object Storage**: Amazon S3

---

# 4. Quy trình triển khai kỹ thuật

## Các giai đoạn thực hiện

1. **Chuẩn bị hạ tầng mạng & Bảo mật**: Tạo VPC, Subnets, Internet Gateway và cấu hình Security Groups mở cổng phù hợp.
2. **Thiết lập Cơ sở dữ liệu & Lưu trữ**: Cấu hình cụm MongoDB Atlas (Network Access, Database User) và tạo Amazon S3 Bucket lưu trữ ảnh.
3. **Đóng gói ứng dụng**: Viết Dockerfile, đóng gói mã nguồn thành Docker Image và kiểm tra chạy thử tại môi trường local.
4. **Đẩy Image lên ECR**: Khởi tạo Repository trên Amazon ECR, xác thực Docker client và đẩy image lên AWS.
5. **Cấu hình IAM Roles**: Thiết lập ecsTaskExecutionRole và gắn policy AmazonS3FullAccess để ứng dụng có quyền ghi vào S3.
6. **Cấu hình Load Balancing & ECS**:
   - Tạo Target Group dạng IP và cấu hình Health Check đường dẫn /.
   - Tạo Application Load Balancer trỏ về Target Group.
   - Khởi tạo ECS Cluster, Task Definition (khai báo các biến MONGODB_URI, S3_BUCKET_NAME, AWS_REGION) và khởi chạy ECS Service.
7. **Thiết lập Giám sát**: Cấu hình CloudWatch Logs stream và tạo CloudWatch Alarm giám sát ngưỡng CPU Utilization 
8. **Kiểm thử & Đánh giá**: Kiểm tra truy cập qua DNS của ALB, thêm mới sản phẩm kèm tải ảnh lên S3 và đối soát dữ liệu trên MongoDB Atlas.

---

# 5. Ước tính chi phí vận hành

Bảng tính toán chi phí vận hành ước tính hàng tháng cho môi trường chạy thử nghiệm/lab:

| Dịch vụ | Mức sử dụng ước tính | Chi phí ước tính |
|:---|:---|:---|
| **Amazon ECS Fargate** | 1 Task (0.25 vCPU, 0.5 GB RAM) chạy liên tục | ~0.30 USD/tháng |
| **Application Load Balancer** | 1 ALB phục vụ lưu lượng test | ~0.20 USD/tháng |
| **Amazon S3** | Lưu trữ < 1 GB ảnh & vài nghìn requests | ~0.05 USD/tháng |
| **Amazon ECR** | Lưu trữ 1 Docker Image (< 500 MB) | ~0.03 USD/tháng |
| **Amazon CloudWatch** | 1 Metric Alarm + Logs cơ bản (< 500 MB) | ~0.02 USD/tháng |
| **MongoDB Atlas** | Cụm miễn phí Shared M0 (512 MB Storage) | 0.00 USD |
| **Tổng ước tính** | | **~0.60 USD/tháng** |

---

# 6. Đánh giá rủi ro & Kế hoạch xử lý

## Ma trận rủi ro

- **Thiếu quyền IAM (Task Role)**: Ứng dụng không thể kết nối hoặc ghi tệp tin lên Amazon S3 (Could not load credentials).
- **Thiếu biến môi trường**: Code không xác định được S3 Bucket (No value provided for input HTTP label: Bucket) hoặc mất kết nối database.
- **Target Group Unhealthy**: Container không phản hồi đúng mã HTTP 200 tại đường dẫn Health Check.
- **Chi phí phát sinh**: Quên tắt Load Balancer hoặc ECS Tasks sau khi hoàn thành kiểm thử.

## Kế hoạch khắc phục & Dự phòng

- Cấp quyền AmazonS3FullAccess trực tiếp cho Task Role trong IAM.
- Khai báo đầy đủ các biến môi trường S3_BUCKET_NAME, AWS_REGION, MONGODB_URI trong Task Definition trước khi deploy.
- Sử dụng CloudWatch Logs để tra cứu stack trace và nhật ký lỗi thời gian thực của container.
- Thực hiện đầy đủ quy trình dọn dẹp tài nguyên (Xóa Service → Cluster → ALB → Target Group → S3 Bucket) ngay sau khi hoàn thành dự án.

---

# 7. Kết quả mong đợi

- Triển khai thành công ứng dụng **Warehouse Inventory Management** hoàn chỉnh trên AWS theo mô hình container.
- Hệ thống hoạt động ổn định, cân bằng tải mượt mà qua Application Load Balancer.
- Dữ liệu sản phẩm và tệp tin hình ảnh được phân tách lưu trữ an toàn giữa MongoDB Atlas và Amazon S3.
- Toàn bộ trạng thái hệ thống được giám sát chủ động bằng Amazon CloudWatch.