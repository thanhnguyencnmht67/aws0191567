---
title : "Configure Load Balancer"
date: 2026-09-07
weight : 1
chapter : false
pre : " <b> 4.7.1. </b> "
---

## Configure Load Balancer

In this section, you will configure an Application Load Balancer (ALB) for the Warehouse Inventory Management application.

The Application Load Balancer receives incoming HTTP requests from users and forwards them to the Amazon ECS service through a target group.

---

## Create a Target Group

Navigate to:

**AWS Console → EC2 → Target Groups → Create target group**

Configure the target group using the following settings.

| Property | Value |
|----------|-------|
| Target type | IP addresses |
| Protocol | HTTP |
| Port | 80 |
| VPC | inventory-vpc |
| Target group name | inventory-tg |

Choose **Next**, keep the default health check configuration, and create the target group.

![Create Target Group](/images/5-Workshop/5.7-Deploy-Application/5.7.1.1.png)

---

## Create an Application Load Balancer

Navigate to:

**AWS Console → EC2 → Load Balancers → Create Load Balancer**

Select **Application Load Balancer** and configure the following settings.

| Property | Value |
|----------|-------|
| Load Balancer name | inventory-alb |
| Scheme | Internet-facing |
| IP address type | IPv4 |
| VPC | inventory-vpc |
| Availability Zones | Public Subnets |

Select the security group created for the Application Load Balancer and continue.

![Create Load Balancer](/images/5-Workshop/5.7-Deploy-Application/5.7.1.2.png)

---

## Configure the Listener

Configure the default listener for the Application Load Balancer.

| Property | Value |
|----------|-------|
| Protocol | HTTP |
| Port | 80 |
| Default action | Forward to inventory-tg |

Review the configuration and choose **Create Load Balancer**.

![Configure Listener](/images/5-Workshop/5.7-Deploy-Application/5.7.1.3.png)

---

## Verify the Load Balancer

Navigate to:

**AWS Console → EC2 → Load Balancers**

Open the Application Load Balancer and verify that:

- The load balancer state is **Active**.
- The listener is configured successfully.
- The target group is associated with the load balancer.

![Load Balancer Listeners](/images/5-Workshop/5.7-Deploy-Application/5.7.1.4.png)

![Load Balancer Details](/images/5-Workshop/5.7-Deploy-Application/5.7.1.5.png)

---

## Expected Result

After completing this section, you will have:

- A Target Group created.
- An Application Load Balancer configured.
- A Listener forwarding requests to the Target Group.
- A Load Balancer ready to be integrated with Amazon ECS.