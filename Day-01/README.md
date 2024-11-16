# IP Addressing Explained

![IP Diagram](https://github.com/AbhishekPattnayak23/Aws-Tasks/blob/main/Assets/Understanding_IP_Addressing.jpg)

## Welcome to the Network Setup Guide!

This guide will help you understand the basics of IP addresses, classes, public and private IPs, and how to configure them for different environments.

---

## Key Topics Covered:
- **Understanding IP Addresses**
  - IPv4: Shorter addresses, like phone numbers for devices.
  - IPv6: Longer addresses, similar to phone numbers but with more digits.
  - **IP Address Ranges**  
    - IPv4 addresses range from `0.0.0.0` to `255.255.255.255`.  
    - Divided into five classes: A, B, C, D, and E.

---

## IP Address Classes

| **Class** | **Range**                           | **Purpose**                             |
|-----------|-------------------------------------|-----------------------------------------|
| A         | `1.0.0.0 - 126.255.255.255`         | Large networks with many devices        |
| B         | `128.0.0.0 - 191.255.255.255`       | Medium-sized networks                   |
| C         | `192.0.0.0 - 223.255.255.255`       | Small networks                          |
| D         | Multicast                           | Data packets to multiple devices        |
| E         | Reserved                            | Experimental purposes and future use    |

---

### Loopback Address

You might notice that `127.0.0.1` is skipped in Class A. This is reserved as the **loopback address**, which means the device is pinging itself.

---

## Public and Private IPs

- **Public IPs**: Used for communication over external networks.
- **Private IPs**: Used internally within closed infrastructures or office environments.

### Private IP Ranges:
- `10.0.0.0 - 10.255.255.255` (10/8 prefix)  
- `172.16.0.0 - 172.31.255.255` (172.16/12 prefix)  
- `192.168.0.0 - 192.168.255.255` (192.168/16 prefix)  

These addresses are for internal use only and should not be accessible from outside the network.

---

## Configuring IP Addresses

### Example:
To demonstrate:
1. Open CMD and type `ipconfig` to view your IPv4 private address.
2. Search "my public IP" on Google to find your public IP address.

---

## More About Networking

### Types of IPs:
1. **IPv4**  
2. **IPv6**

### IP Ranges:
- Range: `0.0.0.0` to `255.255.255.255`

### Classes:
- **Class A**: Range: `1.0.0.0` to `126.255.255.255`  
  Used for large networks.  
  Default subnet mask: `255.0.0.0`  
- **Class B**: Range: `128.0.0.0` to `191.255.255.255`  
  Used for medium-sized networks.  
  Default subnet mask: `255.255.0.0`  
- **Class C**: Range: `192.0.0.0` to `223.255.255.255`  
  Used for small networks.  
  Default subnet mask: `255.255.255.0`  

---

### Public vs Private IP

To avoid shortages of IPs, [RFC1918](https://datatracker.ietf.org/doc/html/rfc1918) introduced **Public and Private IPs**:
- **Private IPs**: Operate within a closed infrastructure (e.g., offices).
- **Public IPs**: Access the internet gateway while ensuring confidential data stays secure.

---

## Diagram of Networking Setup

![Networking Setup](https://github.com/user-attachments/assets/b137a247-b46d-4f45-8a24-1c2d8bcb1d54)

---

Happy Networking!
