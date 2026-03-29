# Hybrid Cloud Architecture: Flask, RDS & Lambda

## Overview

This project demonstrates a decoupled, event-driven architecture for a file-sharing application hosted on AWS. It integrates a Flask web backend with managed database services, serverless compute, and automated notification systems to provide a scalable and secure user experience.

---

## Architecture Diagram

![Architecture Overview](Screenshot%20(24).png)

---

## Core Components

### Web Server (EC2)
A `t3.micro` instance running Ubuntu 22.04 LTS hosts the Flask application. The server is managed via Gunicorn and systemd for high availability.

### Storage (S3 & EBS)
Amazon S3 is used for persistent object storage of shared files, while Amazon EBS provides block storage for the application code and OS.

### Database (RDS)
A managed PostgreSQL instance (`db.t4g.micro`) stores user credentials, file metadata, and application state within a private subnet.

### Serverless Logic (Lambda)
An AWS Lambda function (`generate-download-link`) automatically generates time-limited, secure pre-signed URLs for file access.

### Notifications (SNS)
Amazon SNS sends real-time email alerts to users, such as registration confirmations or file-ready notifications.

### Networking (VPC)
A custom VPC (`file-share-vpc`) provides network isolation, utilizing public subnets for the web server and private subnets for the database to ensure security.

### Security (IAM)
Granular IAM policies (`LambdaPolicy-FileShare`) grant the EC2 and Lambda instances the least-privilege access required to interact with S3 and SNS.

---

## Key Features

- **Secure File Access** — Uses Lambda to generate expiring pre-signed download links, ensuring files are never publicly exposed.
- **Decoupled Architecture** — Separates web, database, and notification layers for improved fault tolerance and scalability.
- **Automated Notifications** — Integrates SNS to provide immediate feedback to users via email.
- **Three-Tier Design** — Adheres to cloud best practices by isolating the database tier from the public internet.

---

## Screenshots

![Screenshot 1](Screenshot%20(24).png)
![Screenshot 2](Screenshot%20(25).png)
![Screenshot 3](Screenshot%20(26).png)
![Screenshot 4](Screenshot%20(28).png)
![Screenshot 5](Screenshot%20(29).png)
![Screenshot 6](Screenshot%20(30).png)
![Screenshot 7](Screenshot%20(31).png)
![Screenshot 8](Screenshot%20(32).png)
![Screenshot 9](Screenshot%20(33).png)
![Screenshot 10](Screenshot%20(34).png)
![Screenshot 11](Screenshot%20(35).png)
![Screenshot 12](Screenshot%20(36).png)
![Screenshot 13](Screenshot%20(37).png)
![Screenshot 14](Screenshot%20(38).png)
