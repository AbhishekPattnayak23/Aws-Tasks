# VPC Peering Setup and EC2 Instance Creation Guide

This guide provides a step-by-step walkthrough to establish VPC Peering and configure EC2 instances under the peered VPCs. It also includes details on best practices and recommendations.

---

## VPC Peering Architecture

![VPC Peering](https://github.com/AbhishekPattnayak23/Aws-Tasks/blob/main/Assets/vpc_peering.png)

---

### Introduction to VPC Peering

VPC Peering allows you to establish communication between two VPCs using the AWS backbone, enabling private, low-latency, and secure communication between resources in those VPCs. By default, there is no built-in communication between VPCs.

---

# Establishing Communication Between VPCs Using VPC Peering

By default, there is no inbuilt communication between VPCs. With the help of **VPC Peering**, we can establish communication between servers.

## Steps to Create a VPC

1. Navigate to **VPC and More** in the North Virginia region.
2. Name the VPC: `App_Server`.
3. Assign an IP CIDR block: `10.0.0.0/16` (Ensure IP ranges do not overlap).
4. Select the availability zone: `us-east-1a` (can be changed as per requirements).
5. Set the number of subnets:
   - **Public Subnets**: 1
   - **Private Subnets**: 0
6. Click **Create VPC**.
7. Navigate to **Security Groups** in the left sidebar.
8. Search for your VPC and edit the inbound rules to allow **All Traffic** (not recommended for production use).

> **Note**: Security group rules with source `0.0.0.0/0` or `::/0` allow access from all IP addresses. It is recommended to allow access only from known IPs.

### Avoid Overlapping IPs
- If `App_Server` has an IPv4 CIDR block `10.0.0.0/16`, then:
  - For `Web_Server`, use a different CIDR block, e.g., `172.16.0.0/16`.

Similarly, create a `Web_Server` VPC and edit the security group rules to allow all traffic (again, not recommended for production environments).

---

## How to Create an EC2 Instance for a VPC?

1. Go to **EC2 (Elastic Cloud)** under Services.
2. Click on **Launch Instance**.
3. Name the instance: `App_Server` and select an Amazon Machine Image (AMI).
4. Choose `Ubuntu t2.micro` (Free Tier eligible).
5. Set up or create a **Key Pair**:
   - For SSH client: generate a `.pem` key.
   - For PuTTY: generate a `.ppk` key and download PuTTY for local machine access.
6. Under **Network Settings**, click **Edit** and:
   - Choose the respective VPC (e.g., `App_Server` VPC).
   - Enable **Auto-assign Public IP**.
7. Select the existing **Security Group** created earlier.
8. Launch the instance.

Repeat the process to create another instance for `Web_Server`, ensuring the same `.ppk` key is used for both servers.

### Testing EC2 Instance Access
- Open **PuTTY**.
- Copy the **Public IPv4 Address** from the EC2 instance details page.
- Under **Host Name**, enter: ubuntu@<EC2_PUBLIC_IP>

- Navigate to **Auth > Credentials > Browse** and select the `.ppk` file for that region.
- Click **Open**.

---

## Creating a `Db_Server` in Ohio Region

1. Create a VPC named `Db_Server` in the Ohio region.
2. Edit the Security Group for `Db_Server` to allow all traffic.
3. Launch an EC2 instance for `Db_Server` with a different `.ppk` key to access it via PuTTY.
4. Test access using the same process as above.

---

## Setting Up VPC Peering Connection

### Steps to Create a Peering Connection:
1. Go to **Peering Connections** under the VPC section.
2. Click **Create Peering Connection**.
3. Provide a name: e.g., `App-to-Web`.
4. Set the **Requester VPC** as `App_Server`.
5. Set the account to **My Account** or another as required.
6. Select the region and choose the **Acceptor VPC ID** (`Web_Server`).
7. Create the peering connection.

Once created, **accept the request** under the **Actions** menu.

### Update Route Tables for Peering:
1. Navigate to the **Route Tables** for `App_Server`:
 - **Routes > Edit Routes > Add Route**.
 - Destination: `172.16.0.0/16` (CIDR block of `Web_Server`).
 - Target: **Peering Connection** (e.g., `App-to-Web`).
2. Save changes.
3. Repeat the same steps for `Web_Server` route tables, specifying `10.0.0.0/16` (CIDR block of `App_Server`).

### Test Connectivity
- Open PuTTY and ping the respective IP addresses between `App_Server` and `Web_Server`.

---

## Establishing Peering Connection Between Multiple Regions

To connect `App_Server` (North Virginia) and `Db_Server` (Ohio):
1. Create a new peering connection named `Db-to-App`.
2. Select:
 - **Requester VPC**: `Db_Server`.
 - **Acceptor VPC**: `App_Server`.
 - Region: North Virginia (`us-east-1`).
3. Accept the request in the **North Virginia** region console.

### Update Route Tables:
1. For `Db_Server` in Ohio:
 - Add route with destination `10.0.0.0/16` (CIDR block of `App_Server`).
 - Set target to **Peering Connection** (`Db-to-App`).
2. For `App_Server` in North Virginia:
 - Add route with destination `192.168.0.0/16` (CIDR block of `Db_Server`).
 - Set target to **Peering Connection** (`Db-to-App`).

Repeat similar steps to establish a peering connection between `Web_Server` and `Db_Server`.

---

### Final Testing
- Test connectivity between all servers (`App_Server`, `Web_Server`, `Db_Server`) using PuTTY and pinging the respective private IPs.

--- 

## Notes:
- Always ensure IP CIDR blocks for VPCs do not overlap.
- Avoid allowing all traffic in security groups for production environments. Restrict access to known IP ranges.



By following this guide, you can establish a robust and secure VPC peering connection, ensuring efficient communication between resources in different VPCs. Happy networking!

