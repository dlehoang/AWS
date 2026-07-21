---
title : "Deploy the Smart Parking Application"
date : 2026-07-10
weight : 3
chapter : false
pre : " <b> 5.3.3 </b> "
---

In this section, you will deploy the Smart Parking application to the Amazon EC2 instance.

The deployment process includes transferring the application files, running the application, and verifying that the Smart Parking system is accessible through the EC2 public IP address.

## Upload the Application

1. Copy the published Smart Parking application to the EC2 instance.

You can use **SCP**, **WinSCP**, or any preferred file transfer tool.

![upload](/images/5-Workshop/5.3-Deploy-Infrastructure/upload.jpg)

---

## Publish the Application

If the application has not been published yet, execute the following command from the project directory.

```bash
dotnet publish -c Release -o publish
```

After publishing, upload the generated **publish** folder to the EC2 instance.

![publish](/images/5-Workshop/5.3-Deploy-Infrastructure/publish.jpg)

---

## Run the Application

Navigate to the published folder.

```bash
cd publish
```

Start the Smart Parking application.

```bash
dotnet SmartParking.dll
```

If the application starts successfully, the console displays a message similar to the following:

```text
Now listening on: http://localhost:5000
Application started.
```

![run](/images/5-Workshop/5.3-Deploy-Infrastructure/run.jpg)

---

## Verify the Deployment

Open a web browser.

Enter the public IP address of the EC2 instance.

```
http://<EC2-Public-IP>:5000
```

If the deployment is successful, the Smart Parking application home page will be displayed.

![homepage](/images/5-Workshop/5.3-Deploy-Infrastructure/homepage.jpg)

---

## Section Summary

Congratulations!

You have successfully deployed the Smart Parking application on Amazon EC2.

The application is now running and ready for database configuration and additional AWS service integration in the following sections.