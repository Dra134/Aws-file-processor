# AWS S3 File Processing
This project uses AWS EventBridge to trigger an AWS Lambda function through an Amazon SQS queue when specific files are uploaded to an S3 bucket. The Lambda function then modifies the file content and saves the modified file to another prefix named "Errors" within the same bucket. The SQS layer helps manage the concurrency and rate at which the Lambda function processes events, providing better control over resource usage and scalability.
## Features
* The system automatically responds to specific file uploads in the s3 bucket
* The project leverages AWS managed services, which are desined to scale automatically
* The use of SQS in the architecture provides built-in error handeling
* The setup can be easily integrated with AWS monitoring and logging services
## Flow
1. A specific file is uploaded to the S3 bucket.
2. S3 generates an Object Created event, which is captured by EventBridge.
3. EventBridge filters the events based on the file name or key pattern and sends the events to the SQS queue.
4. The Lambda function polls the SQS queue, processes the events, modifies the file content, and saves the modified file to the "errors" prefix in the same S3 bucket.
## Low Level Design
1. Amazon S3:A S3 bucket is used to store the files. When a file is uploaded an S# Object Created event is generated
2. Amazon EventBridge: EventBridge is used to capture the S3 Object Created events and filter them based on the file name or key pattern. The filtered events are then sent to the SQS queue.
3. Amazon SQS: An SQS queue is used as an intermediary between EventBridge and the Lambda function. It receives the filtered events from EventBridge and manages the rate at which the Lambda fucntion processes the events.
4. AWS Lambda: A Lambda fucntion is responsible for processing the file upon receiving the event from the SQS queue. The function modifies the file content according to the specified rules and saves the modified file to the "Error" prefix in the same S3 bucket.
![Untitled Diagram](https://user-images.githubusercontent.com/101883275/230234952-d5c56284-fe86-4c5d-83f7-2dd07f1b8792.jpg)
