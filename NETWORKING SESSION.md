

 ## SESSION 12: NETWORKING

### AWS VPC (Virtual Private Cloud)
- **What is it?** AWS VPC lets you create a private network in AWS where you can safely set up and manage your resources.

### Network Basics
- **Network:** A system that allows devices to communicate using specific rules called protocols.

### Types of Addresses
1. **MAC Address (Media Access Control):** A unique code assigned to devices for network communication.
2. **IPv4 Address (Internet Protocol version 4):** Commonly used for the front end, looks like this: `192.168.1.1`.
3. **IPv6 Address (Internet Protocol version 6):** Used for the back end, looks like this: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`.

### Commands to Find IP Address
1. **On Windows (Command Prompt):** `ipconfig` - Shows your IP address and network information.
2. **On Linux:** `ifconfig` - Shows network details and IP address (older command).
3. **On Ubuntu:** `ip addr show` - Shows detailed network information and IP addresses (newer command in Ubuntu).

### IANA (Internet Assigned Numbers Authority)
- **What is it?** IANA is responsible for coordinating the global pool of IP addresses and other internet protocol resources.

### Commands for Network Information

1. **getmac:**
   - **Use:** Displays the MAC address of your network interfaces.
   - **Example:** Run `getmac` in the command prompt to see your MAC addresses.

2. **ipconfig /all:**
   - **Use:** Shows detailed information about your network configuration, including all IP addresses.
   - **Example:** Run `ipconfig /all` in the command prompt to get a comprehensive view of your network settings.

3. **Ping:**
   - **Use:** Tests the ability to reach another computer or website on the network.
   - **Example:** Run `ping google.com` to check if you can connect to Google's website. If successful, it shows the connection is working.

4. **tracert:**
   - **Use:** Traces the route to a network host.
   - **Example:** Run `tracert www.google.com` to trace the route to Google's website.

### Internet Control Messaging Protocol (ICMP)
1. ICMP is used for network devices to send error messages and operational information.
2. It does not use a port number.

### IPv4 Addressing
1. An IPv4 address is unique to each device.
   - **Example:** 10.16.57.112
2. Consists of four parts or octets, each ranging from 0 to 255.
3. Each part is represented by 8 bits, so the total length is 32 bits.

### Binary Representation
1. IPv4 addresses can be represented in binary form.
   - **Example:** 170 in binary is 10101010.
2. Conversion process:
   - **Binary:** 10101010
   - **Place values:** 128 64 32 16 8 4 2 1
   - **Calculation:** 128 + 0 + 32 + 0 + 8 + 0 + 2 + 0 = 170

### IPv4 Address Range
1. The minimum IPv4 address is 0.0.0.0.
2. The maximum IPv4 address is 255.255.255.255.
3. The total number of IPv4 addresses is 2^32, which equals 4,294,967,296 addresses.
4. IPv4 address exhaustion occurred in 2003.

### IPv4 Address Classes
1. **Class A:** 0.0.0.0 to 127.255.255.255
2. **Class B:** 128.0.0.0 to 191.255.255.255
3. **Class C:** 192.0.0.0 to 223.255.255.255
4. **Class D:** 224.0.0.0 to 239.255.255.255 (Multicast)
5. **Class E:** 240.0.0.0 to 255.255.255.255 (Experimental)

### Example 1: IP Address of the Following

#### Series 1
We are dealing with IP addresses in the range starting from 1.0.0.0.

- **PC0:** 257th IP Address
  - Starting from 1.0.0.0, the 257th IP address is 1.0.1.0.
- **PC1:** 259th IP Address
  - Starting from 1.0.0.0, the 259th IP address is 1.0.1.2.

#### Series 2
We are dealing with IP addresses in the range starting from 2.0.0.0.

- **PC2:** 100th IP Address
  - Starting from 2.0.0.0, the 100th IP address is 2.0.0.99.
- **PC3:** 200th IP Address
  - Starting from 2.0.0.0, the 200th IP address is 2.0.0.199.

### Example 2: IP Address and Subnet Analysis

#### PC0
- IP Address: 128.1.255.254
- Subnet Mask: 255.255.0.0 (default for Class B)
- Network: 128.1.0.0

#### PC1
- IP Address: 128.1.1.1
- Subnet Mask: 255.255.0.0 (default for Class B)
- Network: 128.1.0.0

#### PC2
- IP Address: 128.2.1.1
- Subnet Mask: 255.255.0.0 (default for Class B)
- Network: 128.2.0.0

#### Why PC0 Cannot Connect with PC2
- PC0 is in the 128.1.0.0 network.
- PC2 is in the 128.2.0.0 network.
- Because they are in different networks (128.1.0.0 vs. 128.2.0.0), they cannot communicate directly without a router to route the traffic between these subnets.

#### Why PC1 Cannot Connect with PC2
- PC1 is in the 128.1.0.0 network.
- PC2 is in the 128.2.0.0 network.
- Similar to the above, since they are in different networks (128.1.0.0 vs. 128.2.0.0), they cannot communicate directly without a router.

#### Why PC0 Can Connect with PC1
- PC0 and PC1 are both in the 128.1.0.0 network.
- Since they share the same network (128.1.0.0), they can communicate directly without any need for routing.


### Example 3: Class C Network Overview
- **Class C IP Address Range**: 192.0.0.0 to 223.255.255.255.
- **Subnet Mask for Class C**: 255.255.255.0.
- Each Class C network has 256 IP addresses (0 to 255 in the last octet).
- The first address is the **network address** (e.g., 192.168.1.0), and the last address is the **broadcast address** (e.g., 192.168.1.255).

### 1. Last IP in C CLASS
- **Definition**: The very last IP address in the entire Class C range.
- **Calculation**:
  - Class C starts from 192.0.0.0 and ends at 223.255.255.255.
  - The last IP address is 223.255.255.255, which is a broadcast address.
- **Answer**: 223.255.255.255.

### 2. LAST NETWORK IN C CLASS
- **Definition**: The last network in the Class C range.
- **Explanation**:
  - Each network in Class C has 256 addresses.
  - The highest network in the Class C range starts at 223.255.255.0.
  - Its subnet mask is 255.255.255.0.
- **Answer**: 223.255.255.0/24.

### 3. 3RD NETWORK IN C CLASS
- **Definition**: The third network address within the Class C range.
- **Explanation**:
  - The first network is 192.0.0.0/24.
  - The second network is 192.0.1.0/24.
  - The third network is 192.0.2.0/24.
- **Answer**: 192.0.2.0/24.

### 4. LAST IP OF 3rd network in C CLASS
- **Definition**: The last usable IP address in the third network of the Class C range.
- **Explanation**:
  - For the third network (192.0.2.0/24), the addresses range from 192.0.2.0 to 192.0.2.255.
  - The network address is 192.0.2.0.
  - The broadcast address is 192.0.2.255.
  - The last usable IP address is just before the broadcast address.
- **Answer**: 192.0.2.254.

### Summary with Examples
- **Last IP in C CLASS**: The very last IP in the Class C range: **223.255.255.255**.
- **LAST NETWORK IN C CLASS**: The highest network in the Class C range: **223.255.255.0/24**.
- **3RD NETWORK IN C CLASS**: The third network in the Class C range: **192.0.2.0/24**.
- **LAST IP OF 3rd network in C CLASS**: The last usable IP of the third Class C network: **192.0.2.254**.


### Network Terms

- **Network:** A group of interconnected devices.
- **Router:** A device that connects multiple networks.
- **Intranet:** A private network accessible only within an organization.
- **Internet:** A global network connecting multiple private and public networks.
- **Examples:**
  - Communicating outside your network is "Internet."
  - Communicating within your network is "Intranet."

### Types of Networks
1. **LAN (Local Area Network):** Connects devices within a small area (e.g., a single building).
2. **WAN (Wide Area Network):** Connects multiple LANs over a large geographic area.

### Network and Host
1. **Network Part:** Identifies the specific network.
2. **Host Part:** Identifies specific devices within the network.
3. **Example structure:** N.H.H.H (One network, three hosts)
   - **N:** Building name
   - **H:** Individual labs or hosts within the building
4. **Important Note:** No IPv4 address starts with 0.

