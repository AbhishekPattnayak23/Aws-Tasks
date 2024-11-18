# Subnetting and Network Basics

Subnets are a logical subdivision of an IP network, or a network within a network. The process of dividing a network into subnets is called **subnetting**.

---
## VPC- Virtual Private Cloud
## VPC Creations, Subnets:

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
# AWS VPC and VPC Peering

## Overview

### What is AWS VPC?
Amazon Virtual Private Cloud (VPC) enables you to launch AWS resources in a logically isolated virtual network that you define. With a VPC, you have full control over your virtual networking environment, including IP address ranges, subnets, route tables, and network gateways.

### Key Features of AWS VPC:
- **Customizable IP Address Ranges**: Define your own private IP address range using CIDR (e.g., `10.0.0.0/16`).
- **Subnets**: Partition your VPC into public and private subnets to separate resources.
- **Security Groups and NACLs**: Control inbound and outbound traffic at the instance and subnet level.
- **Elastic IPs and NAT Gateways**: Enable communication between instances and the internet.
- **Integration**: Easily connect with other AWS services and on-premises environments.

---

## What is VPC Peering?
VPC Peering is a networking connection between two VPCs that allows traffic to be routed between them using private IP addresses. VPC Peering can be established between VPCs in:
- The same AWS account.
- Different AWS accounts.
- The same or different AWS regions (inter-region VPC Peering).

### Use Cases:
- Sharing resources (e.g., databases, services) across VPCs.
- Multi-account architecture where services in one account need to interact with services in another.
- Simplifying application architectures by connecting isolated environments.

---

## How VPC Peering Works
1. **Request and Accept**:
   - One VPC owner sends a peering request to the target VPC owner.
   - The target VPC owner accepts the request to establish the connection.

2. **Route Configuration**:
   - Update route tables in both VPCs to enable traffic flow between them.

3. **Security Groups and NACLs**:
   - Configure rules to allow traffic between instances in the peered VPCs.

### Important Notes:
- **No Transitive Peering**: If VPC A is peered with VPC B, and VPC B is peered with VPC C, A cannot communicate with C via B.
- **Performance and Security**: Peering traffic stays on AWS's global private network, ensuring high performance and security.

---

## Example Use Case

### Scenario:
You have two VPCs:
- **VPC A (10.0.0.0/16)**: Hosting a web application.
- **VPC B (192.168.0.0/16)**: Hosting a database.

You can use VPC Peering to allow the web application in VPC A to securely communicate with the database in VPC B without exposing it to the internet.

---

## Configuration Steps for VPC Peering

1. **Create a VPC Peering Connection**:
   - Go to the **VPC Console** → Select **Peering Connections** → Click **Create Peering Connection**.
   - Specify the requester VPC and acceptor VPC details.

2. **Accept the Peering Connection**:
   - The owner of the target VPC must accept the peering request.

3. **Update Route Tables**:
   - Add routes in both VPCs' route tables to point to the peering connection.

4. **Modify Security Groups**:
   - Allow inbound and outbound rules to permit communication between the VPCs.

---

## Limitations
- **No Transitive Routing**: Communication is only direct between peered VPCs.
- **Overlapping CIDR Blocks**: VPCs with overlapping IP address ranges cannot peer.
- **Soft Limits**: Maximum of 125 peering connections per VPC (soft limit).

---

## AWS VPC Setup Guide

![AWS VPC](https://github.com/AbhishekPattnayak23/Aws-Tasks/blob/main/Assets/aws-arch-1.png)

### What is VPC?
A Virtual Private Cloud (VPC) is a virtual network environment within AWS that allows you to create a logically isolated section of the AWS Cloud where you can launch AWS resources in a virtual network that you define.

---

## Creating VPC
To create a VPC:
1. Go to the AWS Management Console.
2. Navigate to the VPC dashboard.
3. Click on "Create VPC" and specify the VPC details such as CIDR block.

---

## Creating Subnets & Internet Gateway

### Subnets
Subnets are subdivisions of a VPC's IP address range. They help organize and manage different parts of your network.

*Example:*  
Imagine a large plot of land that you want to develop into a residential area. Subnets are like individual buildings within this plot, each containing multiple flats.

To create subnets:
1. Navigate to the VPC dashboard.
2. Click on "Subnets" and then "Create Subnet".
3. Specify the subnet details including CIDR block and Availability Zone (AZ).

### Internet Gateway (IGW)
An Internet Gateway allows communication between instances in your VPC and the internet.

To create an Internet Gateway:
1. Navigate to the VPC dashboard.
2. Click on "Internet Gateways" and then "Create Internet Gateway".
3. Attach the Internet Gateway to your VPC.

---

## Creating Routing Tables

Routing tables define how traffic is directed within the VPC. They control the flow of traffic between subnets, internet gateways, and other network devices within the VPC.

To create a routing table:
1. Navigate to the VPC dashboard.
2. Click on "Route Tables" and then "Create Route Table".
3. Define the routing rules, ensuring that traffic flows efficiently and securely to its intended destination.

---

## Internet Gateway & Route Tables

### Internet Gateway (IGW)
An Internet Gateway allows communication between instances in your VPC and the internet.

### Route Tables
Route tables control the flow of traffic within the VPC. They ensure that traffic is directed efficiently and securely to its intended destination.

To configure Internet Gateway and Route Tables:
1. Create an Internet Gateway and attach it to your VPC.
2. Create a Route Table and define routing rules, allowing traffic to flow between subnets and the internet.

**Note:** In routing tables, `0.0.0.0/0` means traffic not destined for the local network (e.g., `10.35.0.0/16`) should be routed to the internet gateway.

---

## Example on VPC

On a high level, each company's data and applications are kept separate and secure within their own VPC. Subnets help organize different stages of the software development lifecycle.

![VPC Setup Diagram]([vpc_setup.png](https://github.com/AbhishekPattnayak23/Aws-Tasks/blob/main/Assets/aws-arch-1.png))

Now you have configured VPC and Subnets successfully!

![Example Image](https://github.com/saikiranpi/mastering-aws/assets/109568252/97947faf-5b41-41da-9be0-78fd4e495250)

---

## References
- [AWS VPC Documentation](https://docs.aws.amazon.com/vpc)
- [AWS VPC Peering Guide](https://docs.aws.amazon.com/vpc/latest/peering)

![IP Diagram](https://github.com/AbhishekPattnayak23/Aws-Tasks/blob/main/Assets/vpc.png)

Happy Subnetting!

