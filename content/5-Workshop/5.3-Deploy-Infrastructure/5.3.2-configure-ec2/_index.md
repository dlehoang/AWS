---
title : "Configure the EC2 Instance"
date : 2026-07-10
weight : 2
chapter : false
pre : " <b> 5.3.2 </b> "
---

In this section, you will configure the Amazon EC2 instance to prepare it for deploying the Smart Parking application.

The configuration includes updating the operating system, installing the required software packages, and verifying that the environment is ready for deployment.

## Connect to the EC2 Instance

1. Open the **Amazon EC2 Console**.

2. Select the **SmartParking** EC2 instance.

3. Click **Connect**.

![connect](/images/5-Workshop/5.3-Deploy-Infrastructure/connect.jpg)

4. Choose **EC2 Instance Connect** (or connect using SSH if preferred), then click **Connect**.

![instance-connect](/images/5-Workshop/5.3-Deploy-Infrastructure/instance-connect.jpg)

You are now connected to the EC2 instance.

---

## Update the Operating System

Run the following commands to update the system packages.

```bash
sudo apt update
sudo apt upgrade -y
```



---

## Install Required Packages

Install Git, .NET SDK, ASP.NET Core Runtime, and Nginx.

```bash
sudo apt install git -y
sudo apt install nginx -y
```

Install the .NET SDK.

```bash
sudo apt install dotnet-sdk-8.0 -y
```

Verify the installation.

```bash
dotnet --version
git --version
nginx -v
```



---

## Configure the Firewall

Allow HTTP and HTTPS traffic.

```bash
sudo ufw allow 80
sudo ufw allow 443
sudo ufw enable
```

Verify the firewall status.

```bash
sudo ufw status
```



---

## Verify the Environment

Confirm that all required software has been installed successfully.

```bash
dotnet --version
git --version
systemctl status nginx
```



---

## Section Summary

Congratulations! You have successfully configured the Amazon EC2 instance for the Smart Parking System.

The server is now ready for deploying the Smart Parking application in the next section.