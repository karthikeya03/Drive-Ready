# SESSION 2: VIRTUALIZATION

## Virtualization

- No need to maintain physical servers
- High availability
- Less power consumption
- Create and delete instances instantly
- Requires less manpower
- Physical servers: desktops, very low specifications

## Rack Servers

- Consists of various virtual servers 
- Power is only given to the physical server
- Low power consumption
- Example: THUB, 26 virtual machines (servers) in one physical rack server

  ![Virtualization Example](https://raw.githubusercontent.com/karthikeya03/Drive-Ready/main/SESSION.2.1.png)

### Types of Servers

- Tower servers
- Blade servers
- PowerEdge R740 Rack Server

## Operating Systems

- Traditional OS: Cannot control resource usage
- Virtual OS: Has 2 power sources

## Hypervisor: VMware

- Capability to extract hardware resources and gives control to the user
- Can decide how much data can be used and saved
- Example: Allocate 2GB of 6GB and save the rest for another port

## Example of Virtualization

**Physical server resources:** 50 cores CPU | 40 GB RAM

| Server   | CPU Cores | RAM  |
| -------- | --------- | ---- |
| Server 1 | 10 cores  | 8 GB |
| Server 2 | 10 cores  | 8 GB |
| Server 3 | 10 cores  | 8 GB |
| Server 4 | 10 cores  | 8 GB |
| Server 5 | 10 cores  | 8 GB |

- **Every virtual machine is a separate server**

)

![Virtualization Example](https://raw.githubusercontent.com/karthikeya03/Drive-Ready/main/SESSION.2.2.png)
