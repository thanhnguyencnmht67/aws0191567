---
title : "Deploy Application to Amazon ECS"
date: 2026-09-07
weight : 2
chapter : false
pre : " <b> 4.7.2. </b> "
---

## Deploy Application to Amazon ECS

In this section, you will deploy the Warehouse Inventory Management application to Amazon ECS using AWS Fargate.

The deployment process includes creating the ECS cluster, configuring a task definition, creating an ECS service, and associating the service with the existing Application Load Balancer.

---

## Create an ECS Cluster

Navigate to **Amazon ECS → Clusters → Create cluster** and create a cluster named inventory-cluster using AWS Fargate.

![Create ECS Cluster](/images/5-Workshop/5.7-Deploy-Application/5.7.2.1.png)

---

## Create an ECS Cluster

Navigate to **Amazon ECS -> Clusters -> Create cluster** and create a cluster named inventory-cluster using AWS Fargate.

![Create ECS Cluster](/images/5-Workshop/5.7-Deploy-Application/5.7.2.1.png)

---

## Create a Task Definition

Navigate to:

**AWS Console → Amazon ECS → Task definitions → Create new task definition**

Configure the task definition using the following settings.

| Property | Value |
|----------|-------|
| Launch type | AWS Fargate |
| Task definition family | inventory-task |
| Operating system | Linux |
| CPU | 0.5 vCPU or 1 vCPU |
| Memory | 1 GB or 2 GB |

Choose **Next** to configure the container.

![Task Definition](/images/5-Workshop/5.7-Deploy-Application/5.7.2.2.png)

---

## Configure the Container

Configure the container using the Docker image stored in Amazon ECR.

| Property | Value |
|----------|-------|
| Container name | inventory-app |
| Image URI | Amazon ECR Image |
| Container port | 80 |

Configure the required environment variables and secrets, then create the task definition.

![Container Configuration](/images/5-Workshop/5.7-Deploy-Application/5.7.2.2.png)

---

## Create an ECS Service

Navigate to:

**Amazon ECS → Clusters → inventory-cluster → Create**

Configure the service using the following settings.

| Property | Value |
|----------|-------|
| Launch type | AWS Fargate |
| Task definition | inventory-task |
| Service name | inventory-service |
| Desired tasks | 1 |

Continue to the networking configuration.

![Create Service](/images/5-Workshop/5.7-Deploy-Application/5.7.2.3.png)

---

## Configure Networking

Configure the ECS service networking.

| Property | Value |
|----------|-------|
| VPC | inventory-vpc |
| Subnets | Private Subnets |
| Security Group | inventory-ecs-sg |
| Public IP | Enabled for public subnets, or disabled for private subnets with NAT Gateway |

For the Load Balancer section:

- Select **Use existing load balancer**.
- Choose the Application Load Balancer created in the previous section.
- Select the existing Target Group.

Review the configuration and choose **Create**.

![Networking Configuration](/images/5-Workshop/5.7-Deploy-Application/5.7.2.3.png)

---

## Verify the Deployment

Navigate to:

**Amazon ECS → Clusters → inventory-cluster → Services**

Verify that:

- Service status is **Active**.
- Running tasks equal the desired tasks.
- The task status is **Running**.

![Service Running](/images/5-Workshop/5.7-Deploy-Application/5.7.2.3.png)

---

## Expected Result

After completing this section, you will have:

- A Task Definition created.
- An ECS Service deployed successfully.
- The application running on AWS Fargate.
- Amazon ECS integrated with the existing Application Load Balancer.