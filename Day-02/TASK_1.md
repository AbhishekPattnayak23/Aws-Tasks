## TASK - 1 implement the below architecture in AWS
![vpc_setup.png](https://github.com/AbhishekPattnayak23/Aws-Tasks/blob/main/Assets/aws-arch-1.png)


# Subnets Overview

Subnets are a logical subdivision of an IP network, or a network within a network. The process of dividing a network into subnets is called **subnetting**.

### Example Subnets

#### Network: `10.0.0.0/16` (Class A)
- **Binary Representation**: `00001010.00000000.00000000.00000000`
- **Broadcast**: `10.0.255.255` → `00001010.00000000.11111111.11111111`
- **Host Range**:
  - **Minimum**: `10.0.0.1` → `00001010.00000000.00000000.00000001`
  - **Maximum**: `10.0.255.254` → `00001010.00000000.11111111.11111110`
- **Usable Hosts/Net**: `65,534` (Private Internet)

#### Network: `172.16.2.0/24` (Class B)
- **Binary Representation**: `10101100.00010000.00000010.00000000`
- **Broadcast**: `172.16.2.255` → `10101100.00010000.00000010.11111111`
- **Host Range**:
  - **Minimum**: `172.16.2.1` → `10101100.00010000.00000010.00000001`
  - **Maximum**: `172.16.2.254` → `10101100.00010000.00000010.11111110`
- **Usable Hosts/Net**: `254` (Private Internet)

---

### Security and Real-Time Usage
1. Each organization or company keeps its applications and data separate within its own VPC, ensuring security.
2. Subnets are essentially bundles of IP addresses.
3. Developers often have their own servers to test applications:
   - **Testing Servers**: For development and staging.
   - **Production Servers**: Where the final version of applications is deployed.
4. **AWS Route Tables**: Control the flow of traffic between subnets, internet gateways, or virtual private gateways.

---

### Example: AWS Data Center in North Virginia
- **VPC-1**: `10.35.0.0/16` (contains 65,534 IP addresses).
- **VPC-2**: `10.36.0.0/16` (another VPC with separate IPs).
- **No Direct Communication**: Without **VPC Peering**, there is no communication between VPC-1 and VPC-2.
- **VPC Peering**: Enables communication between VPCs, even if they are in different regions.

---

## Steps to Create a VPC

1. **Go to AWS Console**:
   - Search for "VPC."
   - Assign an IP range, e.g., `10.0.0.0/16`.
   - Disable IPv6 CIDR block unless required.
   - Click "Create VPC."

2. **Enable DNS Hostnames**:
   - Under the **Actions** menu, select "Edit VPC Settings."
   - Enable "DNS Hostnames" to allow public access.

3. **Create Subnets**:
   - Use the created VPC and assign subnet IPs:
     - **Web Servers**: `10.0.1.0/24` (251 IPs).
     - **App Servers**: `10.0.2.0/24` (251 IPs).
     - **Database Servers**: `10.0.3.0/24` (251 IPs).

4. **Create an Internet Gateway**:
   - Navigate to "Internet Gateways."
   - Create and attach the gateway to the VPC.
   - This allows traffic in and out of the VPC.

5. **Create Route Tables**:
   - Navigate to "Route Tables."
   - Create a route table for the VPC.
   - Edit routes:
     - Add `0.0.0.0/0` and associate it with the Internet Gateway.
   - Associate subnets with the route table to allow or restrict access.

---

### IP Address Calculation for `10.0.0.0/16`
The range `10.0.0.0/16` provides a total of **65,536 IP addresses**, calculated as follows:
1. **IPv4 Address**: 32 bits long.
   - Binary: `00001010.00000000.00000000.00000000`.
2. **Subnet Mask (`/16`)**: First 16 bits are for the network, leaving 16 bits for hosts.
   - Binary: `11111111.11111111.00000000.00000000`.
3. **Total Host Addresses**: 
   - \(2^{16} = 65,536\).
4. **Usable IP Addresses**:
   - Subtract 2 addresses (network + broadcast).
   - \(65,536 - 2 = 65,534\).

---

### Key Notes
- **Subnetting** helps organize IP addresses logically.
- VPC Peering allows inter-VPC communication, even across regions.
- Ensure security by using route tables and subnets appropriately.
- Never allow unrestricted traffic (`0.0.0.0/0`) in production environments.

---

### Diagram Example (Fig: 1.1)

```plaintext
VPC: 10.0.0.0/16
├── Subnet 1: Web Servers (10.0.1.0/24)
├── Subnet 2: App Servers (10.0.2.0/24)
└── Subnet 3: Database Servers (10.0.3.0/24)
