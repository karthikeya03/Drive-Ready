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

![image](https://github.com/user-attachments/assets/e25dadce-0d05-4dfa-9622-613119907273)

## Benefits of AWS Lambda

1. **Supports Multiple Programming Languages**: Lambda supports a variety of programming languages including Python, JavaScript (Node.js), Java, C#, and Go, allowing flexibility in development.

2. **Fully Automated Application**: Lambda handles infrastructure management automatically, enabling you to focus solely on your code without worrying about servers.

3. **Scalability**: Lambda automatically scales your application by running code in response to triggers, handling thousands of requests simultaneously without manual intervention.

4. **Pay-as-You-Go Pricing**: You only pay for the compute time you consume. There are no charges when your code is not running, which helps to reduce costs.

5. **Integrated with Other AWS Services**: Lambda integrates seamlessly with other AWS services like S3, DynamoDB, and API Gateway, allowing you to build complex serverless applications.

6. **Automatic Fault Tolerance**: Lambda provides built-in fault tolerance by automatically handling failures and retries, which enhances the reliability of your application.

7. **Event-Driven Execution**: Lambda functions are triggered by events such as HTTP requests, changes in data, or scheduled tasks, enabling responsive and efficient processing.

## AWS Lambda Triggers

| **Trigger Source**               | **Description**                                                                                      |
|----------------------------------|------------------------------------------------------------------------------------------------------|
| **API Gateway**                  | Allows Lambda functions to respond to HTTP requests via REST or WebSocket APIs.                      |
| **S3 (Simple Storage Service)**  | Triggers Lambda functions when objects are created, deleted, or modified in an S3 bucket.           |
| **DynamoDB Streams**             | Invokes Lambda functions when items in a DynamoDB table are added, updated, or deleted.                |
| **SQS (Simple Queue Service)**   | Triggers Lambda functions when messages arrive in an SQS queue.                                    |
| **SNS (Simple Notification Service)** | Executes Lambda functions in response to notifications published to an SNS topic.                   |
| **CloudWatch Events**            | Invokes Lambda functions based on scheduled events or other CloudWatch triggers.                    |
| **Kinesis**                      | Triggers Lambda functions to process data streams from Amazon Kinesis.                              |

## AWS Lambda Limitations

| **Limitation**                       | **Description**                                                                                          |
|-------------------------------------|----------------------------------------------------------------------------------------------------------|
| **Execution Time**                  | Maximum execution time for a Lambda function is 15 minutes.                                             |
| **Memory Allocation**               | Lambda functions can be allocated between 128 MB and 10,240 MB of memory.                               |
| **Deployment Package Size**         | The maximum size of a deployment package is 50 MB (zipped) or 250 MB (uncompressed).                    |
| **Concurrent Executions**           | The default concurrent execution limit is 1,000 per AWS account per region.                            |
| **Invocation Payload Size**         | The maximum size of the invocation payload is 6 MB for synchronous invocations and 256 KB for asynchronous invocations. |
| **Function Timeout**                | The maximum timeout for a Lambda function is 15 minutes.                                                |
| **Execution Role Permissions**      | Lambda functions require permissions through an IAM role, which may limit the actions they can perform. |

## AWS Lambda Function to Stop EC2 Instance :

### Function Overview

1. **Purpose**: Create an AWS Lambda function that stops an EC2 instance at a specified time.

2. **Function Code**:
   - The Lambda function will use the AWS SDK to stop an EC2 instance based on an instance ID.

### Steps to Configure the Lambda Function

1. **Create the Lambda Function**:
   - Access the AWS Lambda console.
   - Click on “Create function” and select “Author from scratch.”
   - Provide a name for your function.
   - Choose the appropriate runtime (e.g., Python 3.x).
   - Create a new IAM role with basic Lambda permissions.

2. **Set Environment Variables**:
   - In the Lambda function configuration, set an environment variable for the instance ID of the EC2 instance you want to stop.

3. **Deploy the Lambda Function**:
   - Input the function code into the Lambda editor.
   - Click “Deploy” to save and activate the function.

### Configure the Trigger

1. **Create a CloudWatch Event Rule**:
   - Go to the CloudWatch console.
   - Navigate to “Rules” under “Events” or “EventBridge.”
   - Click “Create rule” and choose “Event Source” as “Schedule.”
   - Define the schedule expression (e.g., `rate(1 minute)` for every minute or `rate(10 minutes)` for every 10 minutes).
   - Set the Lambda function as the target for the rule.
   - Click “Configure details,” enter a name and description, and create the rule.

### IAM Role

- **Role Requirement**: The Lambda function must have an IAM role with appropriate permissions to stop EC2 instances. Without an IAM role, there can never be a lambda function. 

## AWS Lambda Function to Stop EC2 Instance

| **Step**                        | **Description**                                                                                          |
|---------------------------------|----------------------------------------------------------------------------------------------------------|
| **1. Function Overview**         | Create an AWS Lambda function that stops an EC2 instance based on the instance ID provided.             |
| **2. Create the Lambda Function**| - Access the AWS Lambda console. <br> - Click “Create function” and choose “Author from scratch.” <br> - Enter a function name. <br> - Select runtime (e.g., Python 3.x). <br> - Create a new IAM role with basic Lambda permissions. |
| **3. Set Environment Variables** | - In Lambda configuration, set an environment variable named `INSTANCE_ID` with the EC2 instance ID to be stopped. |
| **4. Deploy the Lambda Function** | - Input the function code into the Lambda editor. <br> - Click “Deploy” to save and activate the function. |
| **5. Configure the Trigger**     | - Go to the CloudWatch console. <br> - Navigate to “Rules” under “Events” or “EventBridge.” <br> - Click “Create rule” and select “Schedule” as the event source. <br> - Define the schedule expression (e.g., `rate(1 minute)` or `rate(10 minutes`). <br> - Set the Lambda function as the target. <br> - Click “Configure details,” provide a name and description, and create the rule. |
| **6. IAM Role**                  | - Ensure the Lambda function has an IAM role with permissions to stop EC2 instances. <br> - The basic Lambda execution role alone is not sufficient. |


# AWS Lambda Hands-On Activity

## Lab Overview

In this activity, you will create an AWS Lambda function that stops an Amazon EC2 instance every minute using an Amazon EventBridge event.

### Architectural Diagram

![Architectural Diagram](https://github.com/user-attachments/assets/0f1129cc-b1fa-47dc-a2e5-299fe40c01b7)


## Duration

This activity takes approximately 30 minutes to complete.

## AWS Service Restrictions

Access is limited to the necessary services and actions for this lab.

## Accessing the AWS Management Console

1. Choose **Start Lab**.
2. Wait for the circle icon next to the **AWS** link to turn green.
3. Choose the **AWS** link to open the console.

## Task 1: Create a Lambda Function

1. Search for and choose **Lambda**.
2. Choose **Create a function**.
3. Configure the settings:
   - **Author from scratch**
   - **Function name**: `myStopinator`
   - **Runtime**: Python 3.11
   - **Execution role**: Use an existing role
   - **Existing role**: `myStopinatorRole`
4. Choose **Create function**.

   ![image](https://github.com/user-attachments/assets/fcae605c-158d-408e-a5ad-1acf92272093)


## Task 2: Configure the Trigger

1. Choose **Add trigger**.
2. Select **EventBridge (CloudWatch Events)**.
3. Create a new rule:
   - **Rule name**: `everyMinute`
   - **Rule type**: Schedule expression
   - **Schedule expression**: `rate(1 minute)`
4. Choose **Add**.

![image](https://github.com/user-attachments/assets/28882f77-dabc-4f40-823e-83ab120ca9d5)

## Task 3: Configure the Lambda Function

1. In the **Function overview** pane, choose **Code**, then **lambda_function.py**.

2. Replace the existing code with the following:

   ```python
   import boto3
   region = '<REPLACE_WITH_REGION>'
   instances = ['<REPLACE_WITH_INSTANCE_ID>']
   ec2 = boto3.client('ec2', region_name=region)
   
   def lambda_handler(event, context):
       ec2.stop_instances(InstanceIds=instances)
       print('stopped your instances: ' + str(instances))
   ```

![image](https://github.com/user-attachments/assets/2529796f-fc2d-45a9-bd8a-08fdd8a0fc01)

3. Replace `<REPLACE_WITH_REGION>` with your region code (e.g., 'us-east-1').

4. Verify an EC2 instance named `instance1` is running and copy its instance ID.

5. Replace `<REPLACE_WITH_INSTANCE_ID>` with the copied instance ID.

6. Save and deploy the code.

## Task 4: Verify the Lambda Function

1. Check the **Monitor** tab for invocation and error metrics.
2. In the EC2 console, verify the instance was stopped.

## Submitting Your Work

1. Choose **Submit** at the top of the instructions.
2. Wait for the grades panel to appear.
3. If needed, wait a few minutes and submit again for credit.

## Activity Complete

- Choose **End Lab** to end the activity.

# CRON :

## Introduction

CRON is a time-based job scheduler in Unix-like operating systems. Users can schedule jobs (commands or scripts) to run at specific times or intervals. CRON is commonly used for system maintenance or administration.

## Basic Concepts

### CRON Daemon

- **Definition:** The CRON daemon is a long-running process that executes CRON jobs at specified times.
- **Location:** Typically located at `/usr/sbin/cron` or `/usr/sbin/crond`.

### CRON Table (Crontab)

- **Definition:** The CRON table, known as the crontab, is a configuration file that specifies shell commands to run periodically on a given schedule.
- **Location:** Each user has their own crontab file, usually stored in `/var/spool/cron/crontabs`.

## Crontab Format

A crontab file has five time-and-date fields followed by a command. The fields are:

| Field        | Allowed Values  | Special Characters |
| ------------ | --------------- | ------------------ |
| Minute       | 0-59            | , - * /            |
| Hour         | 0-23            | , - * /            |
| Day of Month | 1-31            | , - * /            |
| Month        | 1-12 or JAN-DEC | , - * /            |
| Day of Week  | 0-6 or SUN-SAT  | , - * /            |

### Special Characters

- **Comma (,):** Separates multiple values.
- **Dash (-):** Specifies a range of values.
- **Asterisk (*):** Represents all possible values for a field.
- **Slash (/):** Specifies step values.

### Example Crontab Entries

```
# Run a script every day at 2 AM
0 2 * * * /path/to/script.sh

# Run a command every 15 minutes
*/15 * * * * /path/to/command

# Run a task every Monday at 5 PM
0 17 * * 1 /path/to/task

# Run a backup on the 1st of every month at 3:30 AM
30 3 1 * * /path/to/backup.sh
```

## Managing Crontab Files

### List Crontab Entries

To list your current crontab entries, use:

```
crontab -l
```

### Edit Crontab File

To edit your crontab file, use:

```
crontab -e
```

### Remove Crontab File

To remove your crontab file, use:

```
crontab -r
```

## Special Strings

CRON also supports special strings to replace the five time-and-date fields:

| String    | Equivalent to            |
| --------- | ------------------------ |
| @reboot   | Run at startup           |
| @yearly   | 0 0 1 1 * (once a year)  |
| @annually | Same as @yearly          |
| @monthly  | 0 0 1 * * (once a month) |
| @weekly   | 0 0 * * 0 (once a week)  |
| @daily    | 0 0 * * * (once a day)   |
| @midnight | Same as @daily           |
| @hourly   | 0 * * * * (once an hour) |

### Example Using Special Strings

```
# Run a command at every system reboot
@reboot /path/to/startup_script

# Run a job once a year
@yearly /path/to/yearly_job
```

## Conclusion

CRON is a powerful tool for scheduling repetitive tasks in Unix-like operating systems. Understanding its syntax and capabilities can greatly enhance system administration and automation tasks.




