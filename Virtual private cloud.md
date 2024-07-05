# Virtual Private Cloud (VPC) Guide

## Introduction

A Virtual Private Cloud (VPC) is a virtual network that closely resembles a traditional network you would operate in your own data center. This guide will walk you through creating and configuring a VPC, launching an EC2 instance, enabling ICMP, connecting via SSH, detaching the internet gateway, and verifying connectivity.

## ICMP

The Internet Control Message Protocol (ICMP) is a network layer protocol used by network devices to diagnose network communication issues. ICMP is mainly used to determine whether or not data is reaching its intended destination on time.

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

# Creating Your Own Virtual Private Cloud (VPC)

### Introduction

A Virtual Private Cloud (VPC) allows you to provision a logically isolated section of the AWS cloud where you can launch AWS resources in a virtual network. This guide will walk you through the steps to create your own VPC.

### Steps to Create a VPC

1. **Open the Amazon VPC Console**
   - Navigate to the [Amazon VPC Console](https://console.aws.amazon.com/vpc/).

2. **Create a VPC**
   - In the left-hand navigation pane, click on "Your VPCs".
   - Click "Create VPC".

3. **Configure the VPC**
   - **Name tag:** Enter a name for your VPC (e.g., MyVPC).
   - **IPv4 CIDR block:** Enter the CIDR block for your VPC (e.g., 10.0.0.0/16).
   - **IPv6 CIDR block:** Leave this as default (No IPv6 CIDR Block).
   - **Tenancy:** Default.

4. **Create the VPC**
   - Click "Create VPC".

![SUBNET](https://raw.github.com/karthikeya03/IMAGES/JustMain/image2.png)

### Steps to Create a Subnet

1. **Open the Amazon VPC Console**
   - Navigate to the [Amazon VPC Console](https://console.aws.amazon.com/vpc/).

2. **Create a Subnet**
   - In the left-hand navigation pane, click on "Subnets".
   - Click "Create Subnet".

3. **Configure the Subnet**
   - **Subnet Name:**
     - **Field:** Subnet name
     - **Value:** `HELLO_SUBNET`
     - **Description:** This is where you specify a name for your subnet. The name can be up to `256` characters long and helps you identify the subnet later.
   - **Availability Zone:**
     - **Field:** Availability Zone
     - **Value:** No preference
     - **Description:** This dropdown allows you to choose the Availability Zone in which your subnet will reside. If you select "No preference," AWS will choose an appropriate Availability Zone for you.
   - **IPv4 VPC CIDR block:**
     - **Field:** IPv4 VPC CIDR block
     - **Value:** `192.128.64.0`/24
     - **Description:** This specifies the CIDR block of your VPC. The subnet's CIDR block must be within this range.
   - **IPv4 Subnet CIDR block:**
     - **Field:** IPv4 subnet CIDR block
     - **Value:** `192.128.64.63`/26
     - **Description:** Here, you specify the CIDR block for your subnet. In this case, the subnet CIDR block is set to `192.128.64.63/26`, which allows for 64 IP addresses.
   - **Tags (Optional):**
     - **Field:** Tags
     - **Key:** Name
     - **Value:** `HELLO_SUBNET`
     - **Description:** Tags are optional key-value pairs that you can use to organize, manage, and identify your AWS resources. In this example, a tag with the key "Name" and the value "HELLO_SUBNET" is being added to the subnet.

4. **Additional Actions:**
   - **Button:** Add new tag
     - **Description:** You can click this button to add more tags to your subnet. AWS allows you to add up to 50 tags per resource.
   - **Button:** Remove
     - **Description:** Clicking this button removes the tag.

5. **Add New Subnet:**
   - **Button:** Add new subnet
     - **Description:** If you want to create more subnets within the same VPC, you can click this button to start the process for additional subnets.
    
     # Creating Your Own Virtual Private Cloud (VPC)


# EXAMPLE 1 : Steps to Create a VPC with `192.168.1.0/24`: 

 ## Creating Your Own Virtual Private Cloud (VPC)

 ### Steps to Create a VPC

1. **Open the Amazon VPC Console**
   - Navigate to the [Amazon VPC Console](https://console.aws.amazon.com/vpc/).

2. **Create a VPC**
   - In the left-hand navigation pane, click on "Your VPCs".
   - Click "Create VPC".

3. **Configure the VPC**
   - **Name tag:** Enter a name for your VPC (e.g., `MyVPC`).
   - **IPv4 CIDR block:** Enter `192.168.1.0/24`.
   - **IPv6 CIDR block:** Leave this as default (No IPv6 CIDR Block).
   - **Tenancy:** Default.

4. **Create the VPC**
   - Click "Create VPC".

## Steps to Create a Subnet

1. **Open the Amazon VPC Console**
   - Navigate to the [Amazon VPC Console](https://console.aws.amazon.com/vpc/).

2. **Create a Subnet**
   - In the left-hand navigation pane, click on "Subnets".
   - Click "Create Subnet".

3. **Configure the Subnet**
   - **Subnet Name:**
     - **Field:** Subnet name
     - **Value:** `MySubnet`
     - **Description:** This is where you specify a name for your subnet. The name can be up to 256 characters long and helps you identify the subnet later.
   - **VPC:**
     - **Field:** VPC
     - **Value:** Select the VPC created in Step 1.
   - **Availability Zone:**
     - **Field:** Availability Zone
     - **Value:** No preference
     - **Description:** This dropdown allows you to choose the Availability Zone in which your subnet will reside. If you select "No preference," AWS will choose an appropriate Availability Zone for you.
   - **IPv4 CIDR block:**
     - **Field:** IPv4 CIDR block
     - **Value:** `192.168.1.64/27`
     - **Description:** Here, you specify the CIDR block for your subnet. In this case, the subnet CIDR block is set to `192.168.1.64/27`, which is the third subnet in the range and allows for 32 IP addresses (30 usable).

4. **Tags (Optional):**
   - **Field:** Tags
     - **Key:** Name
     - **Value:** `MySubnet`
     - **Description:** Tags are optional key-value pairs that you can use to organize, manage, and identify your AWS resources.

5. **Additional Actions:**
   - **Button:** Add new tag
     - **Description:** You can click this button to add more tags to your subnet. AWS allows you to add up to 50 tags per resource.
   - **Button:** Remove
     - **Description:** Clicking this button removes the tag.

6. **Add New Subnet:**
   - **Button:** Add new subnet
     - **Description:** If you want to create more subnets within the same VPC, you can click this button to start the process for additional subnets.

7. **Create the Subnet**
   - Click "Create Subnet".

## Subnet Details and Calculation

### Calculate the number of subnets:

- **Original CIDR block:** `192.168.1.0/24`
- **New subnet mask:** `/27`
- **Difference in bits:** `27 - 24 = 3` bits
- **Number of subnets:** `2^3 = 8` subnets

### Calculate the range for each subnet:

Each `/27` subnet will have 32 IP addresses (2^5 = 32), with 30 usable IP addresses (excluding the network address and the broadcast address).

### Subnet Ranges

| Subnet Number | Subnet CIDR     | Range                  |
| --------------| ----------------| -----------------------|
| 1st Subnet    | 192.168.1.0/27  | 192.168.1.0 - 192.168.1.31  |
| 2nd Subnet    | 192.168.1.32/27 | 192.168.1.32 - 192.168.1.63 |
| 3rd Subnet    | 192.168.1.64/27 | 192.168.1.64 - 192.168.1.95 |
| 4th Subnet    | 192.168.1.96/27 | 192.168.1.96 - 192.168.1.127 |
| 5th Subnet    | 192.168.1.128/27| 192.168.1.128 - 192.168.1.159 |
| 6th Subnet    | 192.168.1.160/27| 192.168.1.160 - 192.168.1.191 |
| 7th Subnet    | 192.168.1.192/27| 192.168.1.192 - 192.168.1.223 |
| 8th Subnet    | 192.168.1.224/27| 192.168.1.224 - 192.168.1.255 |

### Detailed Breakdown of the 3rd Subnet

| Detail               | IP Address          |
| -------------------- | ------------------- |
| **Network Address:** | 192.168.1.64        |
| **First Usable IP:** | 192.168.1.65        |
| **Last Usable IP:**  | 192.168.1.94        |
| **Broadcast Address:** | 192.168.1.95      |

