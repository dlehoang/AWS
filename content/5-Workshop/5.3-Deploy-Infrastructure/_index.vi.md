---
title : "Triển khai hạ tầng Smart Parking"
date : 2026-07-10
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

#### Triển khai hạ tầng

Trong phần này, bạn sẽ triển khai hạ tầng cần thiết cho hệ thống **Smart Parking** trên nền tảng AWS.

Quá trình triển khai bắt đầu bằng việc khởi tạo một máy chủ **Amazon EC2** để lưu trữ và vận hành ứng dụng Smart Parking. Sau khi EC2 được tạo, bạn sẽ cấu hình hệ điều hành, cài đặt các phần mềm cần thiết và chuẩn bị môi trường triển khai.

Khi máy chủ đã sẵn sàng, bạn sẽ triển khai ứng dụng Smart Parking và kiểm tra để đảm bảo hệ thống hoạt động ổn định.

Hạ tầng được triển khai trong phần này sẽ là nền tảng để kết nối cơ sở dữ liệu, cấu hình các dịch vụ AWS và triển khai các chức năng của hệ thống trong những phần tiếp theo.

![overview](/images/5-Workshop/5.3-Deploy-Infrastructure/w3.jpg)

#### Nội dung

- [Khởi tạo máy chủ Amazon EC2](5.3.1-launch-ec2/)
- [Cấu hình máy chủ EC2](5.3.2-configure-ec2/)
- [Triển khai ứng dụng Smart Parking](5.3.3-deploy-application/)