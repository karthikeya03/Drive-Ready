# SESSION 15 : IP Address Classes and Networking

# IP Address Classes and Networking

## IP Address Classes

IP addresses are divided into classes to accommodate different network sizes. The classes are A, B, C, D, and E.

### Class A
- **Range:** 1.0.0.0 to 126.0.0.0
- **Default Subnet Mask:** 255.0.0.0
- **Number of Networks:** 128 (2^7, considering network address 0 is reserved)
- **Number of Hosts per Network:** 16,777,214 (2^24 - 2)

### Class B
- **Range:** 128.0.0.0 to 191.255.0.0
- **Default Subnet Mask:** 255.255.0.0
- **Number of Networks:** 16,384 (2^14)
- **Number of Hosts per Network:** 65,534 (2^16 - 2)

### Class C
- **Range:** 192.0.0.0 to 223.255.255.0
- **Default Subnet Mask:** 255.255.255.0
- **Number of Networks:** 2,097,152 (2^21)
- **Number of Hosts per Network:** 254 (2^8 - 2)

### Class D (Multicast)
- **Range:** 224.0.0.0 to 239.255.255.255
- **Purpose:** Used for multicast groups
- **No subnet mask** as it's not used for traditional IP networks.

### Class E (Reserved)
- **Range:** 240.0.0.0 to 255.255.255.255
- **Purpose:** Reserved for future use or research and development

## Network and Host Identification

An IP address is divided into two parts:
1. **Network ID:** Identifies the specific network.
2. **Host ID:** Identifies the specific device on the network.

### Example of Class B Network:
- **IP Address:** 172.16.45.1
- **Network ID:** 172.16
- **Host ID:** 45.1

## Tables for Reference

| Class | Range | Default Subnet Mask | Number of Networks | Number of Hosts per Network |
|-------|-------|---------------------|--------------------|----------------------------|
| A     | 1.0.0.0 to 126.0.0.0 | 255.0.0.0 | 128 | 16,777,214 |
| B     | 128.0.0.0 to 191.255.0.0 | 255.255.0.0 | 16,384 | 65,534 |
| C     | 192.0.0.0 to 223.255.255.0 | 255.255.255.0 | 2,097,152 | 254 |
| D     | 224.0.0.0 to 239.255.255.255 | N/A | Multicast only | N/A |
| E     | 240.0.0.0 to 255.255.255.255 | N/A | Reserved | N/A |

## Images for Better Understanding

<BLOCKQUOTE> IP Address Classes :</BLOCKQUOTE>  <BR>
![IP Address Classes](https://raw.github.com/karthikeya03/IMAGES/JustMain/2.jpeg)

<BLOCKQUOTE> Network and Host Portions : </BLOCKQUOTE>   <BR>
![Network and Host Portions](https://raw.github.com/karthikeya03/IMAGES/JustMain/1.gif)

## Summary

- **Class A, B, C:** Used for unicast communication.
- **Class D:** Used for multicast groups.
- **Class E:** Reserved for future use.
- **Network ID:** Identifies the network.
- **Host ID:** Identifies a device within the network.

Understanding these basics helps in designing and managing IP networks effectively.


## NETWORK ID and BROADCAST ID : 

```0.0.0.0``` : a network IP: an id that represents the first network, and cannot be used to represent a computer. <BR>
``` 1.0.0.0``` : is the first NETWORK IP of the first class. <BR>
``` 5.0.0.0``` : is the first NETWORK IP of the fifth class. <BR>
these cannot be used to represent a computer and cannot be provided as an ip address. <BR>
```255.255.255.255``` : is called a broadcast IP.

<BLOCKHEAD>EXAMPLE 1  </BLOCKHEAD>
: 10.250.67.89  <BR>
: 10.0.0.1 is the first ip  <BR>
:  10.255.255.254 is the last usable ip  <BR>
: 10.0.1.0 is the 256th usable ip <BR>

<BLOCKHEAD> EXAMPLE 2 </BLOCKHEAD>
: 172. 254. 89  <BR>
:  172.254.0.0 network id <BR>
: 172.254.255.255 broadcast id  <BR>
  
