---
title: "Proposal"
date: 2026-07-09
weight: 2
chapter: false
pre: " <b> 2. </b> "
---



This proposal presents the Smart Parking System built on Amazon Web Services (AWS). The platform leverages cloud-native and event-driven architecture to provide real-time parking management, online booking, IoT integration, and automated notifications.

# Smart Parking System on AWS
## Cloud-Native Smart Parking Management Platform

### 1. Executive Summary

The Smart Parking System is designed to help drivers quickly find available parking spaces, reserve parking slots, make online payments, and receive notifications in real time.

The platform adopts a Cloud-Native Microservices Architecture running on Amazon ECS with Event-Driven communication using Amazon EventBridge. IoT devices such as RFID readers, cameras, ESP32 sensors, and barrier gates continuously update parking status through AWS IoT Core.

The system is scalable, highly available, secure, and suitable for deployment in shopping malls, office buildings, hospitals, universities, and smart cities.

---

### 2. Problem Statement

### What's the Problem?

Traditional parking systems still rely heavily on manual management.

Common problems include:

- Drivers spend a long time searching for parking spaces.
- Parking availability is not updated in real time.
- Manual ticket management causes human errors.
- Payment processes are inconvenient.
- Administrators cannot effectively monitor parking occupancy.
- Difficult to expand to multiple parking locations.

### The Solution

The Smart Parking System utilizes AWS Cloud services to build a centralized parking management platform.

Key capabilities include:

- Real-time parking slot monitoring.
- Online parking reservation.
- QR Code generation.
- Online payment integration.
- IoT device integration.
- Automated email notifications.
- Event-driven microservices architecture.
- Highly scalable cloud infrastructure.

---

### Benefits and Return on Investment

The proposed solution offers:

- Reduced parking search time.
- Improved parking utilization.
- Lower operational costs.
- Automated parking management.
- Better customer experience.
- Easier maintenance through managed AWS services.
- Easy expansion to multiple parking locations.

The system primarily uses AWS Managed Services, minimizing infrastructure maintenance costs while supporting future business growth.

---

### 3. Solution Architecture

The platform follows a layered cloud architecture consisting of:

- Presentation Layer
- Application Layer
- Integration Layer
- IoT Layer
- Data Layer
- Security & Monitoring Layer

Architecture Diagram:

![Smart Parking Architecture](/images/2-Proposal/smart_parking_architecture.jpg)

---

### AWS Services Used

- Amazon Route 53
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
- Amazon CloudWatch
- AWS IAM
- AWS Secrets Manager
- AWS Certificate Manager

---

### Component Design

#### Presentation Layer

Users access the system through Web or Mobile applications.

Request Flow:

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

---

#### Application Layer

Backend services are deployed on Amazon ECS using Cloud-Native Microservices.

Main services include:

- Auth Service
- User Service
- Parking Service
- Booking Service
- Payment Service

The ECS Cluster is deployed inside a Private Subnet.

When external communication is required (VNPay, Google Maps API, third-party APIs), ECS accesses the Internet through:

Amazon ECS

↓

NAT Gateway

↓

Internet Gateway

↓

Internet

---

#### Integration Layer

The platform adopts Event-Driven Architecture.

Amazon EventBridge receives events from ECS services.

AWS Lambda performs background processing such as:

- QR Code generation
- Data processing
- Business workflows

Amazon SQS buffers asynchronous tasks.

Amazon SNS and Amazon SES deliver notifications to users.

---

#### IoT Layer

Parking devices include:

- RFID Reader
- Camera
- ESP32 Sensor
- Barrier Gate

Device data is transmitted to AWS IoT Core.

Parking Service updates parking slot status accordingly.

---

#### Data Layer

Amazon RDS stores:

- Users
- Parking Lots
- Reservations
- Payments
- Vehicles

Amazon S3 stores:

- QR Codes
- Vehicle Images
- Camera Snapshots
- Reports
- PDF Receipts

---

### Security Layer

The system uses:

- AWS IAM
- AWS Secrets Manager
- AWS Certificate Manager

IAM Roles are assigned directly to ECS Tasks to securely access AWS resources.

---

### Monitoring Layer

Amazon CloudWatch collects:

- Logs
- Metrics
- CPU
- Memory
- Alarms

CloudWatch provides centralized monitoring and alerting.

---

### 4. Technical Implementation

Implementation consists of four phases.

#### Phase 1

- Business analysis
- Requirement gathering
- Architecture design

#### Phase 2

- AWS infrastructure deployment
- Networking configuration
- ECS deployment
- Database configuration

#### Phase 3

Application development

- Authentication
- Parking Management
- Booking
- Payment
- Notification
- IoT Integration

#### Phase 4

Testing

- Functional Testing
- Integration Testing
- Load Testing
- Deployment

---

### Technical Requirements

Programming Languages

- Java Spring Boot / Node.js
- React / Flutter

Database

- Amazon RDS MySQL

Container

- Docker
- Amazon ECS

Infrastructure

- AWS Cloud

IoT Devices

- ESP32
- RFID Reader
- Camera
- Barrier Gate

---

### 5. Timeline & Milestones

Month 1

- Requirement Analysis
- AWS Architecture Design

Month 2

- Infrastructure Deployment
- Backend Development

Month 3

- Frontend Development
- IoT Integration
- Testing

Month 4

- Deployment
- Documentation
- Final Presentation

---

### 6. Budget Estimation

AWS resources mainly consist of managed services.

Estimated monthly services include:

- Amazon ECS
- Amazon RDS
- Amazon S3
- EventBridge
- Lambda
- SQS
- SNS
- SES
- CloudFront
- Route53
- CloudWatch

The estimated infrastructure cost remains below the AWS Educate promotional budget and can be optimized further through AWS Free Tier where applicable.

---

### 7. Risk Assessment

#### Risks

- Internet connectivity failure
- IoT device malfunction
- Unexpected AWS costs
- High traffic spikes

#### Mitigation

- CloudWatch monitoring
- Auto Scaling
- Budget Alerts
- Multi-AZ Database
- Event Queue with Amazon SQS

---

### 8. Expected Outcomes

Technical Outcomes

- Cloud-native Microservices platform
- Real-time parking monitoring
- Online reservation
- IoT integration
- Automated notifications
- Secure cloud infrastructure

Business Outcomes

- Reduced parking search time
- Better parking utilization
- Improved customer experience
- Lower operational costs
- Easy future expansion for Smart City applications