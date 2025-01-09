# TASK FOR VPC ENDPOINT

### Problem Statement
Suppose there is an availability zone **US-EAST-1A**, which contains:
- A **private subnet** and a **public subnet**.
- The public subnet has access to the **internet gateway**.
- An S3 bucket exists **outside the availability zone**.

#### Scenario:
- **Public Subnet**: 
  - Can access the S3 bucket by following the **path highlighted in green**.
  - It traverses through the **Internet Gateway**, utilizes the public internet, and retrieves files from the S3 bucket.

- **Private Subnet**: 
  - Cannot directly access the S3 bucket using the public internet.
  - Requires a **NAT Gateway** attached to the public subnet, enabling indirect access to the S3 bucket.

This task will help you understand the necessity of VPC endpoints in ensuring secure and efficient communication within the AWS infrastructure.

---

### Steps

1. **Create an S3 Bucket**:
   - Add some files to the bucket for testing.

2. **Create a Public Instance**:
   - Launch an EC2 instance in the **public subnet**.

3. **Create a Private Subnet**:
   - Launch an EC2 instance in the **private subnet**.

4. **Test Access from Public Subnet**:
   - Login to the instance in the public subnet.
   - Attempt to access the file present in the S3 bucket.

5. **Setup NAT Gateway**:
   - Create and attach a **NAT Gateway** to the public subnet.
   - Configure the private subnet to route through the NAT Gateway.
   - Access the S3 bucket files from the private subnet.

---

### Why VPC Endpoints Matter
This exercise demonstrates the limitations of using public internet and NAT Gateways for private subnets. It shows how **VPC Endpoints** provide a more secure, cost-effective, and efficient way to access AWS services like S3 without exposing resources to the public internet.

### Visual Representation
![View the Image Here](#) <!-- Replace '#' with the URL to the image -->

For further details, refer to the [AWS VPC Endpoints Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-endpoints.html).

