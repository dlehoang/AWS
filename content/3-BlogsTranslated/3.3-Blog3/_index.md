---
title: "Blog 3"
date: 2026-07-09
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---



# Building an Event-Driven Smart Parking System on AWS

As the number of vehicles increases in modern cities, a smart parking platform must process thousands of parking events quickly and reliably. Traditional synchronous communication between services can easily become a bottleneck when traffic suddenly increases.

To address this challenge, the Smart Parking System adopts an **Event-Driven Architecture (EDA)** using AWS managed services. This architecture enables each microservice to communicate asynchronously, improving scalability, fault tolerance, and maintainability.

---

## Why Event-Driven Architecture?

In a traditional monolithic application, one service often depends directly on another. For example, after a booking is created, the Booking Service must immediately call the Payment Service and Notification Service.

This approach introduces several disadvantages:

- Tight coupling between services.
- Poor scalability.
- Higher latency.
- Difficult maintenance.

Instead, the Smart Parking System publishes events whenever an important action occurs. Other services subscribe to these events and process them independently.

---

## Event Flow in Smart Parking System

The event workflow is designed as follows:

1. A user reserves a parking slot.
2. Booking Service stores booking information in Amazon RDS.
3. Booking Service publishes a **BookingCreated** event to Amazon EventBridge.
4. EventBridge routes the event to the appropriate services.
5. AWS Lambda executes background processing.
6. Notification Service sends confirmation emails using Amazon SES.
7. Payment Service prepares payment information.
8. Parking Service updates parking slot status.

Each service performs only its own responsibility without directly depending on other services.

---

## AWS Services Used

The Integration Layer uses several AWS managed services.

### Amazon EventBridge

Amazon EventBridge acts as the central event bus of the system.

Its responsibilities include:

- Receiving events from microservices.
- Filtering events based on rules.
- Routing events to the correct targets.
- Decoupling communication between services.

Example events include:

- BookingCreated
- BookingCancelled
- PaymentCompleted
- ParkingOccupied
- ParkingReleased

---

### AWS Lambda

AWS Lambda executes serverless background tasks.

Typical responsibilities include:

- Generating QR Codes.
- Processing booking events.
- Updating parking status.
- Triggering notification workflows.
- Calling third-party APIs when necessary.

Since Lambda is fully managed, there is no need to provision or manage servers.

---

### Amazon SQS

Amazon Simple Queue Service (SQS) improves system reliability by buffering asynchronous requests.

Benefits include:

- Preventing traffic spikes.
- Ensuring reliable message delivery.
- Reducing pressure on backend services.
- Supporting automatic retries.

For example, if thousands of users reserve parking simultaneously, requests are temporarily stored in SQS and processed gradually.

---

### Amazon SNS

Amazon Simple Notification Service (SNS) distributes notifications to multiple subscribers simultaneously.

Typical notification scenarios include:

- Booking confirmation.
- Payment success.
- Parking expiration reminder.
- System announcements.

SNS allows one event to notify multiple systems at the same time.

---

### Amazon SES

Amazon Simple Email Service (SES) is responsible for email delivery.

The Smart Parking System uses SES to send:

- Booking confirmation.
- Payment receipt.
- QR Code.
- OTP verification.
- Reservation reminder.

---

## Advantages of Event-Driven Architecture

Compared with synchronous communication, the Event-Driven model provides several advantages:

- Loose coupling between microservices.
- Better scalability.
- Higher fault tolerance.
- Easier maintenance.
- Faster feature development.
- More reliable asynchronous processing.

Each service can evolve independently without affecting the rest of the system.

---

## Conclusion

Using Amazon EventBridge, AWS Lambda, Amazon SQS, Amazon SNS, and Amazon SES allows the Smart Parking System to process events efficiently while maintaining a loosely coupled architecture.

This event-driven approach significantly improves system scalability, reliability, and operational efficiency, making it suitable for modern cloud-native smart parking applications deployed on AWS.