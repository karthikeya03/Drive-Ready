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

AWS Lambda is a powerful tool for automating tasks and running scripts efficiently, reducing both operational overhead and costs.
