---
title: "Blog 2"
date: 2026-07-09
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# Xây dựng kiến trúc Microservices cho hệ thống Smart Parking trên AWS

Trong các hệ thống quản lý bãi đỗ xe thông minh, ứng dụng cần xử lý đồng thời nhiều nghiệp vụ như xác thực người dùng, quản lý bãi xe, đặt chỗ, thanh toán, gửi thông báo và cập nhật dữ liệu từ các thiết bị IoT theo thời gian thực. Nếu toàn bộ chức năng được xây dựng trong một ứng dụng đơn khối (Monolithic), việc mở rộng, bảo trì và triển khai sẽ gặp nhiều khó khăn khi số lượng người dùng tăng lên.

Để giải quyết vấn đề này, hệ thống **Smart Parking System on AWS** được thiết kế theo kiến trúc **Cloud Native Microservices**, triển khai trên **Amazon Elastic Container Service (Amazon ECS)** kết hợp với các dịch vụ Event-Driven của AWS nhằm tăng khả năng mở rộng, giảm sự phụ thuộc giữa các thành phần và nâng cao tính sẵn sàng của hệ thống.

---

# Kiến trúc Microservices

Thay vì triển khai toàn bộ chức năng trong một ứng dụng duy nhất, hệ thống được chia thành nhiều Microservice độc lập.

Các Microservice chính bao gồm:

- Auth Service
- User Service
- Parking Service
- Booking Service
- Payment Service
- Notification Service

Mỗi Microservice chỉ đảm nhiệm một nhóm chức năng riêng và giao tiếp với nhau thông qua các sự kiện (Event), giúp hệ thống dễ dàng mở rộng cũng như bảo trì.

---

# Vì sao lựa chọn Microservices?

Kiến trúc Microservices mang lại nhiều lợi ích cho hệ thống Smart Parking.

Các ưu điểm nổi bật gồm:

- Triển khai độc lập từng dịch vụ.
- Dễ dàng mở rộng riêng từng Microservice.
- Giảm ảnh hưởng khi một dịch vụ gặp sự cố.
- Hỗ trợ nhiều nhóm phát triển song song.
- Thuận tiện bổ sung các chức năng mới trong tương lai.

Toàn bộ Backend được triển khai trong **Amazon ECS Cluster** thuộc **Private Subnet**, đảm bảo các dịch vụ không truy cập trực tiếp từ Internet.

---

# Các Microservice chính

## Auth Service

Auth Service chịu trách nhiệm:

- Đăng ký tài khoản.
- Đăng nhập.
- Xác thực JWT.
- Phân quyền người dùng.

Đây là dịch vụ đầu tiên xử lý trước khi người dùng truy cập các chức năng khác của hệ thống.

---

## User Service

User Service quản lý:

- Hồ sơ người dùng.
- Thông tin phương tiện.
- Lịch sử đặt chỗ.
- Lịch sử thanh toán.

---

## Parking Service

Parking Service là thành phần quan trọng nhất của hệ thống.

Chức năng bao gồm:

- Quản lý bãi đỗ xe.
- Quản lý trạng thái các vị trí đỗ.
- Đồng bộ dữ liệu từ AWS IoT Core.
- Cập nhật trạng thái bãi xe theo thời gian thực.

Khi Camera, RFID Reader hoặc ESP32 phát hiện xe ra vào, Parking Service sẽ cập nhật trạng thái Slot trong Amazon RDS.

---

## Booking Service

Booking Service xử lý các nghiệp vụ:

- Đặt chỗ.
- Hủy đặt chỗ.
- Kiểm tra vị trí còn trống.
- Sinh mã QR.

Sau khi đặt chỗ thành công, dịch vụ sẽ phát sinh một sự kiện để các dịch vụ khác tiếp tục xử lý.

---

## Payment Service

Payment Service quản lý:

- Thanh toán.
- Hóa đơn.
- Lịch sử giao dịch.

Kiến trúc được thiết kế để dễ dàng tích hợp với nhiều cổng thanh toán như:

- VNPay
- Stripe
- PayPal
- MoMo

---

## Notification Service

Notification Service chịu trách nhiệm gửi thông báo đến người dùng.

Bao gồm:

- Email xác nhận đặt chỗ.
- Email thanh toán.
- Mã QR.
- Thông báo trạng thái xe ra vào.

Dịch vụ sử dụng Amazon SNS và Amazon SES để gửi thông báo.

---

# Giao tiếp giữa các Microservice

Thay vì gọi trực tiếp lẫn nhau, các Microservice giao tiếp theo mô hình **Event-Driven Architecture**.

Ví dụ luồng xử lý:

Booking Service

↓

Amazon EventBridge

↓

AWS Lambda

↓

Notification Service

↓

Amazon SES

Cách tiếp cận này giúp giảm sự phụ thuộc giữa các dịch vụ, đồng thời tăng khả năng mở rộng của hệ thống.

---

# Amazon EventBridge

Amazon EventBridge đóng vai trò là trung tâm tiếp nhận và phân phối các sự kiện.

Một số sự kiện của hệ thống:

- BookingCreated
- PaymentCompleted
- VehicleCheckedIn
- VehicleCheckedOut

Mỗi sự kiện sẽ được tự động chuyển đến đúng Microservice cần xử lý.

---

# AWS Lambda

AWS Lambda xử lý các tác vụ nền như:

- Sinh mã QR.
- Chuẩn bị Email.
- Xử lý dữ liệu.
- Đồng bộ thông tin.
- Kích hoạt Notification.

Lambda chỉ được kích hoạt khi có sự kiện nên giúp tối ưu tài nguyên và giảm chi phí vận hành.

---

# Amazon SQS

Amazon Simple Queue Service (Amazon SQS) được sử dụng để xử lý bất đồng bộ.

Khi lượng người dùng tăng cao, các yêu cầu sẽ được đưa vào Queue trước khi xử lý.

Việc sử dụng Amazon SQS giúp:

- Không mất dữ liệu.
- Tăng khả năng chịu tải.
- Giảm nghẽn hệ thống.
- Đảm bảo xử lý tuần tự.

---

# Amazon SNS và Amazon SES

Sau khi Lambda hoàn thành xử lý, Notification Service sẽ sử dụng:

- Amazon SNS để phát thông báo.
- Amazon SES để gửi Email.

Người dùng sẽ nhận được:

- Email xác nhận đặt chỗ.
- Email xác nhận thanh toán.
- QR Code.
- Thông báo trạng thái bãi xe.

---

# Lợi ích của kiến trúc

Việc triển khai Amazon ECS kết hợp với Amazon EventBridge, AWS Lambda, Amazon SQS, Amazon SNS và Amazon SES mang lại nhiều lợi ích:

- Dễ dàng mở rộng từng Microservice.
- Giảm sự phụ thuộc giữa các dịch vụ.
- Tăng tính sẵn sàng của hệ thống.
- Xử lý bất đồng bộ hiệu quả.
- Dễ bảo trì và nâng cấp.
- Tối ưu chi phí nhờ sử dụng các dịch vụ Managed Services của AWS.

---

# Kết luận

Kiến trúc Cloud Native Microservices kết hợp Event-Driven Architecture giúp hệ thống Smart Parking hoạt động ổn định, linh hoạt và dễ dàng mở rộng. Đây là nền tảng phù hợp để phát triển thêm các tính năng như nhận diện biển số xe bằng AI, phân tích dữ liệu bãi đỗ, dự báo lưu lượng phương tiện và triển khai đa khu vực (Multi-Region) trong tương lai.