# Session 17: Subnetting of IP Addresses

## Benefits of Subnetting
- **Reduced Waste**: Efficient use of IP addresses.
- **Increased Security**: Harder for attackers to move between subnets.
- **Reduced Broadcast Traffic**: Only devices in the same subnet receive broadcast messages.

## Example: Allocating 30 IP Addresses Using Class C

### Problem
Using a Class C network (default mask `255.255.255.0`), we get 256 IP addresses. Allocating only 30 addresses wastes 226 IP addresses.

### Steps to Subnetting

#### 1. Identify the Requirement
- **Requirement**: 30 IP addresses

#### 2. Nearest Power of 2
- **Calculation**: \(2^5 = 32\)
  - Formula: \(2^n - 2\) (subtracting 2 for network and broadcast IDs)
  - For 30 addresses, we need 32 IP addresses.

#### 3. Write the New Subnet Mask
- **Default Subnet Mask**: `255.255.255.0`
  - This provides 256 IP addresses (slash value is /24).

- **Change to Fit Requirement**:
  - We need only 30 addresses, so we adjust the subnet mask.
  - Binary Representation:
    - Default: `11111111.11111111.11111111.00000000` (8 host bits)
    - Required: `11111111.11111111.11111111.11100000` (3 new network bits + 5 host bits)

- **New Subnet Mask**:
  - Convert the new mask to decimal: `255.255.255.224`
  - New slash value: `/27`

### 4. Number of Hosts and Networks
- **Number of Hosts**: \(2^5 = 32\)
- **Number of Networks**: \(2^3 = 8\) (number of converted network bits)
- The large network is split into 8 subnets, each with 32 addresses, reducing waste.

### 5. Writing the Range
- **Range Calculation**: Based on \(2^5 = 32\) hosts per subnet.

| No. of Hosts | No. of Networks |
|--------------|-----------------|
| 32           | 8               |

#### Subnet Ranges

| Subnet        | Network ID     | Usable IP Range               | Broadcast ID       |
|---------------|----------------|-------------------------------|--------------------|
| Subnet 1      | `192.168.10.0` | `192.168.10.1 - 192.168.10.30`| `192.168.10.31`    |
| Subnet 2      | `192.168.10.32`| `192.168.10.33 - 192.168.10.62`| `192.168.10.63`   |
| Subnet 3      | `192.168.10.64`| `192.168.10.65 - 192.168.10.94`| `192.168.10.95`   |
| Subnet 4      | `192.168.10.96`| `192.168.10.97 - 192.168.10.126`| `192.168.10.127` |
| Subnet 5      | `192.168.10.128`| `192.168.10.129 - 192.168.10.158`| `192.168.10.159`|
| Subnet 6      | `192.168.10.160`| `192.168.10.161 - 192.168.10.190`| `192.168.10.191`|
| Subnet 7      | `192.168.10.192`| `192.168.10.193 - 192.168.10.222`| `192.168.10.223`|
| Subnet 8      | `192.168.10.224`| `192.168.10.225 - 192.168.10.254`| `192.168.10.255`|

### Visual Aid: Powers of 2
![POWERS OF 2](https://raw.github.com/karthikeya03/IMAGES/JustMain/123.png)

## Summary

### Initial Setup
- **Class C Network**: `192.168.1.0`
- **Default Subnet Mask**: `255.255.255.0` (/24)
- **Usable IPs**: 254
- **Wasted IPs**: 224 (if only 30 are used)

### Subnetting Steps
1. **Requirement**: 30 IP addresses
2. **Calculation**: \(2^5 = 32\) (30 usable, 2 reserved)
3. **New Subnet Mask**: `255.255.255.224` (/27)
4. **Usable IP Range**: 32 - 2 = 30 addresses

### Benefits of Subnetting
- Efficient IP usage
- Enhanced security
- Reduced broadcast traffic

By subnetting, we create a network with exactly the number of IP addresses needed, minimizing waste and optimizing performance.
