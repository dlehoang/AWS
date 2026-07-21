---
title : "Prerequisites"
date : 2026-07-10
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

## Điều kiện chuẩn bị

Trước khi triển khai hệ thống Smart Parking, hãy đảm bảo bạn đã chuẩn bị đầy đủ các yêu cầu dưới đây.

### Tài khoản AWS

Bạn cần có một tài khoản AWS đang hoạt động và có đủ quyền để tạo cũng như quản lý các tài nguyên AWS.

Các dịch vụ AWS sẽ được sử dụng trong workshop này bao gồm:

+ Amazon VPC
+ Amazon ECS (Fargate)
+ Amazon ECR
+ Application Load Balancer
+ Amazon RDS MySQL
+ Amazon S3
+ AWS Lambda
+ Amazon CloudWatch
+ AWS IAM
+ AWS Secrets Manager
+ Amazon SNS
+ Amazon SES

---

### Quyền IAM

Tài khoản AWS hoặc IAM User của bạn cần có quyền tạo và quản lý các tài nguyên phục vụ cho workshop, bao gồm:

+ Amazon VPC
+ Amazon ECS
+ Amazon ECR
+ Amazon RDS
+ Amazon S3
+ AWS Lambda
+ Amazon CloudWatch
+ AWS IAM
+ AWS Secrets Manager
+ Amazon SNS
+ Amazon SES

Để thuận tiện trong quá trình thực hành, bạn nên sử dụng IAM User được gán quyền **AdministratorAccess**.

---

### Môi trường phát triển

Trước khi triển khai hệ thống, hãy cài đặt các công cụ sau:

+ Visual Studio 2022
+ .NET 8 SDK
+ Docker Desktop
+ Git
+ AWS CLI
+ AWS Toolkit for Visual Studio (Tùy chọn)

Kiểm tra quá trình cài đặt bằng các lệnh sau:

```bash
dotnet --version
docker --version
aws --version
git --version
```

---

### Mã nguồn

Sao chép (clone) mã nguồn Smart Parking từ GitHub:

```bash
git clone https://github.com/<your-repository>/SmartParking.git
cd SmartParking
```

---

### Khu vực triển khai AWS

Workshop này sử dụng Region **Asia Pacific (Singapore) - ap-southeast-1**.

Bạn có thể sử dụng Region khác nếu cần, tuy nhiên tất cả các dịch vụ phải được triển khai trong cùng một Region.

---

### Chuẩn bị kiến trúc hệ thống

Trước khi bắt đầu triển khai, hãy đảm bảo kiến trúc của hệ thống đã được thiết kế với các thành phần sau:

+ Amazon VPC
+ Public Subnet và Private Subnet
+ Internet Gateway
+ Application Load Balancer
+ Amazon ECS Cluster
+ Amazon RDS MySQL
+ Amazon S3 Bucket
+ AWS Lambda
+ Amazon CloudWatch

Sau khi hoàn thành các bước chuẩn bị trên, bạn đã sẵn sàng triển khai hạ tầng Smart Parking trong phần tiếp theo.

![prerequisite](/images/5-Workshop/5.2-Prerequisite/w2.jpg)