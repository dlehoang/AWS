---
title: "Workshop"
date: 2026-07-10
weight: 5
chapter: false
pre: "<b> 5. </b>"
---

# Triển khai và bảo mật hệ thống Smart Parking trên AWS

#### Tổng quan

Trong workshop này, bạn sẽ triển khai và cấu hình hệ thống **Smart Parking** trên nền tảng AWS bằng các dịch vụ điện toán đám mây. Hệ thống cho phép người dùng tìm kiếm bãi đỗ xe còn chỗ, đặt chỗ trước, thanh toán trực tuyến và nhận thông báo theo thời gian thực.

Workshop cũng minh họa cách các dịch vụ của AWS phối hợp với nhau để xây dựng một hệ thống Smart Parking có khả năng mở rộng, tính sẵn sàng cao, bảo mật và dễ dàng giám sát.

Trong suốt workshop, bạn sẽ từng bước triển khai hạ tầng, cấu hình mạng, kết nối cơ sở dữ liệu, tích hợp lưu trữ, triển khai ứng dụng và giám sát hệ thống bằng các dịch vụ của AWS.

#### Các thành phần kiến trúc

Hệ thống Smart Parking sử dụng các dịch vụ AWS sau:

+ **Amazon VPC** - Tạo môi trường mạng riêng biệt và an toàn cho toàn bộ hệ thống.
+ **Amazon ECS (Fargate)** - Triển khai và vận hành các dịch vụ (microservices) của Smart Parking.
+ **Application Load Balancer (ALB)** - Phân phối lưu lượng truy cập đến các dịch vụ backend.
+ **Amazon RDS MySQL** - Lưu trữ dữ liệu người dùng, bãi đỗ xe, đặt chỗ và thanh toán.
+ **Amazon S3** - Lưu trữ hình ảnh bãi xe, mã QR và các tệp tin của hệ thống.
+ **AWS Lambda** - Xử lý các tác vụ tự động theo mô hình serverless.
+ **Amazon SNS / Amazon SES** - Gửi thông báo và email xác nhận đến người dùng.
+ **Amazon CloudWatch** - Thu thập log, giám sát hiệu năng và theo dõi hoạt động của hệ thống.
+ **AWS IAM** - Quản lý người dùng, quyền truy cập và bảo mật tài nguyên.
+ **AWS Secrets Manager** - Lưu trữ an toàn thông tin đăng nhập và các khóa bí mật.

#### Nội dung

1. [Tổng quan Workshop](5.1-Workshop-overview/)
2. [Chuẩn bị môi trường](5.2-Prerequiste/)
3. [Triển khai hạ tầng Smart Parking](5.3-Deploy-Infrastructure/)
4. [Dọn dẹp tài nguyên](5.4-Cleanup/)