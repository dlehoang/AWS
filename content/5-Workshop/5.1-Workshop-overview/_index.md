---
title : "Introduction"
date : 2026-07-10
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

#### Smart Parking System

+ **Smart Parking System** is a cloud-native parking management solution deployed on AWS. It enables users to search for available parking spaces, reserve parking slots, make online payments, and receive real-time notifications.
+ The system is built using AWS services to provide scalability, high availability, security, and efficient resource management through a microservices architecture.

#### Workshop Overview

In this workshop, you will deploy a Smart Parking System on AWS using a secure and scalable architecture.

The architecture consists of the following components:

+ **Amazon VPC** provides an isolated and secure networking environment for the application.
+ **Application Load Balancer (ALB)** distributes incoming requests across backend services.
+ **Amazon ECS (Fargate)** hosts the Smart Parking microservices, including Authentication, User, Parking, Booking, Payment, and Notification services.
+ **Amazon RDS MySQL** stores application data such as users, parking lots, reservations, and payment records.
+ **Amazon S3** stores parking images, QR codes, and uploaded files.
+ **AWS Lambda**, **Amazon SNS**, and **Amazon SES** handle serverless processing and user notifications.
+ **Amazon CloudWatch** monitors system performance, collects logs, and provides operational insights.
+ **AWS IAM** and **AWS Secrets Manager** ensure secure access control and protect sensitive credentials.

During this workshop, you will provision the required AWS infrastructure, deploy the Smart Parking application, configure the necessary services, and validate that the entire system operates correctly.

![overview](/images/5-Workshop/5.1-Workshop-overview/w1.jpg)