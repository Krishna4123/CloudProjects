# Serverless File Processing Workflow with Lambda and SNS

## Overview

This project demonstrates a fully event-driven, serverless notification system on AWS. It automates real-time alerts whenever a file is uploaded to an S3 bucket by chaining S3, AWS Lambda, and Amazon SNS together — requiring zero server management.

The workflow is simple: **S3 Upload → Lambda Execution → SNS Notification**

---

## Architecture

```
S3 Bucket (pranav2109)
        |
        | ObjectCreated event
        ▼
AWS Lambda (s3lambda)
        |
        | Publish message
        ▼
Amazon SNS → Email Notification
```

---

## Core Components

### Lambda Function
- Function name: `s3lambda`
- Region: `us-east-1` (N. Virginia)
- ARN: `arn:aws:lambda:us-east-1:245140949754:function:s3lambda`

### S3 Trigger
- Bucket name: `pranav2109`
- Trigger event: `ObjectCreated:Put`
- Test event: file `files.txt` (size: 19 bytes) uploaded at `2025-08-08T08:27:12.434Z`

### IAM Role
- Role name: `s3lambda-role-d4j8kei3`
- Attached policy: `AWSLambdaBasicExecutionRole-4172e759...`
- Grants the Lambda function least-privilege access to execute and interact with SNS

### SNS Notification
- Trigger: Lambda publishes to an SNS topic on each S3 upload
- Email subject: `New S3 Upload Detected`
- Subscriber: confirmed email recipient
- Lambda response: `statusCode: 200` on successful execution

---

## Key Features

- **Event-Driven** — Automatically triggers on every S3 file upload with no manual intervention.
- **Serverless** — No EC2 instances to manage; Lambda handles all compute.
- **Real-Time Alerts** — SNS delivers email notifications instantly upon file upload.
- **Least-Privilege IAM** — The Lambda role is scoped to only the permissions it needs.

---

## Screenshots

![Screenshot 1](Screenshot%20(247).png)
![Screenshot 2](Screenshot%20(248).png)
![Screenshot 3](Screenshot%20(249).png)
![Screenshot 4](Screenshot%20(250).png)
![Screenshot 5](Screenshot%20(251).png)
