---
title: "Configure Security Groups"
date: 2026-09-07
weight: 3
chapter: false
pre: " <b> 4.4.3. </b> "
---

## Configure Security Groups

A Security Group acts as a virtual firewall that controls inbound and outbound traffic for resources in the VPC.

In this section, you will configure two Security Groups according to the principle of least privilege:

1. **ALB Security Group:** Allows Internet users to access the Load Balancer on port 80.
2. **ECS Task Security Group:** Allows traffic forwarded from the ALB to port 80 and blocks direct access from the public Internet.

---

## 1. Create a Security Group for the Application Load Balancer

Navigate to:

**AWS Console → VPC (or EC2) → Security Groups → Create security group**

Configure the basic information:

| Property | Value |
| :--- | :--- |
| **Security group name** | inventory-alb-sg |
| **Description** | Security group for Inventory ALB public access |
| **VPC** | inventory-vpc |

### Inbound Rules

| Type | Port Range | Source | Description |
| :--- | :--- | :--- | :--- |
| HTTP | 80 | 0.0.0.0/0 | Allow HTTP traffic from the Internet |

### Outbound Rules

Keep the default rule: All traffic to 0.0.0.0/0.

Choose **Create security group**.


---

## 2. Create a Security Group for Amazon ECS Tasks

Navigate to:

**AWS Console → Security Groups → Create security group**

Configure the basic information:

| Property | Value |
| :--- | :--- |
| **Security group name** | inventory-ecs-sg |
| **Description** | Security group for ECS tasks only from ALB |
| **VPC** | inventory-vpc |

### Inbound Rules

| Type | Port Range | Source | Description |
| :--- | :--- | :--- | :--- |
| HTTP | 80 | inventory-alb-sg | Allow traffic forwarded from the ALB only |

### Outbound Rules

Keep the default rule: All traffic to 0.0.0.0/0. This allows the container to download the Docker image from ECR and connect to MongoDB Atlas.

Choose **Create security group**.


---

## Expected Result

After completing this section, you will have:

- **inventory-alb-sg** controlling public traffic to the Application Load Balancer.
- **inventory-ecs-sg** protecting the ECS Fargate containers and allowing connections only from the ALB.
- The complete networking infrastructure (VPC, subnets, Route Table, Internet Gateway, and Security Groups) ready for Docker packaging and container deployment.