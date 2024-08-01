# Session 9: AWS Lambda

## Definition
AWS Lambda is a serverless compute service that allows you to run code without provisioning or managing servers. Lambda executes your code only when needed and scales automatically, from a few requests per day to thousands per second.

## Key Features

| Feature              | Definition                                                                                      |
|----------------------|-------------------------------------------------------------------------------------------------|
| **Serverless**       | No need to manage infrastructure, as AWS Lambda automatically handles it.                       |
| **Automatic Scaling**| Scales automatically based on the number of incoming requests, handling thousands per second.   |
| **Pay-as-you-go**    | Charges are incurred only for the compute time consumed, with no charge when your code is not running. |
| **Event-driven**     | Executes code in response to events such as changes in data, shifts in system state, or user actions. |

## Automation and Scripting
AWS Lambda is ideal for automating tasks and running scripts triggered by specific events.

### Example 1: Create Multiple Servers with Different Configurations
Imagine you need to create five servers with different configurations. This can be done by writing a script and telling Lambda when to trigger it. Here’s how:

1. **Write a Script**: Develop a script that uses AWS SDK to create servers with the desired configurations.
2. **Set Up Lambda Function**: Upload the script to a Lambda function.
3. **Trigger the Function**: Configure the trigger for the Lambda function, such as a scheduled event using Amazon CloudWatch Events.

This way, the task is automated, and servers are created as per your specifications without manual intervention.

### Example 2: Send a Birthday Message at a Specific Time
Suppose you want to send a birthday message at 12 PM. Normally, you might launch an EC2 instance to handle this. If the instance is launched at 10 AM, it remains idle for two hours, incurring unnecessary charges. 

With AWS Lambda, you can avoid this by:

1. **Create a Lambda Function**: Write a function that sends the birthday message.
2. **Schedule the Function**: Use Amazon CloudWatch Events to schedule the function to run exactly at 12 PM.

This approach eliminates the need for an always-on server, and you are only charged for the execution time of the Lambda function.

### Additional Examples
- **Image Processing**: Automatically process images uploaded to an S3 bucket.
- **Data Transformation**: Convert data formats or process streams of data in real-time.
- **Monitoring and Alerts**: Trigger alerts based on system metrics or application logs.

# AWS Lambda Use Cases and Examples

## 1. Image Processing
**Description**: Automatically process images uploaded to an S3 bucket using AWS Lambda.

### Example
- **Use Case**: Resize images upon upload to an S3 bucket.
- **Trigger**: S3 Event

### Steps
1. **Create S3 Buckets**: 
   - Create a source bucket (e.g., `image-upload-source`).
   - Create a destination bucket (e.g., `image-upload-destination`).

2. **Create Lambda Function**:
   - Configure the function to handle image resizing.

3. **Add S3 Trigger**:
   - Set up an S3 trigger on the source bucket to invoke the Lambda function on object creation.

## 2. Data Transformation
**Description**: Convert data formats or process streams of data in real-time using AWS Lambda.

### Example
- **Use Case**: Transform incoming JSON data into a different format (e.g., CSV) as it arrives in an S3 bucket.
- **Trigger**: S3 Event or Kinesis Data Stream

### Steps
1. **Set Up Data Stream**:
   - Create a Kinesis Data Stream or S3 bucket for incoming data.

2. **Create Lambda Function**:
   - Configure the function to handle data transformation.

3. **Add Trigger**:
   - Set up a trigger from the data stream or S3 bucket to invoke the Lambda function on data arrival.

## 3. Monitoring and Alerts
**Description**: Trigger alerts based on system metrics or application logs using AWS Lambda.

### Example
- **Use Case**: Send an alert if CPU utilization exceeds a certain threshold.
- **Trigger**: CloudWatch Alarm

### Steps
1. **Create CloudWatch Alarm**:
   - Set up an alarm for the desired metric (e.g., CPU utilization).

2. **Create Lambda Function**:
   - Configure the function to handle alert notifications (e.g., send an email).

3. **Add Alarm Trigger**:
   - Set up the CloudWatch Alarm to invoke the Lambda function when the alarm state is triggered.

> AWS Lambda is a powerful tool for automating tasks and running scripts efficiently, reducing both operational overhead and costs.

# Key Components for AWS Lambda Function

## 1. Lambda Function (Script/Code)
- **Description**: This is the code that runs when the Lambda function is triggered. It defines the logic and operations to be performed.
- **Example**: A Python script that processes images, transforms data, or sends notifications.

## 2. Trigger
- **Description**: The event that initiates the execution of the Lambda function. Triggers define when and how the Lambda function should be executed.
- **Examples**:
  - **S3 Event**: Trigger the function when a file is uploaded to an S3 bucket.
  - **CloudWatch Alarm**: Trigger the function based on a specific metric or log condition.
  - **Kinesis Data Stream**: Trigger the function when data is added to a Kinesis stream.

## 3. IAM Role
- **Description**: An AWS Identity and Access Management (IAM) role that provides the necessary permissions for the Lambda function to access other AWS services and resources.
- **Key Points**:
  - **Permissions**: The IAM role grants permissions to perform actions such as reading from or writing to S3 buckets, accessing DynamoDB, or sending messages to SNS.
  - **Role Assignment**: Without the appropriate IAM role, the Lambda function will not have the required permissions to interact with other services or execute properly.
  - **Interconnection**: If the Lambda function needs to interact with other AWS services, it must be assigned a role with the appropriate permissions.

### Summary
- **Lambda Function**: Contains the code to execute.
- **Trigger**: Defines when the function should run.
- **IAM Role**: Provides the permissions needed for the function to interact with other services.

> Without the IAM role, the Lambda function will not have the necessary permissions to operate and interact with other AWS resources.

