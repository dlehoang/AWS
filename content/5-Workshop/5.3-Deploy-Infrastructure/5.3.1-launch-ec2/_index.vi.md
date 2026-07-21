---
title : "Khởi tạo máy chủ Amazon EC2"
date : 2026-07-10
weight : 1
chapter : false
pre : " <b> 5.3.1 </b> "
---

Trong phần này, bạn sẽ khởi tạo một máy chủ **Amazon EC2** để triển khai ứng dụng Smart Parking.

Máy chủ EC2 sẽ đóng vai trò là máy chủ ứng dụng, nơi triển khai backend và các dịch vụ cần thiết của hệ thống Smart Parking.

### Tạo máy chủ EC2

1. Đăng nhập vào **AWS Management Console**.

2. Trong thanh tìm kiếm, nhập **EC2**, sau đó chọn **EC2** để mở **Amazon EC2 Console**.

![ec2-console](/images/5-Workshop/5.3-Deploy-Infrastructure/ec2-console.jpg)

3. Trong thanh điều hướng bên trái, chọn **Instances**, sau đó nhấn **Launch instances**.

![launch-instance](/images/5-Workshop/5.3-Deploy-Infrastructure/launch-instance.jpg)

4. Cấu hình máy chủ EC2 với các thông số sau:

+ **Tên máy chủ:** `SmartParking`

+ **Amazon Machine Image (AMI):**
    + Ubuntu Server 24.04 LTS (64-bit)

+ **Loại máy (Instance type):**
    + t3.micro (Free Tier eligible)

![instance-config](/images/5-Workshop/5.3-Deploy-Infrastructure/instance-config.jpg)

5. Tạo mới hoặc chọn **Key Pair** đã có để phục vụ việc kết nối SSH đến máy chủ.

![keypair](/images/5-Workshop/5.3-Deploy-Infrastructure/keypair.jpg)

6. Cấu hình các thiết lập mạng.

+ Chọn **VPC** dành cho hệ thống Smart Parking.
+ Chọn **Public Subnet** phù hợp.
+ Bật **Auto-assign Public IP**.
+ Tạo mới hoặc chọn **Security Group** đã có.

Cho phép các quy tắc **Inbound** sau:

| Loại | Cổng |
|------|------|
| SSH | 22 |
| HTTP | 80 |
| HTTPS | 443 |

![security-group](/images/5-Workshop/5.3-Deploy-Infrastructure/security-group.jpg)

7. Giữ nguyên các thiết lập còn lại, sau đó nhấn **Launch Instance** để khởi tạo máy chủ.

![launch](/images/5-Workshop/5.3-Deploy-Infrastructure/lanch.jpg)

8. Chờ đến khi trạng thái của EC2 chuyển sang **Running** và cả hai **Status checks** đều hiển thị **Passed**.

![running](/images/5-Workshop/5.3-Deploy-Infrastructure/running.jpg)

Đến đây, máy chủ Amazon EC2 đã được khởi tạo thành công và sẵn sàng cho việc cấu hình cũng như triển khai ứng dụng Smart Parking trong các bước tiếp theo.