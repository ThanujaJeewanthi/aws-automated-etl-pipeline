# 📌 Automated ETL Pipeline on AWS

### **S3 • Lambda • Glue • EventBridge • SNS • CloudWatch**

## 🧾 Project Overview

This project implements a **fully automated serverless ETL pipeline**
using Amazon Web Services (AWS).
Whenever a CSV file is uploaded into a specific folder in Amazon S3, the
entire workflow executes automatically.

1.  **S3** triggers a **Lambda** function
2.  Lambda starts a **Glue ETL job**
3.  Glue transforms the dataset
4.  Output is written to an S3 **/load** folder
5.  **EventBridge** listens for Glue job status
6.  **SNS** sends an email notification
7.  **CloudWatch** logs the entire workflow

The pipeline is fully automated, event‑driven, and serverless.

------------------------------------------------------------------------

## 🏗 Architecture Diagram

<img width="406" height="191" alt="image" src="https://github.com/user-attachments/assets/d37f7701-8833-44e2-9eb9-45c11c117d3e" />


------------------------------------------------------------------------

## 🧩 AWS Services Used

-   Amazon S3
-   AWS Lambda
-   AWS Glue
-   Amazon EventBridge
-   Amazon SNS
-   AWS CloudWatch
-   IAM

------------------------------------------------------------------------



------------------------------------------------------------------------

## 🧪 Lambda Function Code 

``` python
import boto3

def lambda_handler(event, context):
    glue = boto3.client('glue')
    job_name = 's3-glue-s3'

    try:
        response = glue.start_job_run(JobName=job_name)
        return {
            'statusCode': 200,
            'body': f"Glue job '{job_name}' started: {response['JobRunId']}"
        }
    except Exception as e:
        return {
            'statusCode': 500,
            'body': f"Error: {str(e)}"
        }
```

------------------------------------------------------------------------

⚙️ How the Pipeline Works (Step-by-Step)


1️⃣ Create S3 Bucket Structure

extract/ — upload raw CSV files

load/ — Glue writes transformed CSV files

2️⃣ Lambda Trigger

Trigger type: S3 PUT event

Condition: extract/*.csv

Lambda prints event → starts Glue job

3️⃣ Glue ETL Job

Using AWS Glue Studio (Visual ETL):

Source: S3 /extract folder

Transform: Drop Duplicates

Target: S3 /load folder

Format: CSV

No compression

Single file output

4️⃣ EventBridge Rule

EventBridge listens to:

Glue Job State Change:
- SUCCEEDED
- FAILED
- TIMEOUT


It forwards events to:

SNS Topic 📧

CloudWatch Logs 📊

5️⃣ SNS Email Notification

Created SNS topic

Subscribed email address

Confirmation required

Receives job success/failure notifications

<img width="1920" height="1080" alt="Screenshot (174)" src="https://github.com/user-attachments/assets/b035ddd8-12cc-42ee-ad18-518f0a166753" />


6️⃣ CloudWatch Monitoring

Monitors:

Lambda logs
<img width="1920" height="1080" alt="Screenshot (169)" src="https://github.com/user-attachments/assets/6f94aa4b-1f40-4657-95c6-0b48b14160f1" />

Glue job logs
<img width="1920" height="1080" alt="Screenshot (172)" src="https://github.com/user-attachments/assets/3645d5aa-0c34-43b5-9b70-d3c8da367da8" />

EventBridge rule invocations

<img width="1895" height="880" alt="image" src="https://github.com/user-attachments/assets/ae168588-e8f3-4498-a4f2-4a22860fd27d" />


------------------------------------------------------------------------

## 🚀 Deployment Steps

1.  Create S3 bucket with `extract/` and `load/` folders\
2.  Create Lambda function & add S3 trigger\
3.  Build Glue ETL job using Visual ETL\
4.  Create SNS topic and subscription\
5.  Create EventBridge rule for Glue Job State Change\
6.  Upload a CSV file to test end‑to‑end automation

------------------------------------------------------------------------

## 🎯 Status

✔ Fully automated\
✔ Email notifications working\
✔ Logs available in CloudWatch

------------------------------------------------------------------------

## 📚 Documentation

See the `docs/` folder for reports and diagrams.

------------------------------------------------------------------------

## 💬 Contact

Feel free to reach out for improvements or collaboration!
