# aws-automated-etl-pipeline
Automated ETL Pipeline on AWS using S3, Lambda, Glue, EventBridge, SNS, and CloudWatch.

📌 Automated ETL Pipeline on AWS

S3 • Lambda • Glue • EventBridge • SNS • CloudWatch

🚀 Overview

This project implements a fully automated serverless ETL pipeline on AWS.
When a CSV file is uploaded to an S3 folder, the entire workflow triggers automatically:

S3 event triggers a Lambda function

Lambda starts a Glue ETL job

Glue transforms the data (drop duplicates)

Output stored in a target S3 folder

EventBridge monitors Glue job state

SNS sends an email notification

CloudWatch logs events from all services

The pipeline runs without any manual steps—fully serverless and event-driven.

🏗 Architecture Diagram (ASCII)
<img width="406" height="191" alt="image" src="https://github.com/user-attachments/assets/d7c00d82-b995-40cc-81f6-b605f2e13418" />


🧩 AWS Services Used

Amazon S3 – Storage for raw + transformed data

AWS Lambda – Trigger & Glue job executor

AWS Glue – ETL engine

Amazon EventBridge – Job state monitoring

Amazon SNS – Email notifications

Amazon CloudWatch – Logging

IAM Roles – Secure service permissions

🛠 Technologies
Component	Technology
Storage	Amazon S3
ETL	AWS Glue
Orchestration	AWS Lambda + EventBridge
Notification	AWS SNS
Logging	CloudWatch
Language	Python (Boto3)
