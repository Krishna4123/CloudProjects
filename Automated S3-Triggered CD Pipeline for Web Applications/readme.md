# Automated S3-Triggered CD Pipeline for Web Applications

## Overview

This project demonstrates a modern cloud deployment of a Java web application using AWS Elastic Beanstalk as a PaaS solution, with S3 for artifact storage and an automated SNS notification system that triggers on deployment updates. It also integrates CloudWatch for logging and monitoring.

---

## Architecture

```
WebApp.war (local)
        |
        | aws s3 cp
        ▼
S3 Bucket (elastic1234567890s31234567890)
        |
        | ObjectCreated:Put event
        ▼
Elastic Beanstalk (sampleapp1.ap-south-1.elasticbeanstalk.com)
        |
        | S3 event notification
        ▼
Amazon SNS (webapp topic) → Email Notification
```

---

## Core Components

### Networking (VPC)
- VPC name: `my-vpc` (`vpc-087670d5fe77e9ba0`)
- CIDR block: `10.0.0.0/16`
- Subnets:
  - `my-public-subnet-1` — `ap-south-1b`
  - `my-public-subnet-2` — `ap-south-1c`

### Application Deployment (Elastic Beanstalk)
- Artifact: `WebApp.war` (Java web application)
- Upload command:
  ```bash
  aws s3 cp WebApp.war s3://elastic1234567890s31234567890/
  ```
- Deployed URL: `sampleapp1.ap-south-1.elasticbeanstalk.com`
- App content: "Welcome to MyDevOps" — includes sections on DevOps, Jenkins, and Maven

### S3 Artifact Bucket
- User upload bucket: `elastic1234567890s31234567890`
- Elastic Beanstalk source bucket: `elasticbeanstalk-ap-south-1-538712952108`
- Trigger event: `ObjectCreated:Put` on `.war` file upload

### Notifications (SNS)
- Topic name: `webapp`
- Subscriber: confirmed email subscription
- Trigger: S3 `ObjectCreated:Put` event on the Beanstalk source bucket
- Delivers AWS notification email on each deployment update

### Logging (CloudWatch)
- Log group: `/aws/lambda/sample-test`
- Region: `ap-south-1` (Asia Pacific - Mumbai)
- Contains log streams from a Lambda function involved in processing or monitoring S3 events

---

## Key Features

- **PaaS Deployment** — Elastic Beanstalk abstracts infrastructure management for the Java application.
- **Automated CD Pipeline** — Uploading a new `.war` to S3 triggers the full deployment and notification flow.
- **Event-Driven Notifications** — SNS delivers real-time email alerts on every deployment update.
- **Isolated Networking** — Custom VPC with public subnets across multiple availability zones for resilience.
- **Observability** — CloudWatch log groups capture Lambda execution logs for monitoring and debugging.

---

## Screenshots

![Screenshot 1](Screenshot%20(4).png)
![Screenshot 2](Screenshot%20(5).png)
![Screenshot 3](Screenshot%20(6).png)
![Screenshot 4](Screenshot%20(7).png)
![Screenshot 5](Screenshot%20(9).png)
![Screenshot 6](Screenshot%20(10).png)
![Screenshot 7](Screenshot%202025-08-11%20131806.png)
