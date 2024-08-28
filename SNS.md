# AWS Simple Notification Service (SNS)

## Overview

AWS Simple Notification Service (SNS) is a fully managed service that provides messaging and mobile notification capabilities. SNS enables you to send messages and notifications to subscribers or other applications.

### Key Concepts

- **Topic:** A logical access point that acts as a communication channel. When you publish a message to a topic, all the topic's subscribers receive the message.
- **Subscription:** The process by which you register an endpoint (e.g., email, HTTP endpoint) to receive notifications from a topic.
- **Protocol:** The method used to deliver notifications. Examples include email, HTTP, and SMS.

## Summary

- **SNS Topic:** A communication channel for sending notifications.
- **Subscription:** Registration of an endpoint to receive notifications.
- **Protocols:** Methods for notification delivery (e.g., Email, HTTP).
- **Confirmation:** Required for subscriptions to become active.

# AWS Auto Scaling Groups and EC2 Instance Creation

## Overview

AWS Auto Scaling groups allow you to automatically scale your Amazon EC2 instances based on demand. They ensure that you have the right number of instances available to handle your application load.

### Key Concepts

- **EC2 Instance:** A virtual server in AWS that runs applications.
- **Amazon Machine Image (AMI):** A template that contains the software configuration (e.g., operating system, application server, applications) required to launch an EC2 instance.
- **Launch Configuration/Template:** A configuration template used by an Auto Scaling group to launch EC2 instances.

## Step-by-Step Guide

### 1. Creating an EC2 Instance

