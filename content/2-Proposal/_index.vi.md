---
title: "Bản đề xuất"
date: 2026-07-09
weight: 2
chapter: false
pre: " <b> 2. </b> "
---



Tại phần này, nhóm trình bày đề xuất xây dựng hệ thống **Smart Parking System on AWS**, một nền tảng quản lý bãi đỗ xe thông minh ứng dụng các dịch vụ điện toán đám mây của Amazon Web Services.

# Smart Parking System on AWS
## Hệ thống quản lý bãi đỗ xe thông minh trên nền tảng AWS

### 1. Tóm tắt điều hành

Smart Parking System là hệ thống giúp quản lý bãi đỗ xe theo thời gian thực bằng cách kết hợp công nghệ IoT và điện toán đám mây AWS.

Người dùng có thể tìm kiếm vị trí còn trống, đặt chỗ trước, nhận mã QR, thanh toán trực tuyến và theo dõi trạng thái bãi xe thông qua Website hoặc Mobile App.

Hệ thống được xây dựng theo kiến trúc Cloud Native Microservices sử dụng Amazon ECS, Event-Driven Architecture và các dịch vụ Managed Services của AWS nhằm đảm bảo khả năng mở rộng, tính sẵn sàng cao, tăng khả năng chịu lỗi và tối ưu chi phí vận hành.

---

## 2. Tuyên bố vấn đề

### Vấn đề hiện tại

Hiện nay nhiều bãi giữ xe vẫn hoạt động theo hình thức thủ công:

- Khó theo dõi số lượng chỗ trống theo thời gian thực.
- Người dùng mất nhiều thời gian tìm chỗ đỗ.
- Thanh toán còn thủ công.
- Khó quản lý lưu lượng xe ra vào.
- Thiếu hệ thống cảnh báo và thống kê tập trung.

Điều này làm giảm trải nghiệm người dùng và gây khó khăn trong việc quản lý bãi xe.

### Giải pháp

Nhóm đề xuất xây dựng Smart Parking System trên nền tảng AWS.

Hệ thống sử dụng:

- Amazon ECS triển khai các Microservices.
- Amazon RDS lưu trữ dữ liệu.
- Amazon S3 lưu trữ hình ảnh và QR Code.
- AWS IoT Core tiếp nhận dữ liệu từ Camera, RFID, ESP32.
- Amazon EventBridge, Lambda, SQS, SNS và SES xử lý các sự kiện bất đồng bộ.
- Route53, CloudFront, WAF và Application Load Balancer tiếp nhận và phân phối lưu lượng truy cập.
- NAT Gateway cho phép các ECS Task trong Private Subnet truy cập Internet khi cần.

Hệ thống hỗ trợ:

- Quản lý bãi đỗ xe.
- Theo dõi Slot theo thời gian thực.
- Đặt chỗ.
- Thanh toán trực tuyến.
- Sinh QR Code.
- Gửi Email xác nhận.
- Giám sát toàn bộ hệ thống.

### Lợi ích và hiệu quả

Giải pháp mang lại:

- Giảm thời gian tìm chỗ đỗ xe.
- Tự động hóa quy trình quản lý.
- Hỗ trợ mở rộng quy mô bãi xe.
- Dễ dàng tích hợp AI nhận diện biển số xe trong tương lai.
- Giảm chi phí vận hành nhờ sử dụng các dịch vụ Managed Services của AWS.

---

## 3. Kiến trúc giải pháp

Hệ thống được xây dựng theo kiến trúc Cloud Native Microservices gồm các tầng:

- Presentation Layer
- Application Layer
- Integration Layer
- IoT Layer
- Data Layer
- Security & Monitoring Layer

Kiến trúc tổng thể như hình dưới đây:

![Smart Parking Architecture](/images/2-Proposal/smart_parking_architecture.png)

### Các dịch vụ AWS sử dụng

- Amazon Route53
- Amazon CloudFront
- AWS WAF
- Internet Gateway
- External Application Load Balancer
- Internal Application Load Balancer
- Amazon ECS
- Amazon EventBridge
- AWS Lambda
- Amazon SQS
- Amazon SNS
- Amazon SES
- AWS IoT Core
- Amazon RDS
- Amazon S3
- NAT Gateway
- AWS IAM
- AWS Secrets Manager
- AWS Certificate Manager
- Amazon CloudWatch

### Thiết kế thành phần

**Presentation Layer**

Tiếp nhận request từ Website hoặc Mobile App.

Luồng truy cập:

User

↓

Internet

↓

Amazon Route53

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

---

**Application Layer**

