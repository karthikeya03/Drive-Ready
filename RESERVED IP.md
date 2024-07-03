# SESSION 15: IP Address Classes and Networking

## IP Address Classes

IP addresses are divided into classes to accommodate different network sizes. The classes are A, B, C, D, and E.

### Class A
- **Range:** `1.0.0.0` to `126.0.0.0`
- **Default Subnet Mask:** `255.0.0.0`
- **Number of Networks:** 128 (2^7, considering network address 0 is reserved)
- **Number of Hosts per Network:** 16,777,214 (2^24 - 2)

### Class B
- **Range:** `128.0.0.0` to `191.255.0.0`
- **Default Subnet Mask:** `255.255.0.0`
- **Number of Networks:** 16,384 (2^14)
- **Number of Hosts per Network:** 65,534 (2^16 - 2)

### Class C
- **Range:** `192.0.0.0` to `223.255.255.0`
- **Default Subnet Mask:** `255.255.255.0`
- **Number of Networks:** 2,097,152 (2^21)
- **Number of Hosts per Network:** 254 (2^8 - 2)

### Class D (Multicast)
- **Range:** `224.0.0.0` to `239.255.255.255`
- **Purpose:** Used for multicast groups
- **No subnet mask** as it's not used for traditional IP networks.

### Class E (Reserved)
- **Range:** `240.0.0.0` to `255.255.255.255`
- **Purpose:** Reserved for future use or research and development

## Network and Host Identification

An IP address is divided into two parts:
1. **Network ID:** Identifies the specific network.
2. **Host ID:** Identifies the specific device on the network.

### Example of Class B Network:
- **IP Address:** `172.16.45.1`
- **Network ID:** `172.16`
- **Host ID:** `45.1`

## Tables for Reference

| Class | Range | Default Subnet Mask | Number of Networks | Number of Hosts per Network |
|-------|-------|---------------------|--------------------|----------------------------|
| A     | `1.0.0.0` to `126.0.0.0` | `255.0.0.0` | 128 | 16,777,214 |
| B     | `128.0.0.0` to `191.255.0.0` | `255.255.0.0` | 16,384 | 65,534 |
| C     | `192.0.0.0` to `223.255.255.0` | `255.255.255.0` | 2,097,152 | 254 |
| D     | `224.0.0.0` to `239.255.255.255` | N/A | Multicast only | N/A |
| E     | `240.0.0.0` to `255.255.255.255` | N/A | Reserved | N/A |

## Images for Better Understanding

> **IP Address Classes:**
>
> ![IP Address Classes](https://raw.github.com/karthikeya03/IMAGES/JustMain/2.jpeg)

> **Network and Host Portions:**
>
> ![Network and Host Portions](https://raw.github.com/karthikeya03/IMAGES/JustMain/1.gif)

## Summary

- **Class A, B, C:** Used for unicast communication.
- **Class D:** Used for multicast groups.
- **Class E:** Reserved for future use.
- **Network ID:** Identifies the network.
- **Host ID:** Identifies a device within the network.

Understanding these basics helps in designing and managing IP networks effectively.

## Network ID and Broadcast ID

- `0.0.0.0`: A network IP representing the first network, cannot be used to represent a computer.
- `1.0.0.0`: The first network IP of the first class.
- `5.0.0.0`: The first network IP of the fifth class.
- These cannot be used to represent a computer and cannot be provided as an IP address.
- `255.255.255.255`: Called a broadcast IP.

# IP Address Examples :

## Example 1 :
This example demonstrates the IP address allocation within a given IP range, specifically focusing on finding specific usable IP addresses. The given IP address falls within a range, and the example identifies the first, last, and 256th usable IP addresses.

- **IP Address:** `10.250.67.89`
- **First Usable IP:** `10.0.0.1`
  - This is the first IP address that can be assigned to a host in the network.
- **Last Usable IP:** `10.255.255.254`
  - This is the last IP address that can be assigned to a host in the network.
- **256th Usable IP:** `10.0.1.0`
  - This is the 256th IP address that can be assigned to a host in the network.

## Example 2:
This example shows how to determine the network ID and broadcast ID from a given IP address in the Class B network. The network ID represents the starting address of the network, while the broadcast ID represents the last address that can be reached within the network.

- **IP Address:** `172.254.89.67`
- **Network ID:** `172.254.0.0`
  - This is the base address of the network, which all IPs in this range share.
- **Broadcast ID:** `172.254.255.255`
  - This is the address used to send data to all possible destinations within the network.

## Example 3
This example explains the characteristics of a Class B network. It outlines the network ID, the 257th network, the broadcast ID, the 258th usable IP, and the last usable IP within the network.

> **CLASS B:** `128 to 191`

- **Network ID:** `129.0.0.0`
  - This is the base address for the given network.
- **257th Network:** `129.0.0.0`
  - The 257th network starts at the same base address `129.0.0.0` since network IDs do not change with individual IP assignments within a given network.
- **Broadcast ID:** `129.0.255.255`
  - This is the address used to send data to all hosts within the `129.0.x.x` network.
- **258th Usable IP:** `129.0.1.2`
  - This is the 258th IP address that can be assigned to a host in the network.
- **Last Usable IP:** `129.0.255.254`
  - This is the last IP address that can be assigned to a host in the network.
