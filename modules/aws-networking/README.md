# AWS Networking Module

Welcome to the **AWS Networking** module challenge! In this task, you’ll create two VPCs and configure them to communicate with each other via peering, along with establishing public and private subnets in each VPC. Below is a high-level overview of what we’re looking for.

---

## Overview

- **Two VPCs**: You’ll provision `vpc-1` and `vpc-2` (you are free to use more creative names)
- **VPC Peering**: The two VPCs should be peered together based on their respective CIDR blocks.
- **Subnets**:
  - Each VPC will have two lists of subnets: **private** subnets and **public** subnets.
  - There will be 3 private and 3 public subnets in each VPC
  - Each subnet should define:
    - **Name**
    - **CIDR Block**
    - **Availability Zone**
- **Internet Access**:
  - Public subnets should reach the internet via an Internet Gateway (IGW).
  - Private subnets should reach the internet via a NAT Gateway.

Your primary goal is to demonstrate how you structure and configure VPCs, subnets, peering, and related networking components.

---

## Note

You can safely assume the following in the context of this challene:

- You are working in an existing account
- Inputs can be considered correct, you do not need to validate them in your module

---

## Inputs

At a minimum, your module should acceps the following variables to execute:

- The CIDR blocks of the two VPCs
- The subnet definitions for each of the VPCs with the required information in the [Subnets](#subnets) section.
- A configured `aws` provider

If you find other inputs help to accomplish the required tasks or allow for increased functionality you are free to add them.
---

## Requirements

1. **Create Two VPCs**
   - Each VPC should have an associated CIDR block.

2. **VPC Peering**
   - Establish a VPC peering connection between `vpc-1` and `vpc-2`, ensuring routes are configured to allow communication between them.

3. **Subnet Creation**
   - For both VPCs, create public and private subnets based on the provided lists

4. **Internet Connectivity**
   - Public subnets use an Internet Gateway (IGW) to route traffic to the internet.
   - Private subnets use a NAT Gateway to allow outbound internet access.

5. **Outputs**
   - Provide relevant outputs such as VPC IDs, subnet IDs, or any other information you find helpful.

---

## Bonus Challenges

Here are a few ideas you might consider if you want to go above and beyond:

1. **Security Groups / NACLs**
   - Create and attach custom security groups or network ACLs to ensure fine-grained network control.
   - This could be for

2. **DNS and Route 53**
   - Configure internal DNS or host-based routing for your VPCs, possibly using a private hosted zone in Route 53.

3. **VPC Endpoints**
   - Add a VPC endpoint (e.g., for S3 or DynamoDB) to demonstrate how private subnets can access AWS services without using a public IP.

4. **Multi-Region Peering**
   - Configure the setup across different regions (if you really want to dive deeper), noting any special considerations.

Feel free to pick and choose any of these (or invent your own) if you’d like to showcase additional skills.

---

## Usage

Below is a simplified example of how your module might be consumed (edit as needed):

```hcl
module "aws_vpc_peering" {
  source              = "./path/to/your/module"

  vpc1_cidr_block     = "10.0.0.0/16"
  vpc2_cidr_block     = "10.1.0.0/16"

  vpc1_public_subnets = [
    { name = "vpc1-public-1", cidr_block = "10.0.1.0/24", availability_zone = "us-east-1a" },
    { name = "vpc1-public-2", cidr_block = "10.0.2.0/24", availability_zone = "us-east-1b" }
  ]

  vpc1_private_subnets = [
    { name = "vpc1-private-1", cidr_block = "10.0.3.0/24", availability_zone = "us-east-1a" },
    { name = "vpc1-private-2", cidr_block = "10.0.4.0/24", availability_zone = "us-east-1b" }
  ]

  vpc2_public_subnets = [
    { name = "vpc2-public-1", cidr_block = "10.1.1.0/24", availability_zone = "us-east-1a" }
  ]

  vpc2_private_subnets = [
    { name = "vpc2-private-1", cidr_block = "10.1.2.0/24", availability_zone = "us-east-1a" }
  ]

  # Additional variables as needed...
}