Amazon ECS triển khai các Microservices:

- Auth Service
- User Service
- Parking Service
- Booking Service
- Payment Service
- Notification Service

Các dịch vụ được triển khai trong Private Subnet để tăng cường bảo mật.

---

**Integration Layer**

Hệ thống sử dụng Event-Driven Architecture:

Booking Service

↓

Amazon EventBridge

↓

AWS Lambda

↓

Amazon SQS

↓

Amazon SNS

↓

Amazon SES

Giúp xử lý bất đồng bộ và giảm sự phụ thuộc giữa các Microservices.

---

**IoT Layer**

Các thiết bị:

- Camera
- RFID Reader
- ESP32
- Barrier Gate

gửi dữ liệu lên AWS IoT Core.

Parking Service sẽ đồng bộ trạng thái bãi xe từ AWS IoT Core.

---

**Data Layer**

Amazon RDS lưu trữ:

- Người dùng
- Đặt chỗ
- Thanh toán
- Thông tin bãi xe

Amazon S3 lưu:

- QR Code
- Hình ảnh phương tiện
- Hóa đơn
- File Log

---

**Security & Monitoring**

Sử dụng:

- AWS IAM
- Secrets Manager
- ACM
- CloudWatch

để quản lý quyền truy cập, lưu Secret, SSL/TLS và giám sát hệ thống.

---

## 4. Triển khai kỹ thuật

### Các giai đoạn triển khai

**Giai đoạn 1**

- Phân tích yêu cầu.
- Thiết kế kiến trúc AWS.
- Thiết kế cơ sở dữ liệu.
- Thiết kế Microservices.

**Giai đoạn 2**

- Tính toán chi phí bằng AWS Pricing Calculator.
- Điều chỉnh kiến trúc phù hợp ngân sách.

**Giai đoạn 3**

- Phát triển Backend.
- Triển khai Amazon ECS.
- Cấu hình ALB.
- Thiết lập EventBridge.
- Kết nối AWS IoT Core.
- Xây dựng Website.

**Giai đoạn 4**

- Kiểm thử.
- Triển khai.
- Giám sát bằng CloudWatch.

### Yêu cầu kỹ thuật

- Website hoặc Mobile App.
- Amazon ECS.
- Docker.
- Amazon RDS.
- Amazon S3.
- AWS IoT Core.
- Amazon EventBridge.
- AWS Lambda.
- Amazon SNS.
- Amazon SES.
- Amazon SQS.
- AWS IAM.
- CloudWatch.
- NAT Gateway.

---

## 5. Lộ trình và mốc triển khai

### Tháng 1

- Khảo sát yêu cầu.
- Thiết kế kiến trúc.
- Thiết kế Database.

### Tháng 2

- Phát triển Backend.
- Xây dựng Microservices.
- Cấu hình AWS.

### Tháng 3

- Tích hợp IoT.
- Kiểm thử.
- Triển khai.
- Hoàn thiện báo cáo.

---

## 6. Ước tính ngân sách

Chi phí được tính toán bằng AWS Pricing Calculator.

Các dịch vụ chính:

- Amazon ECS
- Application Load Balancer
- Amazon RDS
- Amazon S3
- AWS IoT Core
- EventBridge
- Lambda
- SQS
- SNS
- SES
- CloudWatch
- NAT Gateway

Chi phí thực tế phụ thuộc vào số lượng người dùng, số lượng thiết bị IoT và lưu lượng truy cập.

---

## 7. Đánh giá rủi ro

### Rủi ro

- Mất kết nối Internet.
- Thiết bị IoT gặp sự cố.
- Quá tải hệ thống.
- Chi phí AWS tăng ngoài dự kiến.

### Giải pháp

- ECS Auto Scaling.
- RDS Multi-AZ.
- Event-Driven Architecture.
- CloudWatch Alarm.
- AWS Budget.
- Backup dữ liệu định kỳ.

---

## 8. Kết quả kỳ vọng

### Về kỹ thuật

- Quản lý bãi xe theo thời gian thực.
- Tự động cập nhật trạng thái chỗ đỗ.
- Đặt chỗ trực tuyến.
- Thanh toán điện tử.
- Gửi Email tự động.
- Hệ thống dễ dàng mở rộng.

### Giá trị lâu dài

- Có thể tích hợp AI nhận diện biển số xe (ALPR).
- Phân tích dữ liệu bằng Machine Learning.
- Mở rộng nhiều bãi xe.
- Triển khai Multi-Region trong tương lai.
- Là nền tảng phục vụ nghiên cứu và phát triển các hệ thống Smart City.