---
title: "Blog 3"
date: 2026-07-09
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn, kể cả warning này.
{{% /notice %}}

# Xây dựng kiến trúc Event-Driven cho Smart Parking System trên AWS

Trong các hệ thống bãi đỗ xe thông minh, hàng nghìn sự kiện có thể xảy ra đồng thời như đặt chỗ, thanh toán, xe vào bãi, xe rời bãi hoặc gửi thông báo cho người dùng. Nếu tất cả các dịch vụ giao tiếp trực tiếp với nhau, hệ thống sẽ khó mở rộng và dễ xảy ra tình trạng quá tải.

Để giải quyết vấn đề này, Smart Parking System được thiết kế theo mô hình **Event-Driven Architecture (EDA)** kết hợp với các dịch vụ Managed Services của AWS. Mỗi Microservice chỉ tập trung xử lý nghiệp vụ của mình và giao tiếp với nhau thông qua các sự kiện (Event), giúp hệ thống hoạt động linh hoạt, dễ mở rộng và có khả năng chịu lỗi cao.

---

# Tại sao sử dụng Event-Driven Architecture?

Trong kiến trúc truyền thống, sau khi người dùng đặt chỗ thành công, Booking Service sẽ phải gọi trực tiếp đến Payment Service, Notification Service và Parking Service.

Cách làm này có một số nhược điểm:

- Các dịch vụ phụ thuộc trực tiếp vào nhau (Tight Coupling).
- Khó mở rộng khi số lượng người dùng tăng cao.
- Một dịch vụ gặp lỗi có thể ảnh hưởng đến toàn bộ hệ thống.
- Khó bảo trì và nâng cấp.

Đối với Smart Parking System, sau khi một sự kiện được tạo ra, các dịch vụ khác sẽ tự động xử lý thông qua EventBridge mà không cần gọi trực tiếp đến nhau.

---

# Luồng xử lý sự kiện trong Smart Parking System

Quy trình hoạt động của hệ thống được thực hiện như sau:

1. Người dùng đặt chỗ trên Website hoặc Mobile App.
2. Booking Service lưu thông tin đặt chỗ vào Amazon RDS.
3. Booking Service phát sinh sự kiện **BookingCreated**.
4. Amazon EventBridge tiếp nhận sự kiện.
5. EventBridge chuyển sự kiện đến các dịch vụ liên quan.
6. AWS Lambda xử lý các tác vụ nền như sinh QR Code hoặc xử lý dữ liệu.
7. Notification Service gửi Email xác nhận thông qua Amazon SES.
8. Payment Service chuẩn bị thông tin thanh toán.
9. Parking Service cập nhật trạng thái vị trí đỗ xe.

Nhờ cơ chế này, mỗi Microservice chỉ thực hiện đúng chức năng của mình mà không phụ thuộc vào các dịch vụ khác.

---

# Các dịch vụ AWS được sử dụng

## Amazon EventBridge

Amazon EventBridge đóng vai trò là trung tâm tiếp nhận và phân phối sự kiện của toàn hệ thống.

Chức năng chính:

- Tiếp nhận sự kiện từ các Microservices.
- Định tuyến sự kiện theo Rule.
- Kết nối các dịch vụ mà không cần gọi trực tiếp.
- Hỗ trợ kiến trúc Event-Driven.

Một số sự kiện tiêu biểu:

- BookingCreated
- BookingCancelled
- PaymentCompleted
- ParkingOccupied
- ParkingReleased

---

## AWS Lambda

AWS Lambda chịu trách nhiệm xử lý các tác vụ nền (Background Tasks) mà không cần quản lý máy chủ.

Các tác vụ bao gồm:

- Sinh mã QR.
- Xử lý dữ liệu đặt chỗ.
- Đồng bộ trạng thái bãi xe.
- Gửi dữ liệu sang các dịch vụ khác.
- Gọi API của bên thứ ba khi cần.

Việc sử dụng Lambda giúp giảm tải cho các Microservice chính và tiết kiệm chi phí vận hành.

---

## Amazon SQS

Amazon Simple Queue Service (SQS) được sử dụng để xử lý các tác vụ bất đồng bộ.

Lợi ích:

- Lưu tạm các yêu cầu khi lưu lượng tăng cao.
- Tránh mất dữ liệu khi một dịch vụ tạm thời không phản hồi.
- Hỗ trợ cơ chế Retry.
- Giảm tải cho Backend.

Ví dụ, khi nhiều người dùng đặt chỗ cùng lúc, các yêu cầu sẽ được lưu trong Queue và xử lý tuần tự.

---

## Amazon SNS

Amazon Simple Notification Service (SNS) giúp gửi thông báo đến nhiều dịch vụ hoặc người dùng cùng lúc.

Một số trường hợp sử dụng:

- Xác nhận đặt chỗ.
- Thanh toán thành công.
- Nhắc thời gian giữ chỗ.
- Thông báo hệ thống.

Một sự kiện có thể được gửi đến nhiều Subscriber khác nhau chỉ với một lần Publish.

---

## Amazon SES

Amazon Simple Email Service (SES) được sử dụng để gửi Email cho người dùng.

Hệ thống sử dụng SES để gửi:

- Email xác nhận đặt chỗ.
- Biên lai thanh toán.
- Mã QR.
- Mã OTP.
- Thông báo nhắc lịch.

SES giúp gửi Email nhanh chóng với chi phí thấp và khả năng mở rộng cao.

---

# Lợi ích của kiến trúc Event-Driven

Việc áp dụng Event-Driven Architecture mang lại nhiều lợi ích:

- Giảm sự phụ thuộc giữa các Microservices.
- Dễ dàng mở rộng hệ thống khi số lượng người dùng tăng.
- Tăng khả năng chịu lỗi.
- Đơn giản hóa việc bảo trì và nâng cấp.
- Xử lý bất đồng bộ hiệu quả.
- Tối ưu hiệu năng và tài nguyên hệ thống.

Kiến trúc này đặc biệt phù hợp với các ứng dụng Cloud Native triển khai trên AWS.

---

# Kết luận

Thông qua việc kết hợp Amazon EventBridge, AWS Lambda, Amazon SQS, Amazon SNS và Amazon SES, Smart Parking System có thể xử lý các sự kiện theo thời gian thực một cách linh hoạt và ổn định.

Kiến trúc Event-Driven không chỉ giúp giảm sự phụ thuộc giữa các Microservices mà còn nâng cao khả năng mở rộng, tính sẵn sàng và hiệu quả vận hành của toàn bộ hệ thống. Đây là nền tảng quan trọng để phát triển các ứng dụng bãi đỗ xe thông minh trên AWS theo hướng hiện đại và Cloud Native.