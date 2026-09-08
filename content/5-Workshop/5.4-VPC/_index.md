---
title : "Networking Infrastructure"
date: 2026-09-07
weight : 4
chapter : false
pre : " <b> 4.4. </b> "
---

### Goal

Build a basic, secure, and cost-efficient networking infrastructure on AWS for deploying the Warehouse Inventory Management application.

---

## 1. Overview

Networking is the foundation that enables AWS resources to communicate with one another and connect to the Internet. In this chapter, you will create an Amazon Virtual Private Cloud (VPC) and configure its essential networking components.

The streamlined network architecture includes:
- Amazon VPC: A logically isolated virtual network dedicated to the system.
- Public Subnets: Host the Application Load Balancer (ALB) and ECS Fargate tasks.
- Internet Gateway (IGW): Allows resources in the VPC to connect to the Internet so users can access the application and the application can communicate with MongoDB Atlas.
- Route Table: Routes network traffic through the Internet Gateway (0.0.0.0/0 $\rightarrow$ igw).
- Security Groups: Act as virtual firewalls to securely control traffic for the ALB and ECS tasks.

---

---

## 3. Practice Content

Complete the following configuration steps in order:

- **4.4.1 Create the VPC and Public Subnets**
- **4.4.2 Configure the Internet Gateway and Route Table**
- **4.4.3 Configure Security Groups for the Application Load Balancer (ALB) and Amazon ECS**

---

## 4. Expected Result

After completing this chapter, you will have:

- An Amazon Virtual Private Cloud (VPC) created with the specified CIDR range.
- Public subnets distributed across the Availability Zones (AZs).
- An Internet Gateway directly attached to the VPC and a correctly configured route table.
- Security Groups configured correctly: the ALB allows public traffic on port 80, while the ECS Security Group accepts traffic forwarded only from the ALB.
- A networking infrastructure ready for creating the Application Load Balancer and deploying containers.