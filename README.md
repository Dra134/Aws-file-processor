# AWS S3 File Processing
This project uses AWS EventBridge to trigger an AWS Lambda function through an Amazon SQS queue when specific files are uploaded to an S3 bucket. The Lambda function then modifies the file content and saves the modified file to another prefix named "errors" within the same bucket. The SQS layer helps manage the concurrency and rate at which the Lambda function processes events, providing better control over resource usage and scalability.
## Features
* A simple method for log checking
* Automatically detects and checks files upon upload
* Uses SQS as an intermediary to decouple the S3 event
