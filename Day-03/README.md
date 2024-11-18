# VPC Peering Guide

Welcome to the **VPC Peering Guide**! This document provides a comprehensive overview of VPC peering in AWS and walks you through setting up and managing VPC peering connections.

---

## What is VPC Peering?

**VPC Peering** in AWS (Amazon Web Services) is a networking connection that allows two Virtual Private Clouds (VPCs) to communicate with each other privately as if they were part of the same network. This is useful when separate VPCs hosting distinct resources, such as databases or services, need direct interaction.

---

## Key Features of VPC Peering

1. **Private Communication**:
   - Traffic between two peered VPCs remains on the AWS backbone.
   - It avoids the public internet, ensuring secure and low-latency communication.

2. **No Transitive Peering**:
   - VPC Peering does **not** support transitive routing.
     - Example: If VPC A is peered with VPC B, and VPC B is peered with VPC C, VPC A cannot communicate with VPC C unless a direct peering connection is established.

3. **Cross-Region Peering**:
   - AWS supports peering of VPCs located in different regions, enabling the creation of a global network of connected resources.

4. **CIDR Overlap Restrictions**:
   - The CIDR blocks of the peered VPCs **must not overlap** to avoid IP address conflicts.

5. **Cost**:
   - There is **no charge** for creating a VPC peering connection.
   - Data transfer across VPC peering is charged based on AWS inter-region or intra-region transfer rates.

---

## Common Use Cases for VPC Peering

1. **Multi-Tier Applications**:
   - Separate tiers (e.g., web servers, application servers, and databases) into different VPCs for better isolation and security.

2. **Cross-Account Collaboration**:
   - Collaborate across teams or departments using separate AWS accounts by sharing resources via VPC Peering.

3. **Inter-Region Communication**:
   - Enable communication between applications and resources in different AWS regions.

---

## Setting Up VPC Peering

### Step-by-Step Guide

1. **Visualize the Architecture**:
   - Create a network diagram to understand how the VPCs will connect and ensure there is no IP overlap.

2. **Create VPCs**:
   - Example:
     - **VPC1**: `10.1.0.0/16` (US East 1A)
     - **VPC2**: `172.16.0.0/16` (US East 1A)
     - **VPC3**: `192.168.0.0/16` (US East 2A)

3. **Launch EC2 Instances**:
   - Deploy EC2 instances in each VPC.
   - Use **user data** to run setup scripts (e.g., configure Nginx or install necessary software).

4. **Configure Security Groups**:
   - Open the required ports and allow traffic from the other VPC CIDR blocks.

5. **Create VPC Peering Connections**:
   - Navigate to the **VPC Dashboard** and establish peering connections.
   - Ensure:
     - No IP overlap between VPCs.
     - Cross-region peering is enabled, if required.

6. **Update Route Tables**:
   - Add routes to the route tables of each VPC to direct traffic to the peer VPCs via the peering connection.

---

## Example VPC Peering Diagram

```plaintext
VPC1 (10.1.0.0/16) ─────────┐
                             ├─ VPC Peering Connection
VPC2 (172.16.0.0/16) ───────┘

VPC3 (192.168.0.0/16) ──────┐
                             ├─ VPC Peering Connection
VPC2 (172.16.0.0/16) ───────┘
