# SESSION 13: NETWORKING

## AWS VPC (Virtual Private Cloud)
- **What is it?** AWS VPC lets you create a private network in AWS where you can safely set up and manage your resources.

## Network Basics
- **Network:** A system that allows devices to communicate using specific rules called protocols.

## Types of Addresses

1. **MAC Address (Media Access Control):** 
   - A unique code assigned to devices for network communication.

2. **IPv4 Address (Internet Protocol version 4):**
   - Commonly used for the front end, looks like this: `192.168.1.1`.

3. **IPv6 Address (Internet Protocol version 6):**
   - Used for the back end, looks like this: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`.

## Commands to Find IP Address

1. **On Windows (Command Prompt):**
   - `ipconfig` - Shows your IP address and network information.

2. **On Linux:**
   - `ifconfig` - Shows network details and IP address (older command).

3. **On Ubuntu:**
   - `ip addr show` - Shows detailed network information and IP addresses (newer command in Ubuntu).

## IANA (Internet Assigned Numbers Authority)
- **What is it?** IANA is responsible for coordinating the global pool of IP addresses and other internet protocol resources.

## Commands for Network Information

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

## Internet Control Messaging Protocol (ICMP)

1. **What is it?** ICMP is used for network devices to send error messages and operational information.
2. **Note:** It does not use a port number.

## IPv4 Addressing

1. An IPv4 address is unique to each device.
   - **Example:** `10.16.57.112`

2. Consists of four parts or octets, each ranging from 0 to 255.

3. Each part is represented by 8 bits, so the total length is 32 bits.

## Binary Representation

1. **IPv4 addresses can be represented in binary form.**
   - **Example:** `170` in binary is `10101010`.

2. **Conversion process:**
   - **Binary:** `10101010`
   - **Place values:** `128 64 32 16 8 4 2 1`
   - **Calculation:** `128 + 0 + 32 + 0 + 8 + 0 + 2 + 0 = 170`

## IPv4 Address Range

1. The minimum IPv4 address is `0.0.0.0`.
2. The maximum IPv4 address is `255.255.255.255`.
3. The total number of IPv4 addresses is `2^32`, which equals `4,294,967,296` addresses.
4. **IPv4 address exhaustion occurred in 2003.**

## IPv4 Address Classes

| Class | Address Range              | Description        |
|-------|----------------------------|--------------------|
| A     | `0.0.0.0` to `127.255.255.255` | Large networks     |
| B     | `128.0.0.0` to `191.255.255.255` | Medium networks    |
| C     | `192.0.0.0` to `223.255.255.255` | Small networks     |
| D     | `224.0.0.0` to `239.255.255.255` | Multicast          |
| E     | `240.0.0.0` to `255.255.255.255` | Experimental       |

# IP Address Classes and Default Subnet Masks

| IP Address Class | Default Subnet Mask   |
|------------------|-----------------------|
| Class A          | 255.0.0.0             |
| Class B          | 255.255.0.0           |
| Class C          | 255.255.255.0         |
| Class D          | Not defined           |
| Class E          | Not defined           |


## Example 1: IP Address of the Following

### Series 1
We are dealing with IP addresses in the range starting from `1.0.0.0`.

- **PC0:** 257th IP Address
  - Starting from `1.0.0.0`, the 257th IP address is `1.0.1.0`.
- **PC1:** 259th IP Address
  - Starting from `1.0.0.0`, the 259th IP address is `1.0.1.2`.

### Series 2
We are dealing with IP addresses in the range starting from `2.0.0.0`.

- **PC2:** 100th IP Address
  - Starting from `2.0.0.0`, the 100th IP address is `2.0.0.99`.
- **PC3:** 200th IP Address
  - Starting from `2.0.0.0`, the 200th IP address is `2.0.0.199`.

## Example 2: IP Address and Subnet Analysis

### PC0
- **IP Address:** `128.1.255.254`
- **Subnet Mask:** `255.255.0.0` (default for Class B)
- **Network:** `128.1.0.0`

### PC1
- **IP Address:** `128.1.1.1`
- **Subnet Mask:** `255.255.0.0` (default for Class B)
- **Network:** `128.1.0.0`

### PC2
- **IP Address:** `128.2.1.1`
- **Subnet Mask:** `255.255.0.0` (default for Class B)
- **Network:** `128.2.0.0`

### Why PC0 Cannot Connect with PC2
- **PC0** is in the `128.1.0.0` network.
- **PC2** is in the `128.2.0.0` network.
- **Explanation:** Because they are in different networks (`128.1.0.0` vs. `128.2.0.0`), they cannot communicate directly without a router to route the traffic between these subnets.

### Why PC1 Cannot Connect with PC2
- **PC1** is in the `128.1.0.0` network.
- **PC2** is in the `128.2.0.0` network.
- **Explanation:** Similar to the above, since they are in different networks (`128.1.0.0` vs. `128.2.0.0`), they cannot communicate directly without a router.

### Why PC0 Can Connect with PC1
- **PC0** and **PC1** are both in the `128.1.0.0` network.
- **Explanation:** Since they share the same network (`128.1.0.0`), they can communicate directly without any need for routing.

## Example 3: Class C Network Overview

- **Class C IP Address Range:** `192.0.0.0` to `223.255.255.255`.
- **Subnet Mask for Class C:** `255.255.255.0`.
- Each Class C network has `256` IP addresses (0 to 255 in the last octet).
- The first address is the **network address** (e.g., `192.168.1.0`), and the last address is the **broadcast address** (e.g., `192.168.1.255`).

## Summary of IPv4 Address Classes

1. **10th Network in Class A**: `10.0.0.0`
2. **260th IP Address in the 10th Network**: `10.0.1.3`
3. **Number of Hosts in the 10th Network**: `16,777,216`
4. **Number of Networks in Class A**: `126`

5. **5th Network in Class B**: `128.4.0.0`
6. **256th IP Address in the 5th Network**: `128.4.0.255`
7. **Number of Hosts in the 5th Network**: `65,536`
8. **Number of Networks in Class B**: `64`

## Example 4: Class A and Class B Network Overview

### Class A Network

1. **10th Network in Class A**
   - **Definition:** The 10th network in the Class A IP range.
   - **Calculation:** Class A networks start from `10.0.0.0`.
   - **Answer:** `10.0.0.0`.

2. **260th IP Address in the 10th Network**
   - **Definition:** The 260th IP address within the 10th network.
   - **Calculation:** Counting from `10.0.0.0`, the 260th address is `10.0.1.3`.
   - **Answer:** `10.0.1.3`.

3. **Number of Hosts in the 10th Network**
   - **Definition:** The total number of usable addresses in the 10th network.
   - **Calculation:** Subtracting network and broadcast addresses from total IPs.
   - **Answer:** `16,777,216` total IP addresses, minus 2 for network and broadcast addresses.

4. **Number of Networks in Class A**
   - **Definition:** Total possible networks within Class A range.
   - **Calculation:** `2^7` or `128` total networks, minus 2 (0 and 127 are reserved).
   - **Answer:** `126`.

### Class B Network

1. **5th Network in Class B**
   - **Definition:** The 5th network in the Class B IP range.
   - **Calculation:** Class B networks start from `128.0.0.0`.
   - **Answer:** `128.4.0.0`.

2. **256th IP Address in the 5th Network**
   - **Definition:** The 256th IP address within the 5th network.
   - **Calculation:** Counting from `128.4.0.0`, the 256th address is `128.4.0.255`.
   - **Answer:** `128.4.0.255`.

3. **Number of Hosts in the 5th Network**
   - **Definition:** The total number of usable addresses in the 5th network.
   - **Calculation:** Subtracting network and broadcast addresses from total IPs.
   - **Answer:** `65,536` total IP addresses, minus 2 for network and broadcast addresses.

4. **Number of Networks in Class B**
   - **Definition:** Total possible networks within Class B range.
   - **Calculation:** `2^14` or `16,384` total networks.
   - **Answer:** `16,384`.

---

This summary includes an overview of the networking concepts and examples covered in the session, along with details about IPv4 addressing and the various classes of IP addresses.
