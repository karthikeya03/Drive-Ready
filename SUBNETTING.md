# Session 17: Subnetting of IP Addresses

## Benefits of Subnetting
- **Reduced Waste**: Efficient use of IP addresses.
- **Increased Security**: Harder for attackers to move between subnets.
- **Reduced Broadcast Traffic**: Only devices in the same subnet receive broadcast messages.

## Example: Allocating 30 IP Addresses To 30 Computers Using Class C

### Problem
Using a Class C network (default mask 255.255.255.0), we get 256 IP addresses. Allocating only 30 addresses wastes 226 IP addresses.

### Steps to Subnetting

#### STEP 1. Identify the Requirement
- **Requirement**: 30 IP addresses

#### STEP 2. Nearest Power of 2
- **Calculation**: \(2^5 = 32\)
  - Formula: \(2^n - 2\) (subtracting 2 for network and broadcast IDs)
  - For 30 addresses, we need 32 IP addresses.

#### STEP 3. Write the New Subnet Mask
- **Default Subnet Mask**: 255.255.255.0
  - This provides 256 IP addresses (slash value is /24).

- **Change to Fit Requirement**:
  - We need only 30 addresses, so we adjust the subnet mask.
  - Binary Representation:
    - Default: 11111111.11111111.11111111.00000000 (8 host bits)
    - Required: 11111111.11111111.11111111.11100000 (3 new network bits + 5 host bits)

- **New Subnet Mask**:
  - Convert the new mask to decimal: 255.255.255.224
  - New slash value: /27

#### STEP 4. Number of Hosts and Networks
- **Number of Hosts**: \(2^5 = 32\)
- **Number of Networks**: \(2^3 = 8\) (number of converted network bits)
- The large network is split into 8 subnets, each with 32 addresses, reducing waste.

#### STEP 5. Writing the Range
- **Range Calculation**: Based on \(2^5 = 32\) hosts per subnet.

| No. of Hosts | No. of Networks |
|--------------|-----------------|
| 32           | 8               |

#### Subnet Ranges

| Subnet        | Network ID     | Usable IP Range               | Broadcast ID       |
|---------------|----------------|-------------------------------|--------------------|
| Subnet 1      | 192.168.10.0   | 192.168.10.1 - 192.168.10.30   | 192.168.10.31      |
| Subnet 2      | 192.168.10.32  | 192.168.10.33 - 192.168.10.62  | 192.168.10.63      |
| Subnet 3      | 192.168.10.64  | 192.168.10.65 - 192.168.10.94  | 192.168.10.95      |
| Subnet 4      | 192.168.10.96  | 192.168.10.97 - 192.168.10.126 | 192.168.10.127     |
| Subnet 5      | 192.168.10.128 | 192.168.10.129 - 192.168.10.158| 192.168.10.159     |
| Subnet 6      | 192.168.10.160 | 192.168.10.161 - 192.168.10.190| 192.168.10.191     |
| Subnet 7      | 192.168.10.192 | 192.168.10.193 - 192.168.10.222| 192.168.10.223     |
| Subnet 8      | 192.168.10.224 | 192.168.10.225 - 192.168.10.254| 192.168.10.255     |

