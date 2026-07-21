---
title : "Clean Up"
date : 2026-07-10
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

Congratulations on completing this workshop!

In this workshop, you successfully deployed the Smart Parking System on AWS. You launched an Amazon EC2 instance, configured the deployment environment, deployed the Smart Parking application, connected it to an Amazon RDS database, and monitored the system using AWS services.

To avoid unnecessary AWS charges, make sure to delete all resources created during this workshop.

## Clean Up

### 1. Terminate the Amazon EC2 Instance

1. Open the **Amazon EC2 Console**.
2. Select the **SmartParking** EC2 instance.
3. Choose **Instance state** → **Terminate instance**.
4. Confirm the termination.

![terminate-ec2](/images/5-Workshop/5.4-Cleanup/terminate-ec2.jpg)
![terminate-ec2](/images/5-Workshop/5.4-Cleanup/terminate-ec21.jpg)

---

### 2. Delete the Amazon RDS Database

1. Open the **Amazon RDS Console**.
2. Select the Smart Parking database instance.
3. Click **Delete**.
4. Disable the **Create final snapshot** option if a backup is not required.
5. Confirm the deletion.

![delete-rds](/images/5-Workshop/5.4-Cleanup/delete-rds.jpg)

---

### 3. Verify Resource Cleanup

Return to the AWS Management Console and verify that all resources created during this workshop have been removed successfully.

Congratulations! You have successfully completed the Smart Parking Workshop and cleaned up all AWS resources.