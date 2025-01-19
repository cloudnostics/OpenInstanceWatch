# OpenInstanceWatch
Open Source Instance Watch Daily Report

Receive an email once a day with a list of all your EC2 and RDS instances in all regions.

## Architecture

The architecture of the solution is based on the following components:
* Lambda function to list all EC2 and RDS instances in all regions, currently a python function using the python v3.13 runtime.
* Lambda execution role.
* An SNS topic to send the list of instances to the subscribers
* Scheduled EventBridge Event Rule to trigger the Lambda function once a day

## Installation

Deploy the CloudFormation template

You will receive an email asking to confirm you subscription to the SNS topic.

Some email providers such as Google Gmail may automatically unsubscribe you from the SNS topic. To avoid this **DO NOT** click on the **confirm subscription** link the email.

Instead follow these steps:

* Copy the URL from the Confirm subscription link in the email.
* Go to SNS in the AWS console.
* In the navigation pane of the console, choose Subscriptions.
* On the Subscriptions page, select the subscription that's **Pending confirmation** and then choose **Confirm subscription**.
* In the Confirm subscription dialog, paste the subscription confirmation URL that you copied.
* Choose Confirm subscription.

Once you confirm the subscription, you will start receiving the daily email with the list of all your EC2 and RDS instances in all regions.

Each day you will receive an email with the list of all your EC2 and RDS instances in all regions.

The Subject of the email wil be in the format of 

**YYYY-MM-DD OpenInstanceWatch Daily Report for AWS Account 999999999999**

The body of the email will contain a list of all your EC2 and RDS instances in all regions.
Similar to the following example:

```
Summary
|  Total EC2  |  Total RDS  |  Regions Scanned  |
| ----------- | ----------- | ----------------- |
|      1      |      0      |         17        |

EC2 Instances
|    Region   |       InstanceId      |  InstanceType  |   State   |
| ----------- | --------------------- | -------------- | --------- |
|  eu-west-2  |  i-08000000000000000  |   t3.medium    |  stopped  |

RDS Instances
No instances found.
```

Copyright (c) 2024 Dean Layton-James