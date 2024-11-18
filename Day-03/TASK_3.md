# VPC Peering Setup and EC2 Instance Creation Guide

This guide provides a step-by-step walkthrough to establish VPC Peering and configure EC2 instances under the peered VPCs. It also includes details on best practices and recommendations.

---

## VPC Peering Architecture

![VPC Peering](https://github.com/AbhishekPattnayak23/Aws-Tasks/blob/main/Assets/vpc_peering.png)

---

### Introduction to VPC Peering

VPC Peering allows you to establish communication between two VPCs using the AWS backbone, enabling private, low-latency, and secure communication between resources in those VPCs. By default, there is no built-in communication between VPCs.

---

## Steps to Establish VPC Peering

### **Step 1: Create VPCs**

1. **Navigate to the VPC Section**:
   - Go to **VPC and More** in the AWS Console.

2. **Create the First VPC**:
   - **IPv4 CIDR Block**: `10.0.0.0/16`
   - **Availability Zone**: Select a zone (e.g., `us-east-1a`).
   - **Public Subnets**: Set to 1.
   - **Private Subnets**: Set to 0.
   - Click **Create VPC**.

3. **Create the Second VPC**:
   - **IPv4 CIDR Block**: `172.16.0.0/16`
   - Ensure the CIDR blocks of both VPCs do not overlap.

---

### **Step 2: Configure Security Groups**

1. Navigate to **Security Groups** in the left-side navigation bar.
2. Search for the security group associated with your VPC.
3. Edit the **Inbound Rules**:
   - Add a rule to allow **all traffic** for testing purposes. *(Note: Allowing all traffic is not recommended for production environments. Instead, restrict access to specific IP ranges.)*
   - Example:
     - **Type**: All Traffic
     - **Source**: `0.0.0.0/0` or specific trusted IP ranges.

---

### **Step 3: Create a VPC Peering Connection**

1. **Initiate the Peering Request**:
   - Navigate to the **VPC Dashboard** > **Peering Connections**.
   - Click **Create Peering Connection**.
   - Specify the requester and accepter VPCs.

2. **Accept the Peering Request**:
   - In the accepter VPC, go to **Peering Connections** and accept the request.

3. **Update Route Tables**:
   - Add routes in both VPCs' route tables to enable communication:
     - Target: VPC Peering Connection
     - Destination: CIDR of the other VPC.

---

### **Step 4: Create EC2 Instances in the Peered VPCs**

#### **Step 4.1: Login to AWS Console**
1. Go to **AWS Console**.
2. Navigate to **EC2** under the "Services" tab.

#### **Step 4.2: Launch an EC2 Instance**
1. Click **Launch Instance** in the EC2 dashboard.

#### **Step 4.3: Configure Basic Instance Settings**
1. **Name and Tags**:
   - Provide a name (e.g., `App_Server` or `Web_Server`).
2. **Choose Amazon Machine Image (AMI)**:
   - Select an AMI (e.g., Amazon Linux 2, Ubuntu, or Windows Server).
3. **Instance Type**:
   - Choose a type based on your workload (e.g., `t2.micro` for free tier).

#### **Step 4.4: Configure Key Pair**
1. In the **Key Pair (login)** section:
   - Select an existing key pair or create a new one.
   - Download the `.pem` file for new key pairs (required for SSH access).

#### **Step 4.5: Configure Network Settings**
1. **VPC**:
   - Select the previously created VPC.
2. **Subnet**:
   - Choose a subnet (public or private) based on your use case.
3. **Auto-assign Public IP**:
   - Enable for public subnets to access the instance externally.

#### **Step 4.6: Configure Security Groups**
1. Create or select an existing security group:
   - For **SSH (Linux)**: Allow **port 22** from your IP.
   - For **HTTP/HTTPS**: Allow **ports 80/443**.
   - For **RDP (Windows)**: Allow **port 3389**.

#### **Step 4.7: Configure Storage**
1. Specify the root volume size and type:
   - Example: `gp2` or `gp3`.
2. Add additional volumes if necessary.

#### **Step 4.8: Configure Advanced Options (Optional)**
1. Add **IAM Roles** for access to other AWS resources.
2. Include **user data scripts** to install software or configure the instance on first boot.

#### **Step 4.9: Review and Launch**
1. Review all settings and click **Launch Instance**.

#### **Step 4.10: Connect to Your EC2 Instance**
1. Wait for the instance state to change to `Running`.
2. Connect using:
   - **SSH (Linux)**:
     ```bash
     ssh -i "your-key.pem" ec2-user@<public-ip-address>
     ```
   - **RDP (Windows)**: Use Remote Desktop with the public IP and password.

---

### Testing Connectivity

1. **Public Subnet**:
   - Ping or SSH into the instance using its public IP.
2. **Private Subnet**:
   - Ensure a NAT Gateway or VPN is set up for external access.

---

## Notes and Recommendations

1. **Avoid Overlapping CIDR Blocks**:
   - Example:
     - App_Server VPC: `10.0.0.0/16`
     - Web_Server VPC: `172.16.0.0/16`

2. **Security Best Practices**:
   - Do not allow `0.0.0.0/0` for production environments. Restrict access to known IP ranges.

3. **Transitive Peering Not Supported**:
   - Each VPC must be directly peered for communication.

---

By following this guide, you can establish a robust and secure VPC peering connection, ensuring efficient communication between resources in different VPCs. Happy networking!

