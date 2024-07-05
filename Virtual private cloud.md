# Virtual Private Cloud (VPC) Guide

## Introduction

A Virtual Private Cloud (VPC) is a virtual network that closely resembles a traditional network you would operate in your own data center. This guide will walk you through creating and configuring a VPC, launching an EC2 instance, enabling ICMP, connecting via SSH, detaching the internet gateway, and verifying connectivity.

## Steps

### Step 1: Launch an EC2 Instance in the Default VPC

1. **Open the Amazon EC2 Console**
   - Navigate to the [Amazon EC2 Console](https://console.aws.amazon.com/ec2/).

2. **Launch Instance**
   - Click on "Launch Instance".

3. **Choose an Amazon Machine Image (AMI)**
   - Select an appropriate AMI, such as Amazon Linux 2 AMI.

4. **Choose an Instance Type**
   - Select the instance type (e.g., t2.micro for free tier).

5. **Configure Instance**
   - Ensure the default VPC is selected.
   - Click "Next: Configure Instance Details".

6. **Add Storage**
   - Configure the storage as needed.
   - Click "Next: Add Tags".

7. **Add Tags**
   - Optionally, add tags to your instance.
   - Click "Next: Configure Security Group".

8. **Configure Security Group**
   - Create a new security group or select an existing one.
   - Ensure SSH (port 22) is allowed.
   - Add a rule to allow ICMP (ping).
   - Click "Review and Launch".

9. **Review and Launch**
   - Review your instance configuration.
   - Click "Launch".
   - Select an existing key pair or create a new one to access your instance.

### Step 2: Connect to Your EC2 Instance via SSH

1. **Obtain the Public IP**

   - From the EC2 Dashboard, select your instance and note the public IP address.

2. **Open SSH Terminal**

   - Open a terminal on your local machine.

3. **Connect Using SSH**

   - Use the following command to connect:

     ```bash
     ssh -i /path/to/your-key-pair.pem ec2-user@your-instance-public-ip
     ```

### Step 3: Detach the Internet Gateway from the Default VPC

1. **Navigate to the VPC Console**
   - Go to the [Amazon VPC Console](https://console.aws.amazon.com/vpc/).

2. **Select the Default VPC**
   - Under "Virtual Private Cloud", select "Your VPCs".
   - Choose the default VPC.

3. **Detach the Internet Gateway**
   - Go to "Internet Gateways".
   - Select the internet gateway attached to the default VPC.
   - Click "Actions" and then "Detach from VPC".

### Step 4: Verify SSH Connection

1. **Reconnect via SSH**
   - Try reconnecting to your EC2 instance using SSH.
   - You should not be able to connect, as the internet gateway is detached.

2. **Verify ICMP**
   - Try pinging your instance.
   - The ping should fail, indicating no connectivity.

### Conclusion

This guide has walked you through launching an EC2 instance in a default VPC, enabling ICMP, connecting via SSH, detaching the internet gateway, and verifying the connection status. By following these steps, you can understand the basic operations and connectivity within a VPC.

## Images

- [EC2 Console](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-console.png)
- [Launch Instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/launch-wizard1.png)
- [Security Group](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/launch-wizard4.png)
- ![VPC Console](https://raw,docs.aws.amazon.com/vpc/latest/userguide/images/vpc-dashboard.png)
