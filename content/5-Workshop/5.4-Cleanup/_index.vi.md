---
title : "Dọn dẹp tài nguyên"
date : 2026-07-10
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

Chúc mừng bạn đã hoàn thành workshop!

Trong workshop này, bạn đã triển khai thành công hệ thống Smart Parking trên AWS. Bạn đã thực hiện việc tạo máy chủ Amazon EC2, cấu hình môi trường triển khai, triển khai ứng dụng Smart Parking, kết nối với cơ sở dữ liệu Amazon RDS và giám sát hệ thống bằng các dịch vụ AWS.

Để tránh phát sinh chi phí không cần thiết, hãy xóa toàn bộ các tài nguyên đã tạo trong quá trình thực hành.

## Dọn dẹp tài nguyên

### 1. Xóa máy chủ Amazon EC2

1. Mở **Amazon EC2 Console**.
2. Chọn máy chủ **SmartParking**.
3. Chọn **Instance state** → **Terminate instance**.
4. Xác nhận việc xóa máy chủ.

![terminate-ec2](/images/5-Workshop/5.4-Cleanup/terminate-ec2.jpg)
![terminate-ec2](/images/5-Workshop/5.4-Cleanup/terminate-ec21.jpg)

---

### 2. Xóa cơ sở dữ liệu Amazon RDS

1. Mở **Amazon RDS Console**.
2. Chọn cơ sở dữ liệu của Smart Parking.
3. Nhấn **Delete**.
4. Bỏ chọn tạo bản sao lưu cuối cùng (nếu không cần).
5. Xác nhận xóa cơ sở dữ liệu.

![delete-rds](/images/5-Workshop/5.4-Cleanup/delete-rds.jpg)

---

### 3. Kiểm tra lại

Truy cập AWS Management Console và kiểm tra để đảm bảo tất cả các tài nguyên đã được xóa thành công.

Chúc mừng! Bạn đã hoàn thành workshop Smart Parking và dọn dẹp toàn bộ tài nguyên AWS.