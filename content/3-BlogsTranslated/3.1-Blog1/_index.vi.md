---
title: "Blog 1"
date: 2026-07-09
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---



# Thiết kế hệ thống Smart Parking trên AWS theo kiến trúc Cloud Native Microservices

Sự phát triển của các đô thị thông minh kéo theo nhu cầu quản lý bãi đỗ xe ngày càng hiệu quả. Tuy nhiên, nhiều bãi đỗ xe hiện nay vẫn hoạt động theo phương thức truyền thống, khiến việc tìm kiếm chỗ đỗ, quản lý phương tiện và theo dõi trạng thái bãi xe gặp nhiều khó khăn.

Trong bài viết này, nhóm sẽ giới thiệu kiến trúc tổng thể của hệ thống **Smart Parking System** được triển khai trên nền tảng Amazon Web Services (AWS) theo mô hình **Cloud Native Microservices**, giúp hệ thống dễ dàng mở rộng, đảm bảo tính sẵn sàng cao và tăng khả năng tự động hóa.

---

## Tổng quan bài toán

Hiện nay, việc quản lý bãi đỗ xe theo phương pháp thủ công tồn tại nhiều hạn chế như:

- Người dùng mất nhiều thời gian tìm chỗ đỗ xe.
- Không thể theo dõi số lượng vị trí còn trống theo thời gian thực.
- Quy trình đặt chỗ và thanh toán còn thủ công.
- Khó mở rộng khi số lượng bãi xe hoặc người dùng tăng lên.
- Thiếu hệ thống giám sát và cảnh báo tập trung.

Để giải quyết những vấn đề trên, nhóm xây dựng hệ thống Smart Parking dựa trên các dịch vụ Managed Services của AWS nhằm tăng khả năng mở rộng, giảm chi phí quản trị hạ tầng và nâng cao trải nghiệm người dùng.

---

## Kiến trúc tổng thể

Hệ thống được chia thành 6 lớp chính:

- Presentation Layer
- Application Layer
- Integration Layer
- IoT Layer
- Data Layer
- Security & Monitoring Layer

Việc phân chia theo từng lớp giúp hệ thống dễ quản lý, dễ bảo trì và thuận tiện khi mở rộng thêm chức năng trong tương lai.

---

## Presentation Layer

Đây là lớp tiếp nhận toàn bộ yêu cầu từ người dùng.

Luồng truy cập của hệ thống như sau:

User

↓

Internet

↓

Amazon Route 53

↓

Amazon CloudFront

↓

AWS WAF

↓

Internet Gateway

↓

External Application Load Balancer

↓

Internal Application Load Balancer

↓

Amazon ECS Cluster

Trong đó:

- **Amazon Route 53** thực hiện phân giải tên miền (DNS Resolution).
- **Amazon CloudFront** tăng tốc truy cập bằng cách cache nội dung tĩnh.
- **AWS WAF** bảo vệ hệ thống khỏi các cuộc tấn công như SQL Injection, XSS và Bot Traffic.
- **External Application Load Balancer** tiếp nhận lưu lượng truy cập từ Internet.
- **Internal Application Load Balancer** phân phối request đến các Microservices bên trong Amazon ECS Cluster.

---

## Application Layer

Toàn bộ Backend của hệ thống được triển khai trên **Amazon ECS (Elastic Container Service)** theo kiến trúc Microservices.

Amazon ECS Cluster bao gồm nhiều dịch vụ độc lập như:

- Auth Service
- User Service
- Parking Service
- Booking Service
- Payment Service
- Notification Service

Mỗi Microservice đảm nhận một chức năng riêng biệt, giúp việc phát triển, triển khai và mở rộng trở nên đơn giản hơn.

Ngoài việc xử lý request từ Internal Application Load Balancer, các ECS Task còn có thể truy cập Internet thông qua **NAT Gateway** để gọi các API bên ngoài như Google Maps, VNPay hoặc Stripe.

---

## Integration Layer

Để giảm sự phụ thuộc giữa các Microservices, hệ thống sử dụng mô hình **Event-Driven Architecture**.

Các dịch vụ AWS được sử dụng bao gồm:

- Amazon EventBridge
- AWS Lambda
- Amazon SQS
- Amazon SNS
- Amazon SES

Ví dụ, khi người dùng đặt chỗ thành công:

Booking Service

↓

Amazon EventBridge

↓

AWS Lambda

↓

Amazon SNS

↓

Amazon SES

Thông qua mô hình này, các Microservices không cần giao tiếp trực tiếp với nhau mà chỉ cần phát sinh và lắng nghe các sự kiện, giúp hệ thống dễ mở rộng và tăng khả năng chịu tải.

---

## IoT Layer

Hệ thống tích hợp các thiết bị IoT tại bãi đỗ xe như:

- Camera
- RFID Reader
- ESP32
- Barrier Gate

Các thiết bị này gửi dữ liệu theo thời gian thực lên **AWS IoT Core**.

Parking Service sẽ nhận dữ liệu từ AWS IoT Core để cập nhật trạng thái các vị trí đỗ xe trong hệ thống.

---

## Data Layer

Hệ thống sử dụng hai dịch vụ lưu trữ chính:

### Amazon RDS

Lưu trữ các dữ liệu quan hệ như:

- Người dùng
- Thông tin phương tiện
- Thông tin bãi xe
- Đặt chỗ
- Thanh toán

### Amazon S3

Lưu trữ:

- QR Code
- Hình ảnh phương tiện
- Ảnh từ Camera
- Hóa đơn
- Nhật ký hệ thống (Log)

---

## Security & Monitoring Layer

Để đảm bảo hệ thống hoạt động ổn định và an toàn, nhóm sử dụng các dịch vụ:

- AWS IAM để quản lý quyền truy cập.
- AWS Secrets Manager để lưu trữ thông tin nhạy cảm.
- AWS Certificate Manager (ACM) để quản lý chứng chỉ SSL/TLS.
- Amazon CloudWatch để thu thập Logs, Metrics và giám sát toàn bộ hệ thống.

---

## Lợi ích của kiến trúc

Kiến trúc Smart Parking trên AWS mang lại nhiều lợi ích:

- Dễ dàng mở rộng khi số lượng người dùng tăng.
- Các Microservices hoạt động độc lập, thuận tiện bảo trì.
- Tăng khả năng chịu lỗi nhờ Event-Driven Architecture.
- Bảo mật cao với IAM, WAF và Secrets Manager.
- Giảm chi phí vận hành nhờ sử dụng các dịch vụ Managed Services của AWS.
- Dễ dàng tích hợp thêm AI nhận diện biển số xe hoặc Machine Learning trong tương lai.

---

## Kết luận

Việc kết hợp Amazon ECS, EventBridge, Lambda, Amazon RDS, Amazon S3, AWS IoT Core và các dịch vụ bảo mật của AWS đã tạo nên một kiến trúc Cloud Native hiện đại cho hệ thống Smart Parking.

Kiến trúc này không chỉ đáp ứng nhu cầu quản lý bãi đỗ xe theo thời gian thực mà còn tạo nền tảng để mở rộng thêm nhiều tính năng thông minh trong tương lai.

Ở bài viết tiếp theo, nhóm sẽ trình bày chi tiết cách triển khai các Microservices trên Amazon ECS, cơ chế cân bằng tải thông qua External và Internal Application Load Balancer cũng như phương pháp triển khai hệ thống theo mô hình Container.