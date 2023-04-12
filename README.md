# AWS S3 File Processing
This project uses AWS EventBridge to trigger an AWS Lambda function through an Amazon SQS queue when specific files are uploaded to an S3 bucket. The Lambda function then modifies the file content and saves the modified file to another prefix named "Errors" within the same bucket. The SQS layer helps manage the concurrency and rate at which the Lambda function processes events, providing better control over resource usage and scalability.
## Rationale
Managed services ensure scalability and performance with automatic scaling, letting you focus on the core functionality of file processing tasks without worrying about managing the infrastructure. The pay-per-use pricing model makes the solution cost-effective, especially for variable workloads, compared to running your own servers or containers with fixed costs. The integration of SQS offers built-in error handling and automatic retries, enhancing the system's resiliency, while the overall architecture promotes maintainability and seamless integration with the AWS ecosystem. In essence, this selection of services delivers a scalable, cost-effective, and maintainable solution that simplifies infrastructure management, making it an ideal choice for your file processing needs.
## High Level Design
1. A specific file is uploaded to the S3 bucket.
2. S3 generates an Object Created event, which is captured by EventBridge.
3. EventBridge filters the events based on the file name or key pattern and sends the events to the SQS queue.
4. The Lambda function polls the SQS queue, processes the events, modifies the file content, and saves the modified file to the "errors" prefix in the same S3 bucket.
![Untitled Diagram](https://user-images.githubusercontent.com/101883275/230234952-d5c56284-fe86-4c5d-83f7-2dd07f1b8792.jpg)

## Low Level Design
1. A S3 bucket is used to store the files. When a file is uploaded an S3 Object Created event is generated
2. EventBridge is used to capture the S3 Object Created events and filter them based on the file name or key pattern. The filtered events are then sent to the SQS queue.
3. An SQS queue is used as an intermediary between EventBridge and the Lambda function. It receives the filtered events from EventBridge and manages the rate at which the Lambda fucntion processes the events.
4. A Lambda fucntion is responsible for processing the file upon receiving the event from the SQS queue. The function modifies the file content according to the specified rules and saves the modified file to the "Error" prefix in the same S3 bucket.
![Untitled Diagram (1)](https://user-images.githubusercontent.com/101883275/231315708-3ca3047d-59e0-4849-acc0-9884b1c0a413.jpg)
