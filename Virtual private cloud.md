# Virtual Private Cloud (VPC) Guide

## Introduction

A Virtual Private Cloud (VPC) is a virtual network that closely resembles a traditional network you would operate in your own data center. This guide will walk you through creating and configuring a VPC, launching an EC2 instance, enabling ICMP, connecting via SSH, detaching the internet gateway, and verifying connectivity.

## ICMP

The Internet Control Message Protocol (ICMP) is a network layer protocol used by network devices to diagnose network communication issues. ICMP is mainly used to determine whether or not data is reaching its intended destination on time.

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

 ## STEP 1 : Creating Your Own Virtual Private Cloud (VPC)

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

# STEP 2 : Steps to Create a Subnet

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

# STEP 3: Additional Networking Settings

When configuring the network settings for your EC2 instance, you need to ensure that you have selected the appropriate VPC and subnet. Below are the detailed steps for setting up the additional networking settings.

### Network Settings

1. **VPC (Virtual Private Cloud)**
   - **Field:** VPC - required
   - **Value:** `vpc-0b7a0895f29e32a6b (VPC_1)`
   - **Description:** Select the VPC where your EC2 instance will reside. In this example, the selected VPC is `VPC_1`.

2. **Subnet**
   - **Field:** Subnet - required
   - **Value:** `subnet-09dfe57d64d6f7958 (subnet1)`
   - **Description:** Choose the subnet within the selected VPC. The subnet chosen here is `subnet1` with the CIDR block `192.168.1.64/27`.

3. **Auto-assign public IP**
   - **Option:** Disable
   - **Description:** Choose whether to auto-assign a public IP address to your instance. Here, it is disabled.

4. **Firewall (Security groups)**
   - **Option:** Select existing security group or create a new one.
   - **Description:** Security groups act as a virtual firewall to control the inbound and outbound traffic to your instance.

5. **Security Group Name**
   - **Field:** Security group name - required
   - **Value:** `launch-wizard-2`
   - **Description:** The name of the security group created or selected for your instance.

6. **Security Group ID**
   - **Field:** Security group ID
   - **Value:** `sg-0a8768a042b493f6d`
   - **Description:** The unique identifier of the security group.

7. **Description**
   - **Field:** Description - optional
   - **Value:** `launch-wizard-2 created 2024-07-05T08:26:29.073+12`
   - **Description:** A description of the security group.

### Inbound Security Group Rules

1. **Rule 1: Allow SSH**
   - **Type:** SSH
   - **Protocol:** TCP
   - **Port range:** 22
   - **Source type:** Anywhere
   - **Source:** `0.0.0.0/0`
   - **Description:** `SSH for admin desktop`
   - **Explanation:** This rule allows SSH access from any IP address to port 22.

2. **Rule 2: Allow ICMP**
   - **Type:** All ICMP - IPv4
   - **Protocol:** ICMP
   - **Port range:** N/A
   - **Source type:** Anywhere
   - **Source:** `0.0.0.0/0`
   - **Description:** `ICMP for admin desktop`
   - **Explanation:** This rule allows ICMP (ping) requests from any IP address.

### Warning

- **Message:**
  `Rules with source of 0.0.0.0/0 allow all IP addresses to access your instance.'
  'We recommend restricting security group rules to allow access from known IP addresses only.`
  
- **Description:** This warning indicates that allowing access from any IP address (`0.0.0.0/0`) can be a security risk, and it's recommended to restrict access to known IP addresses.

### Advanced Network Configuration

- **Option:** Add additional security group rules as needed to fit your security requirements. ```(ALL ICMP IPv4)```

  
# Step 4: Attaching an Internet Gateway

1. Log in to AWS Management Console:
   - Open your browser and go to the AWS Management Console.
   - Enter your credentials and log in.

2. Navigate to VPC Dashboard:
   - Click on 'Services' in the top-left corner.
   - Select 'VPC' from the list of services.

3. Create an Internet Gateway:
   - In the left navigation pane, click on 'Internet Gateways'.
   - Click 'Create internet gateway'.
   - Enter a name for your Internet Gateway.
   - Click 'Create internet gateway'.

4. Attach the Internet Gateway to Your VPC:
   - Select the newly created Internet Gateway.
   - Click 'Actions' > 'Attach to VPC'.
   - Select your VPC from the drop-down list.
   - Click 'Attach internet gateway'.

# Step 5: Associating a Route Table

1. Create a Route Table:
   - In the left navigation pane, click on 'Route Tables'.
   - Click 'Create route table'.
   - Enter a name for your Route Table.
   - Select the VPC you want to associate it with.
   - Click 'Create route table'.

2. Add a Route to the Route Table:
   - Select the newly created Route Table.
   - Click the 'Routes' tab.
   - Click 'Edit routes'.
   - Click 'Add route'.
   - In 'Destination', enter '0.0.0.0/0'.
   - In 'Target', select 'Internet Gateway' and choose your Internet Gateway from the drop-down list.
   - Click 'Save routes'.

3. Associate the Route Table with a Subnet:
   - Select the newly created Route Table.
   - Click the 'Subnet Associations' tab.
   - Click 'Edit subnet associations'.
   - Select the subnet(s) you want to associate with this Route Table.
   - Click 'Save associations'.



