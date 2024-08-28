# AWS Simple Notification Service (SNS) Notes

## Overview

AWS Simple Notification Service (SNS) is a fully managed service that provides messaging and mobile notification capabilities. SNS enables you to send messages and notifications to subscribers or other applications.

### Key Concepts

- **Topic:** A logical access point that acts as a communication channel. When you publish a message to a topic, all the topic's subscribers receive the message.
- **Subscription:** The process by which you register an endpoint (e.g., email, HTTP endpoint) to receive notifications from a topic.
- **Protocol:** The method used to deliver notifications. Examples include email, HTTP, and SMS.

## Creating an SNS Topic

1. **Sign in to AWS Management Console**
   - Navigate to the [Amazon SNS console](https://console.aws.amazon.com/sns/).

2. **Create a New Topic**
   - Click on the **Topics** option from the left-hand menu.
   - Click on the **Create topic** button.
   - Select the type of topic (Standard or FIFO). For most use cases, the **Standard** topic is sufficient.
   - **Standard Topic:** Best for high-throughput, distributed systems where messages are delivered at least once.
   - **FIFO Topic:** Best for ordered message delivery and exactly-once processing.

3. **Configure the Topic**
   - Enter a **Name** for the topic.
   - (Optional) Enter a **Display Name**.
   - Click **Create topic**.

4. **Get the Topic ARN**
   - After creation, you will see the Topic ARN (Amazon Resource Name) which is used to uniquely identify the topic.

## Creating a Subscription

1. **Navigate to Subscriptions**
   - From the SNS dashboard, select **Subscriptions** from the left-hand menu.
   - Click **Create subscription**.

2. **Configure Subscription**
   - **Select Topic:** Choose the topic you created by pasting its ARN or selecting it from the drop-down menu.
   - **Select Protocol:** Choose the method of notification delivery (e.g., Email, HTTP, HTTPS).
   - **Endpoint:** Provide the endpoint information (e.g., email address, URL).

3. **Confirm Subscription**
   - If you selected Email as the protocol, an email will be sent to the provided address.
   - The email will contain a confirmation link. Click the link to confirm the subscription.
   - For other protocols like HTTP, the endpoint must handle the confirmation request.

4. **Verify Subscription Status**
   - Return to the **Subscriptions** section in the SNS console.
   - Refresh the page to see the updated subscription status.
   - The status should change from **Pending Confirmation** to **Confirmed** once the subscription is confirmed.

## Using SNS Topics

- **Attach SNS Topic to a Service:** When you attach an SNS topic to a service (e.g., CloudWatch alarms), the notifications from that service will be sent to the SNS topic.
- **Forwarding Alerts:** The alerts will be forwarded to all the endpoints subscribed to the topic.

## Example

1. **Create Topic**
   - Topic Name: `MyAlertTopic`
   - Topic ARN: `arn:aws:sns:region:account-id:MyAlertTopic`

2. **Create Subscription**
   - Topic ARN: `arn:aws:sns:region:account-id:MyAlertTopic`
   - Protocol: Email
   - Endpoint: `example@example.com`

3. **Confirmation Email**
   - The recipient receives an email with a confirmation link.
   - After clicking the confirmation link, the subscription status changes to Confirmed.

4. **Attach to Service**
   - Example: Attach the `MyAlertTopic` to a CloudWatch alarm.
   - Notifications related to the alarm will be sent to `example@example.com`.

## Summary

- **SNS Topic:** A communication channel for sending notifications.
- **Subscription:** Registration of an endpoint to receive notifications.
- **Protocols:** Methods for notification delivery (e.g., Email, HTTP).
- **Confirmation:** Required for subscriptions to become active.

For more detailed information, refer to the [AWS SNS Documentation](https://docs.aws.amazon.com/sns/latest/dg/welcome.html).

