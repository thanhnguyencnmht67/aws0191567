---
title : "Configure Network"
date: 2026-09-07
weight : 2
chapter : false
pre : " <b> 4.4.2. </b> "
---

## Configure Network

After creating the Virtual Private Cloud (VPC), the next step is to configure the networking components required for the services to connect to the Internet and communicate with MongoDB Atlas.

In this section, you will create two public subnets in different Availability Zones, attach an Internet Gateway, and configure a Route Table to route network traffic.

---

## Create Public Subnets

Navigate to:

**AWS Console → VPC → Subnets → Create subnet**

In **VPC ID**, select **inventory-vpc**.

Create two subnets using the following configuration:

| Name | Availability Zone | IPv4 CIDR |
|------|-------------------|------------|
| inventory-public-subnet-a | ap-southeast-1a | 10.0.1.0/24 |
| inventory-public-subnet-b | ap-southeast-1b | 10.0.2.0/24 |

Enable automatic public IP assignment for both subnets:

Select **inventory-public-subnet-a → Actions → Edit subnet settings**, enable **Auto-assign public IPv4 address**, and choose **Save**.

Repeat the same steps for **inventory-public-subnet-b**.

![Subnets](/images/5-Workshop/5.4-VPC/5.4.2.1.png)

---

## Configure the Internet Gateway

The Internet Gateway allows resources inside the VPC to connect to the public Internet.

Navigate to:

**AWS Console → VPC → Internet Gateways → Create internet gateway**

Configure the Internet Gateway as follows:

| Property | Value |
|----------|-------|
| Name | inventory-igw |

After creating the Internet Gateway:

- Select **Attach to VPC**.
- Choose **inventory-vpc**.

Verify that the Internet Gateway status is **Attached**.

![Internet Gateway](/images/5-Workshop/5.4-VPC/5.4.2.2.png)

---

## Configure the Route Table

The Route Table defines how traffic from the subnets reaches the Internet Gateway and MongoDB Atlas.

Navigate to:

**AWS Console → VPC → Route Tables → Create route table**

Create a Route Table with the following configuration:

| Property | Value |
|----------|-------|
| Name | inventory-public-rt |
| VPC | inventory-vpc |

Choose **Create route table**.

### Configure the Routes

Select **inventory-public-rt**, open the **Routes** tab, choose **Edit routes**, and add the following route:

| Destination | Target |
|-------------|--------|
| 0.0.0.0/0 | inventory-igw (Internet Gateway) |

Choose **Save changes**.

![Public Route Table Routes](/images/5-Workshop/5.4-VPC/5.4.2.3.png)

### Configure Subnet Associations

Open the **Subnet associations** tab, choose **Edit subnet associations**, and select both public subnets:

- inventory-public-subnet-a
- inventory-public-subnet-b

Choose **Save associations**.

![Subnet Associations](/images/5-Workshop/5.4-VPC/5.4.2.3.png)

---

## Expected Result

After completing this section, you will have:

- Two public subnets in different Availability Zones (ap-southeast-1a and ap-southeast-1b) with automatic public IP assignment enabled.
- An Internet Gateway named **inventory-igw** successfully attached to **inventory-vpc**.
- A public Route Table named **inventory-public-rt** routing all `0.0.0.0/0` traffic through the Internet Gateway and associated with both subnets.
- A networking infrastructure ready for Security Group configuration in the next section.