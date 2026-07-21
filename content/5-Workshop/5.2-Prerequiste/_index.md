---
title : "Prerequisites"
date : 2026-07-10
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

## Prerequisites

Before deploying the Smart Parking System, ensure that the following requirements are completed.

### AWS Account

You need an active AWS account with sufficient permissions to create and manage AWS resources.

The following AWS services will be used throughout this workshop:

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

### Required IAM Permissions

Your AWS account (or IAM user) should have permissions to create and manage the resources required for this workshop, including:

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

It is recommended to use an IAM user with **AdministratorAccess** for the workshop environment.

---

### Development Environment

Prepare the following tools before deployment.

+ Visual Studio 2022
+ .NET 8 SDK
+ Docker Desktop
+ Git
+ AWS CLI
+ AWS Toolkit for Visual Studio (Optional)

Verify the installation by running:

```bash
dotnet --version
docker --version
aws --version
git --version
```

---

### Source Code

Clone the Smart Parking project from GitHub.

```bash
git clone https://github.com/<your-repository>/SmartParking.git
cd SmartParking
```

---

### AWS Region

This workshop uses the **Asia Pacific (Singapore) - ap-southeast-1** Region.

You may choose another AWS Region, but all services should be deployed within the same Region.

---

### Architecture Preparation

Before starting the deployment, verify that the following architecture has been prepared.

+ Amazon VPC
+ Public and Private Subnets
+ Internet Gateway
+ Application Load Balancer
+ Amazon ECS Cluster
+ Amazon RDS MySQL
+ Amazon S3 Bucket
+ AWS Lambda
+ Amazon CloudWatch

After completing the prerequisites, you are ready to deploy the Smart Parking infrastructure in the next section.

![prerequisite](/images/5-Workshop/5.2-Prerequisite/w2.jpg)