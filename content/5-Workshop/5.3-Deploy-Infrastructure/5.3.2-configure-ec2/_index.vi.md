---
title : "Cấu hình máy chủ Amazon EC2"
date : 2026-07-10
weight : 2
chapter : false
pre : " <b> 5.3.2 </b> "
---

Trong phần này, bạn sẽ cấu hình máy chủ **Amazon EC2** để chuẩn bị cho việc triển khai ứng dụng Smart Parking.

Quá trình cấu hình bao gồm cập nhật hệ điều hành, cài đặt các phần mềm cần thiết và kiểm tra môi trường trước khi triển khai ứng dụng.

## Kết nối đến máy chủ EC2

1. Mở **Amazon EC2 Console**.

2. Chọn máy chủ EC2 có tên **SmartParking**.

3. Nhấn **Connect**.

![connect](/images/5-Workshop/5.3-Deploy-Infrastructure/connect.jpg)

4. Chọn **EC2 Instance Connect** (hoặc kết nối bằng SSH nếu muốn), sau đó nhấn **Connect**.

![instance-connect](/images/5-Workshop/5.3-Deploy-Infrastructure/instance-connect.jpg)

Sau khi kết nối thành công, bạn sẽ truy cập được vào giao diện dòng lệnh (Terminal) của máy chủ EC2.

---

## Cập nhật hệ điều hành

Chạy các lệnh sau để cập nhật các gói phần mềm của hệ điều hành.

```bash
sudo apt update
sudo apt upgrade -y
```

---

## Cài đặt các phần mềm cần thiết

Cài đặt Git, .NET SDK và Nginx.

```bash
sudo apt install git -y
sudo apt install nginx -y
```

Cài đặt **.NET SDK 8.0**.

```bash
sudo apt install dotnet-sdk-8.0 -y
```

Kiểm tra quá trình cài đặt bằng các lệnh sau:

```bash
dotnet --version
git --version
nginx -v
```

---

## Cấu hình tường lửa

Cho phép truy cập thông qua các cổng HTTP và HTTPS.

```bash
sudo ufw allow 80
sudo ufw allow 443
sudo ufw enable
```

Kiểm tra trạng thái của tường lửa.

```bash
sudo ufw status
```

---

## Kiểm tra môi trường

Xác nhận rằng các phần mềm cần thiết đã được cài đặt thành công.

```bash
dotnet --version
git --version
systemctl status nginx
```

---

## Tổng kết

Chúc mừng! Bạn đã cấu hình thành công máy chủ **Amazon EC2** cho hệ thống Smart Parking.

Máy chủ hiện đã sẵn sàng để triển khai ứng dụng Smart Parking trong phần tiếp theo.