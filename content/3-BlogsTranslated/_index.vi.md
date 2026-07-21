---
title: "Các Blog Đã Dịch"
date: 2026-07-09
weight: 3
chapter: false
pre: " <b> 3. </b> "
---



Trong phần này, nhóm sẽ giới thiệu các bài blog được xây dựng dựa trên chủ đề **Smart Parking System on AWS**. Mỗi bài tập trung vào một thành phần quan trọng của hệ thống, giúp người đọc hiểu rõ kiến trúc, quy trình triển khai và cách các dịch vụ AWS phối hợp để xây dựng một hệ thống quản lý bãi đỗ xe thông minh.

### [Blog 1 - Tổng quan kiến trúc Smart Parking System trên AWS](3.1-Blog1/)

Bài viết giới thiệu kiến trúc tổng thể của hệ thống Smart Parking System được xây dựng trên nền tảng AWS. Nội dung trình bày các lớp kiến trúc của hệ thống, luồng xử lý request từ người dùng, mô hình Microservices trên Amazon ECS, cùng vai trò của Route 53, CloudFront, AWS WAF, Application Load Balancer và các dịch vụ lưu trữ như Amazon RDS và Amazon S3.

---

### [Blog 2 - Thiết kế Microservices và Event-Driven Architecture](3.2-Blog2/)

Bài viết trình bày cách hệ thống được xây dựng theo kiến trúc Microservices nhằm tách biệt các chức năng như xác thực người dùng, quản lý bãi xe, đặt chỗ, thanh toán và gửi thông báo. Đồng thời giới thiệu mô hình Event-Driven Architecture sử dụng Amazon EventBridge, AWS Lambda và Amazon SQS để xử lý các tác vụ bất đồng bộ, giúp hệ thống dễ mở rộng và tăng khả năng chịu tải.

---

### [Blog 3 - Thiết kế mạng AWS và bảo mật hệ thống](3.3-Blog3/)

Bài viết giới thiệu mô hình mạng triển khai trên AWS với VPC, Public Subnet, Private Subnet, Internet Gateway và NAT Gateway. Nội dung cũng trình bày cách sử dụng External Application Load Balancer và Internal Application Load Balancer để bảo vệ hệ thống Backend, đồng thời kết hợp AWS IAM, AWS Secrets Manager, AWS Certificate Manager và AWS WAF nhằm tăng cường tính bảo mật cho toàn bộ hệ thống.