### Powers of 2
![POWERS OF 2](https://raw.github.com/karthikeya03/IMAGES/JustMain/123.png)

## Example 2: Allocating 16 IP Addresses TO 16 COMPUTERS Using C Class :

### Problem
Given the requirement of 16 IP addresses, follow the subnetting steps.

#### STEP 1. Identify the Requirement
- **Requirement**: 16 IP addresses

#### STEP 2. Nearest Power of 2
- **Calculation**: \(2^4 = 16\)

#### STEP 3. Write the New Subnet Mask
- **Default Subnet Mask**: 255.255.255.0

- **Change to Fit Requirement**:
  - Adjust the subnet mask to accommodate 16 addresses.
  - Binary Representation:
    - Default: 11111111.11111111.11111111.00000000
    - Required: 11111111.11111111.11111111.11110000 (4 new network bits + 4 host bits)

- **New Subnet Mask**:
  - Convert the new mask to decimal: 255.255.255.240
  - New slash value: /28

#### STEP 4. Number of Hosts and Networks
- **Number of Hosts**: \(2^4 = 16\)
- **Number of Networks**: \(2^4 = 16\)

#### STEP 5. Writing the Range
- **Range Calculation**: Based on \(2^4 = 16\) hosts per subnet.

| No. of Hosts | No. of Networks |
|--------------|-----------------|
| 16           | 16              |

#### Subnet Ranges

| Subnet        | Network ID     | Usable IP Range               | Broadcast ID       |
|---------------|----------------|-------------------------------|--------------------|
| Subnet 1      | 192.168.10.0   | 192.168.10.1 - 192.168.10.14   | 192.168.10.15      |
| Subnet 2      | 192.168.10.16  | 192.168.10.17 - 192.168.10.30  | 192.168.10.31      |
| Subnet 3      | 192.168.10.32  | 192.168.10.33 - 192.168.10.46  | 192.168.10.47      |
| Subnet 4      | 192.168.10.48  | 192.168.10.49 - 192.168.10.62  | 192.168.10.63      |
| Subnet 5      | 192.168.10.64  | 192.168.10.65 - 192.168.10.78  | 192.168.10.79      |
| Subnet 6      | 192.168.10.80  | 192.168.10.81 - 192.168.10.94  | 192.168.10.95      |
| Subnet 7      | 192.168.10.96  | 192.168.10.97 - 192.168.10.110 | 192.168.10.111     |
| Subnet 8      | 192.168.10.112 | 192.168.10.113 - 192.168.10.126| 192.168.10.127     |
| Subnet 9      | 192.168.10.128 | 192.168.10.129 - 192.168.10.142| 192.168.10.143     |
| Subnet 10     | 192.168.10.144 | 192.168.10.145 - 192.168.10.158| 192.168.10.159     |
| Subnet 11     | 192.168.10.160 | 192.168.10.161 - 192.168.10.174| 192.168.10.175     |
| Subnet 12     | 192.168.10.176 | 192.168.10.177 - 192.168.10.190| 192.168.10.191     |
| Subnet 13     | 192.168.10.192 | 192.168.10.193 - 192.168.10.206| 192.168.10.207     |
| Subnet 14     | 192.168.10.208 | 192.168.10.209 - 192.168.10.222| 192.168.10.223     |
| Subnet 15     | 192.168.10.224 | 192.168.10.225 - 192.168.10.238| 192.168.10.239     |
| Subnet 16     | 192.168.10.240 | 192.168.10.241 - 192.168.10.254| 192.168.10.255     |

## Summary

### Initial Setup
- **Class C Network**: 192.168.1.0
- **Default Subnet Mask**: 255.255.255.0 (/24)
- **Usable IPs**: 254
- **Wasted IPs**: 224 (if only 30 are used)

### Subnetting Steps
1. **Requirement**: 30 IP addresses
2. **Calculation**: \(2^5 = 32\) (30 usable, 2 reserved)
3. **New Subnet Mask**: 255.255.255.224 (/27)
4. **Usable IP Range**: 32 - 2 = 30 addresses

### Benefits of Subnetting
- Efficient IP usage
- Enhanced security
- Reduced broadcast traffic

By subnetting, we create a network with exactly the number of IP addresses needed, minimizing waste and optimizing performance.

# Example: Understanding Subnet Mask and IP Address Communication

## Scenario

### Network 1
- **IP Addresses**: 192.168.10.1 and 192.168.10.30
- **Subnet Mask**: 255.255.255.0 (/24)

### Network 2
- **IP Addresses**: 192.168.10.1 and 192.168.10.30
- **Subnet Mask**: 255.255.255.224 (/27)

## Explanation

### Network 1: Subnet Mask 255.255.255.0 (/24)

- **Subnet Mask**: 255.255.255.0
- **Binary Representation**: 11111111.11111111.11111111.00000000
- **Network Portion**: First 24 bits (192.168.10)
- **Host Portion**: Last 8 bits (0 to 255)

**IP Range for /24 Network**: 192.168.10.0 - 192.168.10.255

- **192.168.10.1** and **192.168.10.30** fall within this range.
- **Conclusion**: Both IPs are in the same subnet, so they can communicate directly.

### Network 2: Subnet Mask 255.255.255.224 (/27)

- **Subnet Mask**: 255.255.255.224
- **Binary Representation**: 11111111.11111111.11111111.11100000
- **Network Portion**: First 27 bits (192.168.10.x, where x is 0 to 31, 32 to 63, etc.)
- **Host Portion**: Last 5 bits (0 to 31, 32 to 63, etc.)

**IP Range for /27 Network**:

| Subnet      | Network ID     | Usable IP Range                | Broadcast ID       |
|-------------|----------------|--------------------------------|--------------------|
| Subnet 1    | 192.168.10.0   | 192.168.10.1 - 192.168.10.30    | 192.168.10.31      |
| Subnet 2    | 192.168.10.32  | 192.168.10.33 - 192.168.10.62   | 192.168.10.63      |
| Subnet 3    | 192.168.10.64  | 192.168.10.65 - 192.168.10.94   | 192.168.10.95      |

- **192.168.10.1** is in the first subnet (192.168.10.0/27).
- **192.168.10.30** is also in the first subnet (192.168.10.0/27).

**Conclusion for Different IP Ranges**:
- If we consider IPs that fall into different subnets, they will not communicate directly.
- Example: 
  - **192.168.10.1** is in 192.168.10.0/27 (1st subnet).
  - **192.168.10.33** is in 192.168.10.32/27 (2nd subnet).

### Why Doesn't 192.168.10.1 Ping 192.168.10.33 in /27?
- **Different Subnets**: 192.168.10.1 (Subnet 1: 192.168.10.0/27) and 192.168.10.33 (Subnet 2: 192.168.10.32/27) are in different subnets.
- **Routing Required**: Communication between different subnets requires routing.

### Summary

- **Subnet Mask /24**: IPs 192.168.10.1 and 192.168.10.30 can ping each other because they are in the same subnet.
- **Subnet Mask /27**: IPs 192.168.10.1 and 192.168.10.33 cannot ping each other directly because they are in different subnets.
