# SESSION 16: CLASSFUL IP ADDRESSING 

## Definition
Classful IP addressing refers to the method of assigning IP addresses using a default subnet mask or default prefix length as defined by IANA. In this method, the subnet mask is fixed and cannot be altered.

## Private IP Address Range - RFC 1918
- **10.0.0.0 - 10.255.255.255**
- **172.16.0.0 - 172.31.255.255**
- **192.168.0.0 - 192.168.255.255**

These ranges are reserved for private use within local networks and are not routable on the public internet.

## Subnet Masks of Different Classes
Classful addressing divides IP addresses into five classes (A, B, C, D, and E). The primary classes used for networking are A, B, and C. Each class has a default subnet mask.

1. **Class A:**
   - Subnet Mask: `255.0.0.0`
   - Notation: `n.h.h.h` (where `n` is the network part and `h` is the host part)
   - Prefix Length: `/8` (8 bits for the network)

2. **Class B:**
   - Subnet Mask: `255.255.0.0`
   - Notation: `n.n.h.h`
   - Prefix Length: `/16` (16 bits for the network)

3. **Class C:**
   - Subnet Mask: `255.255.255.0`
   - Notation: `n.n.n.h`
   - Prefix Length: `/24` (24 bits for the network)

![subnet](https://raw.github.com/karthikeya03/IMAGES/JustMain/SUB.png))

### Prefix Length
The prefix length indicates the number of bits used for the network portion of the address. The remaining bits are used for host addresses within the network.

- **Class A:**
  - Subnet Mask: `255.0.0.0`
  - Number of Network Bits: `8`
  - Number of Host Bits: `24`
  - Network Range: `1.0.0.0 - 126.255.255.255` (excluding `127.0.0.0` reserved for loopback)

- **Class B:**
  - Subnet Mask: `255.255.0.0`
  - Number of Network Bits: `16`
  - Number of Host Bits: `16`
  - Network Range: `128.0.0.0 - 191.255.255.255`

- **Class C:**
  - Subnet Mask: `255.255.255.0`
  - Number of Network Bits: `24`
  - Number of Host Bits: `8`
  - Network Range: `192.0.0.0 - 223.255.255.255`

## Concept of Telecommunication
Telecommunication refers to the transmission of signals over a distance for communication. In the context of IP addressing, it involves the use of IP addresses to facilitate the routing and delivery of data packets across networks.

Classful IP addressing has largely been replaced by classless inter-domain routing (CIDR), which allows for a more flexible and efficient allocation of IP addresses. However, understanding classful addressing provides a foundational knowledge of how IP addressing originally worked and is essential for grasping more advanced concepts in networking.

# IP Address Allocation Guide

## Overview
To allocate IP addresses efficiently for various network sizes, it's important to understand the different classes of IP addresses and their characteristics. This guide provides a detailed explanation of Class A, B, and C networks, their subnetting, and examples of allocating IP addresses for different numbers of devices.

## Class C Network
Class C networks are suitable for small networks. They provide up to 254 usable IP addresses.

- **Default Subnet Mask**: `255.255.255.0`
- **Number of Bits for Host**: 8 bits
- **Usable IP Addresses**: \(2^8 - 2 = 256 - 2 = 254\)

### Example: Allocating 30 IP Addresses
To allocate 30 IP addresses, use a /27 subnet mask.

- **Subnet Mask**: `255.255.255.224` (/27)
- **Number of Usable IP Addresses**: \(2^5 - 2 = 32 - 2 = 30\)
- **Network Address**: `192.168.1.0/27`
- **Usable IP Range**: `192.168.1.1` to `192.168.1.30`
- **Broadcast Address**: `192.168.1.31`

## Class B Network
Class B networks are suitable for medium-sized networks. They provide up to 65,534 usable IP addresses.

- **Default Subnet Mask**: `255.255.0.0`
- **Number of Bits for Host**: 16 bits
- **Usable IP Addresses**: \(2^{16} - 2 = 65,536 - 2 = 65,534\)

### Example: Allocating 300 IP Addresses
To allocate 300 IP addresses, use a /23 subnet mask.

- **Subnet Mask**: `255.255.254.0` (/23)
- **Number of Usable IP Addresses**: \(2^9 - 2 = 512 - 2 = 510\)
- **Network Address**: `172.16.0.0/23`
- **Usable IP Range**: `172.16.0.1` to `172.16.1.254`
- **Broadcast Address**: `172.16.1.255`

## Class A Network
Class A networks are suitable for large networks. They provide up to 16,777,214 usable IP addresses.

- **Default Subnet Mask**: `255.0.0.0`
- **Number of Bits for Host**: 24 bits
- **Usable IP Addresses**: \(2^{24} - 2 = 16,777,216 - 2 = 16,777,214\)

### Example: Allocating 5000 IP Addresses
To allocate 5000 IP addresses, use a /19 subnet mask.

- **Subnet Mask**: `255.255.224.0` (/19)
- **Number of Usable IP Addresses**: \(2^{13} - 2 = 8192 - 2 = 8190\)
- **Network Address**: `10.0.0.0/19`
- **Usable IP Range**: `10.0.0.1` to `10.0.31.254`
- **Broadcast Address**: `10.0.31.255`

## Summary Table

| Network Class | Default Subnet Mask | Usable IP Addresses | Example Subnet Mask | Usable IPs in Example Subnet | Example Network Address | Example Usable IP Range         | Example Broadcast Address |
|---------------|---------------------|---------------------|---------------------|-----------------------------|--------------------------|---------------------------------|----------------------------|
| Class C       | 255.255.255.0       | 254                 | 255.255.255.224 (/27) | 30                          | 192.168.1.0/27          | 192.168.1.1 - 192.168.1.30     | 192.168.1.31              |
| Class B       | 255.255.0.0         | 65,534              | 255.255.254.0 (/23)  | 510                         | 172.16.0.0/23           | 172.16.0.1 - 172.16.1.254      | 172.16.1.255              |
| Class A       | 255.0.0.0           | 16,777,214          | 255.255.224.0 (/19)  | 8190                        | 10.0.0.0/19             | 10.0.0.1 - 10.0.31.254         | 10.0.31.255               |

## Conclusion
By understanding the characteristics and capabilities of different IP address classes, you can efficiently allocate IP addresses for networks of various sizes. Class C is suitable for small networks, Class B for medium-sized networks, and Class A for large networks.


# Why Full IP Addressing is Not Recommended

## Overview
Using a single large IP address space for an entire network can cause problems. It's better to divide the network into smaller parts called subnets. Here's why.

## Problems with Full IP Addressing

### 1. Too Much Traffic
- **Problem**: All devices receive every broadcast message, slowing down the network.
- **Example**: Imagine everyone in a classroom talking at the same time. It gets noisy and hard to understand anything.

### 2. Security Issues
- **Problem**: If one part of the network is hacked, the whole network is at risk.
- **Example**: If someone sneaks into a house, they can go to any room. But if each room has a lock, it's harder to access other rooms.

### 3. Hard to Manage
- **Problem**: Managing a large network is complex and confusing.
- **Example**: Keeping track of everyone's phone number in a big city is harder than in a small town.

### 4. Wasted IP Addresses
- **Problem**: Many IP addresses might not be used, wasting resources.
- **Example**: Like having a giant pizza and only eating two slices.

## Benefits of Subnetting

### 1. Less Traffic
- **Benefit**: Only devices in the same subnet receive broadcast messages.
- **Example**: In smaller groups, conversations are easier and clearer.

### 2. Better Security
- **Benefit**: Harder for attackers to move between subnets.
- **Example**: Each room in a house has a lock, so intruders can't easily get into other rooms.

### 3. Easier Management
- **Benefit**: Smaller networks are easier to handle.
- **Example**: Managing phone numbers in a small town is simpler.

### 4. Efficient Use of IP Addresses
- **Benefit**: Allocates just the right amount of IP addresses needed.
- **Example**: Ordering a pizza that’s just the right size.

## Example: Subnetting a Network

### Scenario
You have a network with 10 devices.

### Full IP Addressing
- **Network**: `192.168.0.0/24`
- **Usable IPs**: 254
- **Problems**: Too much traffic, security risks, hard to manage, wasted IP addresses.

### Subnetting Approach
- **Subnet 1**: `192.168.0.0/28`
  - **Usable IPs**: 14
  - **Devices**: 7
- **Subnet 2**: `192.168.0.16/28`
  - **Usable IPs**: 14
  - **Devices**: 3

### Benefits of Subnetting
- **Less Traffic**: Devices in `192.168.0.0/28` don't hear broadcasts from `192.168.0.16/28`.
- **Better Security**: An attacker in one subnet can't easily reach the other.
- **Easier Management**: Smaller subnets are simpler to manage.
- **Efficient Use of IPs**: Only the necessary IP addresses are used.

## Summary Table

| Full IP Addressing          | Subnetting                         |
|-----------------------------|------------------------------------|
| Too much traffic            | Less traffic                       |
| Security risks              | Better security                    |
| Hard to manage              | Easier management                  |
| Wasted IP addresses         | Efficient use of IP addresses      |

## Conclusion
Subnetting helps in reducing network traffic, enhancing security, making management easier, and using IP addresses efficiently. It's like organizing a big task into smaller, manageable parts.


