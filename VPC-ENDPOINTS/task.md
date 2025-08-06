# TASK FOR VPC ENDPOINT
### Visual Representation
![View the Image Here](https://github.com/AbhishekPattnayak23/Aws-Tasks/blob/main/Assets/vpc_endpoint.png)
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




## In Detailed Steps:
# 🚀 AWS Project: Accessing S3 from Private EC2 via Public EC2 and NAT Gateway

This guide walks through setting up a secure AWS architecture with the following:

- A VPC with public and private subnets
- EC2 instances in each subnet
- An S3 bucket hosting an image
- Accessing the image from a public EC2 instance
- Attempting (and failing) to access it from a private EC2 instance without NAT
- Configuring a NAT Gateway to enable internet access from the private subnet

---

## 📦 Step 1: Create a Custom VPC with Public and Private Subnets

1. Go to **VPC Dashboard** in AWS Console.
2. Click on **Create VPC**, then choose **"VPC and more"**.
3. Set the following values:
   - **Name tag**: `MyCustomVPC`
   - **Region**: `Asia Pacific (Mumbai) - ap-south-1`
   - **Availability Zones**: Select only **1 AZ**
   - **Number of public subnets**: `1`
   - **Number of private subnets**: `1`
   - **IPv4 CIDR block**: `10.0.0.0/16`
   - **Public Subnet CIDR**: `10.0.1.0/24`
   - **Private Subnet CIDR**: `10.0.2.0/24`
4. Enable auto-assign public IPs for public subnet.
5. Leave the rest as default and click **Create VPC**.

---

## 📁 Step 2: Create an S3 Bucket and Upload a File

1. Go to the **S3 Dashboard** → **Create bucket**.
2. Set the bucket name as `my-public-image-bucket`.
3. Choose the same region: `ap-south-1 (Mumbai)`.
4. **Uncheck** the option: “Block all public access”.
5. Acknowledge the warning and create the bucket.
6. After creation:
   - Go inside the bucket and click **Upload**.
   - Upload a file, e.g., `myphoto.jpg`.
   - After upload, go to **Permissions** tab → Enable public access.
   - Copy the **Object URL** for testing.

---

## 💻 Step 3: Launch EC2 Instances in Public and Private Subnets

### 3.1 Create Key Pair

1. Go to **EC2 Dashboard** → **Key Pairs** → **Create key pair**.
2. Name it `mykey` and select **PEM** format.
3. Download the `mykey.pem` file to your local machine.

### 3.2 Create Security Groups

1. **Public SG**: Allow inbound SSH (port 22) from your IP.
2. **Private SG**: Allow inbound SSH (port 22) **from the public instance's security group** only.

### 3.3 Launch EC2 Instances

- **Public EC2:**
  - AMI: Ubuntu 20.04
  - Instance type: t2.micro
  - Subnet: `PublicSubnet (10.0.1.0/24)`
  - Enable auto-assign public IP
  - Attach `mykey.pem`
  - Use **Public SG**

- **Private EC2:**
  - AMI: Ubuntu 20.04
  - Instance type: t2.micro
  - Subnet: `PrivateSubnet (10.0.2.0/24)`
  - **No** public IP
  - Attach `mykey.pem`
  - Use **Private SG**

---

## 🌍 Step 4: Internet Gateway and Route Table Configuration

1. An **Internet Gateway** should be automatically created if you used "VPC and more".
   - If not, go to VPC → Internet Gateways → Create.
   - Attach the IGW to your VPC.

2. **Route Tables:**
   - For the **Public Route Table**:
     - Add a route: `0.0.0.0/0` → Internet Gateway.
     - Associate with the **public subnet**.
   - For the **Private Route Table**:
     - No internet route yet — will be updated when NAT Gateway is added.
     - Associate with the **private subnet**.

---

## 🔐 Step 5: SSH Access to Public EC2 Instance

### 5.1 Convert PEM to PPK (if using PuTTY)

- Open **PuTTYgen**
- Load `mykey.pem`
- Click **Save private key** → Save as `mykey.ppk`

### 5.2 SSH into Public EC2

- Open **PuTTY**
  - Hostname: `ubuntu@<public-ec2-ip>`
  - Port: `22`
  - Auth → Browse to `mykey.ppk`
- Click **Open** to connect

---

## 🌐 Step 6: Download Image from S3 Bucket via Public EC2

Once inside the public EC2 instance:

1. Use `curl` to download the image:

   ```bash
   curl -O https://my-public-image-bucket.s3.ap-south-1.amazonaws.com/myphoto.jpg

The image should download successfully, confirming internet and S3 access.

🔁 Step 7: SSH into Private EC2 from Public EC2
In the public EC2 terminal, create the key file:


nano key.pem
Paste the full content of your mykey.pem file into this editor.

Save and exit (Ctrl+O, Enter, Ctrl+X).

Modify permissions:


chmod 400 key.pem
SSH into the private EC2 instance:


ssh -i key.pem ubuntu@<private-ec2-private-ip>
🚫 Step 8: Attempt to Access S3 from Private EC2 (Fails)
Try downloading the image in the private EC2:


curl -O https://my-public-image-bucket.s3.ap-south-1.amazonaws.com/myphoto.jpg
This should fail because the private instance has no internet access.

🌐 Step 9: Configure NAT Gateway for Private Subnet Internet Access
Go to EC2 Dashboard → Elastic IPs → Allocate a new EIP.

Go to NAT Gateways → Create NAT Gateway

Name: MyNATGateway

Subnet: Public Subnet

Elastic IP: Select the one you just created

Once created, update the Private Route Table:

Add route: 0.0.0.0/0 → NAT Gateway

Now, the private EC2 instance can reach the internet.

✅ Step 10: Access S3 from Private EC2 (After NAT Configuration)
Back on the private EC2 instance, try:


curl -O https://my-public-image-bucket.s3.ap-south-1.amazonaws.com/myphoto.jpg
This time the image should successfully download — confirming that the NAT Gateway is working.

🧹 Step 11: Clean Up AWS Resources
To avoid unnecessary charges:

Terminate both EC2 instances

Delete the NAT Gateway

Release the Elastic IP

Delete the S3 bucket (if not needed)

Delete the VPC and associated components

🔐 Security Notes
Never expose .pem files publicly.

Always use security groups with least-privilege access.

Use IAM roles for EC2s when accessing AWS services like S3.

Avoid keeping NAT Gateways running unnecessarily — they incur hourly costs.


---

### Why VPC Endpoints Matter
This exercise demonstrates the limitations of using public internet and NAT Gateways for private subnets. It shows how **VPC Endpoints** provide a more secure, cost-effective, and efficient way to access AWS services like S3 without exposing resources to the public internet.

 <!-- Replace '#' with the URL to the image -->

For further details, refer to the [AWS VPC Endpoints Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-endpoints.html).

