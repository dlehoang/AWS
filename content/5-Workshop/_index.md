---
title: "Workshop"
date: 2026-07-10
weight: 5
chapter: false
pre: "<b> 5. </b>"
---

# Deploy and Secure Smart Parking System on AWS

#### Overview

In this workshop, you will deploy and configure a Smart Parking System on AWS using cloud-native services. The system enables users to search for available parking spaces, make reservations, process payments, and receive notifications in real time.

The workshop also demonstrates how AWS networking, security, storage, and monitoring services work together to build a scalable, secure, and highly available Smart Parking platform.

Throughout this workshop, you will deploy backend services, configure networking, connect databases, integrate storage, and monitor the system using AWS services.

#### Architecture Components

The Smart Parking System includes the following AWS services:

+ **Amazon VPC** - Provides an isolated network environment for the application.
+ **Amazon ECS (Fargate)** - Hosts Smart Parking microservices.
+ **Application Load Balancer (ALB)** - Distributes incoming traffic to backend services.
+ **Amazon RDS MySQL** - Stores users, parking lots, bookings, and payment information.
+ **Amazon S3** - Stores QR codes, parking images, and uploaded files.
+ **AWS Lambda** - Processes serverless business logic.
+ **Amazon SNS / SES** - Sends notifications and confirmation emails.
+ **Amazon CloudWatch** - Collects logs and monitors application performance.
+ **AWS IAM** - Controls access permissions.
+ **AWS Secrets Manager** - Stores database credentials securely.

#### Content

1. [Workshop Overview](5.1-Workshop-overview/)
2. [Prerequisites](5.2-Prerequiste/)
3. [Deploy Smart Parking Infrastructure](5.3-Deploy-Infrastructure/)
4. [Clean up](5.4-Cleanup/)