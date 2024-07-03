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

![subnet](https://raw.github.com/karthikeya03/IMAGES/JustMain/image.png)

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
Telecommunication refers to the transmission of signals over a distance for the purpose of communication. In the context of IP addressing, it involves the use of IP addresses to facilitate the routing and delivery of data packets across networks.

Classful IP addressing has largely been replaced by classless inter-domain routing (CIDR), which allows for more flexible and efficient allocation of IP addresses. However, understanding classful addressing provides a foundational knowledge of how IP addressing originally worked and is essential for grasping more advanced concepts in networking.