1. **Sign in to AWS Management Console**
   - Navigate to the [Amazon EC2 console](https://console.aws.amazon.com/ec2/).

2. **Launch an EC2 Instance**
   - Click on **Launch Instance**.
   - **Choose an AMI:** Select an existing AMI or a public AMI provided by AWS. An AMI is a pre-configured template for your instance.
     - **Example AMI:** Amazon Linux 2 AMI (HVM), SSD Volume Type.
   - **Choose an Instance Type:**
     - For example, choose `t2.micro` (free tier eligible).
   - **Configure Instance Details:**
     - You can leave the default settings or customize the network, subnet, etc.
   - **Add Storage:**
     - Set the storage size and type. Default settings are usually sufficient.
   - **Add Tags:**
     - (Optional) Add tags to your instance for identification.
   - **Configure Security Group:**
     - Choose an existing security group or create a new one.
     - Ensure that the security group allows inbound traffic for SSH (port 22) and HTTP (port 80).
   - **Review and Launch:**
     - Review your instance configuration.
     - Choose an existing key pair or create a new one. This key pair will be used to SSH into the instance.
     - Click **Launch**.

3. **Access Your Instance**
   - Once launched, your EC2 instance will appear in the EC2 dashboard.
   - Use the public DNS or IP address to connect to your instance via SSH.

### 2. Creating an Amazon Machine Image (AMI)

1. **Connect to Your EC2 Instance**

   - SSH into your instance using the key pair you specified during launch.

2. **Install and Configure Applications**

   - Install any applications, services, or configurations required for your web app.

3. **Create an AMI from the Instance**

   - Navigate to the **Instances** section of the EC2 console.
   - Right-click on your instance, choose **Image** > **Create Image**.
   - Provide a name and description for your AMI.
   - Specify any additional storage volumes if necessary.
   - Click **Create Image**.

4. **Using the AMI**

   - Your newly created AMI will appear in the **AMIs** section of the EC2 dashboard.
   - This AMI can now be used to launch new instances with the same configuration.

## 3. Step-by-Step Guide to Create an SNS

### 1. Create an SNS Topic

1. **Sign in to AWS Management Console**
   - Navigate to the [Amazon SNS console](https://console.aws.amazon.com/sns/).

2. **Create a New Topic**
   - Go to **Topics** in the left-hand menu and click **Create topic**.
   - Select the type of topic (Standard or FIFO).
     - **Standard Topic:** For high-throughput, distributed systems. Messages are delivered at least once.
     - **FIFO Topic:** For ordered message delivery with exactly-once processing.
   - Enter a **Name** for the topic and optionally a **Display Name**.
   - Click **Create topic**.

3. **Note the Topic ARN**
   - After creating the topic, the Topic ARN (Amazon Resource Name) is displayed. This ARN uniquely identifies the topic.

### 2. Create a Subscription

1. **Navigate to Subscriptions**
   - From the SNS dashboard, select **Subscriptions** from the left-hand menu.
   - Click **Create subscription**.

2. **Configure the Subscription**
   - **Select Topic:** Choose the topic by pasting its ARN or selecting it from the dropdown.
   - **Select Protocol:** Choose the delivery method (e.g., Email, HTTP, HTTPS).
   - **Endpoint:** Provide the necessary endpoint information (e.g., email address, URL).

3. **Confirm Subscription**
   - For **Email Protocol**, an email is sent to the provided address.
   - The recipient must click the confirmation link in the email to confirm the subscription.
   - For other protocols like HTTP, the endpoint must handle the confirmation request.

4. **Verify Subscription Status**
   - Go back to the **Subscriptions** section in the SNS console.
   - Refresh the page to update the subscription status.
   - Once confirmed, the status changes from **Pending Confirmation** to **Confirmed**.

### 3. Attach SNS Topic to a Service

- You can attach the SNS topic to AWS services like CloudWatch Alarms.
- When an alert is generated, it is sent to the SNS topic, which forwards it to all subscribed endpoints.

## Example Workflow

1. **Create Topic**
   - Topic Name: `MyAlertTopic`
   - Topic ARN: `arn:aws:sns:region:account-id:MyAlertTopic`

2. **Create Subscription**
   - Topic ARN: `arn:aws:sns:region:account-id:MyAlertTopic`
   - Protocol: Email
   - Endpoint: `example@example.com`

3. **Confirmation Email**
   - The recipient clicks the confirmation link in the email to activate the subscription.

4. **Attach to Service**
   - For example, attach `MyAlertTopic` to a CloudWatch alarm.
   - All notifications from the alarm will be sent to `example@example.com`.

### 4. Creating an Auto Scaling Group

1. **Sign in to AWS Management Console**
   - Navigate to the [Amazon EC2 Auto Scaling console](https://console.aws.amazon.com/ec2autoscaling/).

2. **Create an Auto Scaling Group**
   - Click on **Create Auto Scaling group**.

3. **Configure Basic Settings**
   - **Name:** Provide a name for your Auto Scaling group.
   - **Launch Configuration or Launch Template:**
     - You can either select a **Launch Configuration** or **Launch Template**.
     - Note: In a sandbox environment, **Launch Templates** may not work. If you encounter issues, switch to using a **Launch Configuration**.

4. **Create a Launch Configuration (If Needed)**
   - **Select an AMI:** Choose the AMI you created earlier (`my-web-app`).
   - **Instance Type:** Choose `t2.micro` (or another appropriate instance type).
   - **Configure Security Group:**
     - Choose an existing security group or create a new one with HTTP (port 80) enabled.
   - **Key Pair:** Select an existing key pair that was created earlier.

5. **Advanced Configuration**
   - **Load Balancer:** You can create or attach a load balancer to the Auto Scaling group during this step.
   - **Scaling Policies:** Define how the group should scale in and out based on metrics like CPU usage or network traffic.

6. **Review and Create**
   - Review all configurations and click **Create Auto Scaling group**.

## Using Auto Scaling Groups

- **Auto Scaling Group Management:** The group will automatically scale the number of instances up or down based on the defined policies.
- **Monitoring:** Use the EC2 dashboard or CloudWatch to monitor the performance and health of the instances within the Auto Scaling group.

## Summary

- **EC2 Instance:** A virtual server running applications in AWS.
- **AMI:** A template used to create new EC2 instances with pre-configured software.
- **Auto Scaling Group:** Manages EC2 instances, automatically scaling them based on demand.
- **Launch Configuration/Template:** Specifies the AMI, instance type, and other settings used by an Auto Scaling group to launch instances.


# Auto Scaling Groups with Application Load Balancer: Step-by-Step Guide

## 1. Attach to a New Load Balancer

### Application Load Balancer (ALB)
- **Name**: Assign a unique name to your ALB.
- **Internet Facing**: Set this to "Yes" to allow the ALB to be accessible from the internet.
- **Subnets**: Choose the subnets where the ALB will be deployed. These should be in the same VPC as your Auto Scaling Group. For example: Subnets A, B, and C.

### Target Group
- **No need to create manually**: The ASG will automatically create a target group for you.
- **Health Check**: Set the health check interval to 100 seconds. This is the frequency with which the ALB checks the health of the instances.

## 2. Configure Auto Scaling Group

### Size (Min, Max, Desired Capacity)
- **Minimum Desired Capacity**: The minimum number of EC2 instances you want running at all times. For example: `2`
- **Maximum Capacity**: The maximum number of EC2 instances you want running. For example: `3` (due to sandbox limitations).
- **Desired Capacity**: The number of EC2 instances you want to start with initially. For example: `2`

**Explanation**: 
- **Minimum Capacity** ensures that there are always a minimum number of instances running.
- **Maximum Capacity** limits the number of instances that can scale up to, preventing excessive resource use.
- **Desired Capacity** is the initial number of instances the ASG will maintain.

### Target Tracking Policy
- **Policy Type**: Choose the target tracking policy.
- **CPU Utilization**: Set the policy to scale out (add more instances) if CPU utilization exceeds 30%. This means if the CPU usage goes above 30%, the ASG will automatically launch additional instances.
- **Target Value**: Set this to 30%, which is the threshold for scaling.

### Instance Warm-Up
- **Instance Warm-Up**: Set to 100 seconds. This is the amount of time the ASG will wait before considering a new instance to be fully operational and available to handle traffic.

### No Policy
- **No Additional Policies**: You do not need to set any other policies for this configuration.

## 3. Notifications

### Adding SNS Notifications
- **Add Notification**: Enable notifications for your ASG.
- **Add Topic**: Create or select an existing SNS topic to which notifications will be sent.
- **When to Send Alerts**: Check the tick boxes for the types of notifications you want to receive. For example:
  - **Instance Launch**: Notify when a new instance is launched.
  - **Instance Termination**: Notify when an instance is terminated.
  - **Health Check Failures**: Notify if there are health check failures.

**Explanation**:
- **SNS Topic**: An SNS topic is used to send notifications to subscribers when certain events occur in your ASG.
- **Notification Options**: Choose the events for which you want to receive notifications to stay informed about the status and changes in your ASG.

## Summary

1. **Attach to ALB**: Configure your ALB with the correct settings and subnets.
2. **Configure ASG**: Set the minimum, maximum, and desired capacities, and configure target tracking policies and instance warm-up times.
3. **Add Notifications**: Set up SNS notifications to receive alerts about significant events in your ASG.

By following these steps, you can effectively set up and manage an Auto Scaling Group with an Application Load Balancer in AWS.
