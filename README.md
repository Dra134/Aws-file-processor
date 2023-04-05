# AWS S3 File Processing
This project uses AWS EventBridge to trigger an AWS Lambda function through an Amazon SQS queue when specific files are uploaded to an S3 bucket. The Lambda function then modifies the file content and saves the modified file to another prefix named "errors" within the same bucket. The SQS layer helps manage the concurrency and rate at which the Lambda function processes events, providing better control over resource usage and scalability.
## Features
* The system automatically responds to specific file uploads in the s3 bucket
* The project leverages AWS managed services, which are desined to scale automatically
* The use of SQS in thye architecture provides built-in error handeling
* The setup can be easily integrated with AWS monitoring and logging services
## Flow
1. A specific file is uploaded to the S3 bucket.
2. S3 generates an Object Created event, which is captured by EventBridge.
3. EventBridge filters the events based on the file name or key pattern and sends the events to the SQS Fifo queue.
4. The Lambda function polls the SQS Fifo queue, processes the events, modifies the file content, and saves the modified file to the "errors" prefix in the same S3 bucket.
## Low Level Design
