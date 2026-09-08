---

title : "Tạo VPC"

date: 2026-09-07

weight : 1

chapter : false

pre : " <b> 4.4.1. </b> "

---



## Tạo VPC



Trong phần này, bạn sẽ tạo một **Virtual Private Cloud (VPC)** để xây dựng môi trường mạng riêng cho ứng dụng **Warehouse Inventory Management** trên AWS.

VPC là nền tảng của toàn bộ hạ tầng mạng. Tất cả các tài nguyên như Subnet, Route Table, Internet Gateway, Application Load Balancer và Amazon ECS Fargate sẽ được triển khai bên trong VPC này.



---



## Tạo Virtual Private Cloud



Truy cập:



**AWS Console → VPC → Your VPCs → Create VPC**



Chọn **VPC only**, sau đó cấu hình như sau:



| Thuộc tính | Giá trị |

|------------|----------|

| Tài nguyên cần tạo | VPC only |

| Tên | inventory-vpc |

| IPv4 CIDR | 10.0.0.0/16 |

| IPv6 CIDR | None |

| Tenancy | Default |



Kiểm tra lại cấu hình và chọn **Create VPC**.



![Create VPC](/images/5-Workshop/5.4-VPC/5.4.1.1.png)



---



## Bật DNS Hostnames cho VPC



Truy cập:



Mặc định khi chọn "VPC only", AWS sẽ tắt DNS Hostnames. Cần bật lại để dịch vụ phân giải tên miền nội bộ hoạt động



Tạo danh sách **VPC only**, tích chọn  **inventory-vpc** 

Bấm menu **Action**, chọn**Edit VPC settings** 

Tại phần **DNS setting**, tích chọn  **Enable DNS resolution và Enable DNS hostname** 


Bấm **Save changes**.



![Create VPC](/images/5-Workshop/5.4-VPC/5.4.1.2.png)


---


## Kiểm tra VPC



Truy cập:



**AWS Console → VPC → Your VPCs**



Bấm vào **inventor-vpc** và kiểm tra các thông tin hiển thị:



| Thuộc tính | Giá trị mong đợi |

|------------|------------------|

| Trạng thái | Available |

| IPv4 CIDR | 10.0.0.0/16 |

| DNS Resolution | Enabled |

| DNS Hostnames | Enabled |



Xác nhận VPC đã được tạo thành công trước khi chuyển sang bước tạo Subnet và Route Table.




---



## Kết quả mong đợi



Sau khi hoàn thành phần này, bạn sẽ có:



- Một Virtual Private Cloud tên **inventory-vpc**.

- Môi trường mạng riêng với dải địa chỉ **10.0.0.0/16**.

- DNS Resolution và DNS Hostnames được bật.

- VPC sẵn sàng để cấu hình Subnet và các tài nguyên mạng ở bước tiếp theo. 

