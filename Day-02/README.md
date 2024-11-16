# Subnetting and Network Basics

Subnets are a logical subdivision of an IP network, or a network within a network. The process of dividing a network into subnets is called **subnetting**.

---

## Subnet Examples:

### Subnet 1:
- **Network**: `10.0.0.0/16`  
  Binary: `00001010.00000000.00000000.00000000` (Class A)  
- **Broadcast**: `10.0.255.255`  
  Binary: `00001010.00000000.11111111.11111111`  
- **HostMin**: `10.0.0.1`  
  Binary: `00001010.00000000.00000000.00000001`  
- **HostMax**: `10.0.255.254`  
  Binary: `00001010.00000000.11111111.11111110`  
- **Hosts/Net**: `65534`  
  Use: (Private Internet)

---

### Subnet 2:
- **Network**: `172.16.2.0/24`  
  Binary: `10101100.00010000.00000010.00000000` (Class B)  
- **Broadcast**: `172.16.2.255`  
  Binary: `10101100.00010000.00000010.11111111`  
- **HostMin**: `172.16.2.1`  
  Binary: `10101100.00010000.00000010.00000001`  
- **HostMax**: `172.16.2.254`  
  Binary: `10101100.00010000.00000010.11111110`  
- **Hosts/Net**: `254`  
  Use: (Private Internet)

---

## Importance of Subnets:

- In terms of **security**, each organization or company ensures their applications or data are kept separate within their own Virtual Private Cloud (VPC).
- A subnet is essentially a **bundle of IP addresses**.  
- In real-world scenarios:
  - Developers have their own servers for testing applications (**testing servers**).  
  - **Production servers** are separate and host the final versions of applications.

---

## AWS and Subnetting:

- **AWS Route Tables** are used to control the flow of traffic:
  - Between subnets.
  - Between internet gateways or virtual private gateways.
- This ensures secure and efficient communication within and outside the network.

---

Happy Subnetting!

