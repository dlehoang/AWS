---
title : "Triển khai ứng dụng Smart Parking"
date : 2026-07-10
weight : 3
chapter : false
pre : " <b> 5.3.3 </b> "
---

Trong phần này, bạn sẽ triển khai ứng dụng **Smart Parking** lên máy chủ Amazon EC2.

Quá trình triển khai bao gồm việc sao chép ứng dụng lên EC2, khởi chạy ứng dụng và kiểm tra để đảm bảo hệ thống Smart Parking có thể truy cập thông qua địa chỉ Public IP của máy chủ.

## Tải ứng dụng lên EC2

1. Sao chép thư mục **publish** của ứng dụng Smart Parking lên máy chủ EC2.

Bạn có thể sử dụng **SCP**, **WinSCP** hoặc bất kỳ công cụ truyền tệp nào phù hợp.

![upload](/images/5-Workshop/5.3-Deploy-Infrastructure/upload.jpg)

---

## Publish ứng dụng

Nếu ứng dụng chưa được publish, hãy thực hiện lệnh sau trong thư mục dự án:

```bash
dotnet publish -c Release -o publish
```

Sau khi quá trình publish hoàn tất, sao chép thư mục **publish** lên máy chủ EC2.

![publish](/images/5-Workshop/5.3-Deploy-Infrastructure/publish.jpg)

---

## Khởi chạy ứng dụng

Di chuyển đến thư mục **publish**.

```bash
cd publish
```

Khởi động ứng dụng Smart Parking bằng lệnh:

```bash
dotnet SmartParking.dll
```

Nếu ứng dụng khởi động thành công, màn hình Terminal sẽ hiển thị thông báo tương tự:

```text
Now listening on: http://localhost:5000
Application started.
```

![run](/images/5-Workshop/5.3-Deploy-Infrastructure/run.jpg)

---

## Kiểm tra kết quả triển khai

Mở trình duyệt web.

Nhập địa chỉ Public IP của máy chủ EC2 theo cú pháp:

```text
http://<EC2-Public-IP>:5000
```

Nếu triển khai thành công, giao diện trang chủ của hệ thống Smart Parking sẽ được hiển thị.

![homepage](/images/5-Workshop/5.3-Deploy-Infrastructure/homepage.jpg)

---

## Tổng kết

Chúc mừng!

Bạn đã triển khai thành công ứng dụng **Smart Parking** trên máy chủ Amazon EC2.

Ứng dụng hiện đã hoạt động ổn định và sẵn sàng để kết nối với cơ sở dữ liệu cũng như tích hợp các dịch vụ AWS khác trong các phần tiếp theo.