---
title : "Create VPC"
date: 2026-09-07
weight : 1
chapter : false
pre : " <b> 4.4.1. </b> "
---

## Create VPC

In this section, you will create a Virtual Private Cloud (VPC), which provides an isolated networking environment for deploying the application on AWS.

The VPC serves as the foundation of the entire infrastructure. All networking resources, including subnets, route tables, Internet Gateway, NAT Gateway, Application Load Balancer, and Amazon ECS, will be deployed inside this VPC.

---

## Create a Virtual Private Cloud

Navigate to:

**AWS Console → VPC → Your VPCs → Create VPC**

Select **VPC only**, then configure the following settings:

| Property | Value |
|----------|-------|
| Resources to create | VPC only |
| Name tag | inventory-vpc |
| IPv4 CIDR | 10.0.0.0/16 |
| IPv6 CIDR | None |
| Tenancy | Default |

Review the configuration and choose **Create VPC**.

![Create VPC](/images/5-Workshop/5.4-VPC/5.4.1.1.png)

---

## Enable DNS Hostnames for the VPC

Navigate to:

**AWS Console → VPC → Your VPCs**

When **VPC only** is selected, AWS may disable DNS Hostnames by default. Enable DNS settings so internal domain name resolution works correctly.

Select **inventory-vpc**, choose **Actions**, and then select **Edit VPC settings**.

Under **DNS settings**, enable **DNS resolution** and **DNS hostnames**, then choose **Save changes**.

![Edit VPC settings](/images/5-Workshop/5.4-VPC/5.4.1.2.png)

---

## Verify the VPC

Navigate to:

**AWS Console → VPC → Your VPCs**

Select **inventory-vpc** and verify the following settings:

| Property | Expected Value |
|----------|----------------|
| State | Available |
| IPv4 CIDR | 10.0.0.0/16 |
| DNS Resolution | Enabled |
| DNS Hostnames | Enabled |

Confirm that the VPC has been created successfully before proceeding to create subnets and route tables.

![VPC Details](/images/5-Workshop/5.4-VPC/5.4.1.2.png)

---

## Expected Result

After completing this section, you will have:

- A Virtual Private Cloud named **inventory-vpc**.
- A private networking environment with the IPv4 CIDR block **10.0.0.0/16**.
- DNS Resolution and DNS Hostnames enabled.
- A VPC ready for configuring subnets and other networking resources.