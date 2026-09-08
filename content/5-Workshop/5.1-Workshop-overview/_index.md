---
title : "Workshop Overview"
date: 2026-09-07
weight : 1
chapter : false
pre : " <b> 4.1. </b> "
---

### Goal

This workshop demonstrates how to deploy a **Warehouse Inventory Management** application on AWS using a cloud-native architecture, managed services, container deployment, and cloud storage. After completing this workshop, you will be able to deploy a complete warehouse management web application with scalability, high availability, and security.

---

## 1. Use Case and Solution Overview

**Warehouse Inventory Management** is a web application that allows users to manage product catalogs, monitor inventory, and update stock quantities in real time. The system supports features such as adding new items by SKU, uploading product images, increasing or decreasing inventory quantities, and displaying an intuitive warehouse list.

Instead of deploying the application on a traditional server, this workshop adopts a cloud-native architecture on AWS. The application is containerized using **Docker** and deployed on **Amazon ECS Fargate**, product images are stored in **Amazon S3**, and application data is stored in **MongoDB Atlas**.

To improve security and manageability, sensitive information, such as the database connection string, is stored in **AWS Secrets Manager**. The **Application Load Balancer** distributes traffic over HTTP port 80. The **Docker image** is stored and managed directly through **Amazon ECR**, and the system is monitored through **Amazon CloudWatch**.

---

## 2. System Architecture

The system architecture consists of the following major components:

- Client
- Load Balancer
- Network Infrastructure
- Containerized Application
- Storage Services
- Docker Image Management
- Security and Monitoring

**Figure 1 – Warehouse Inventory Management System Architecture**


---

## 3. System Workflow

The main system workflow consists of the following steps:

1. Users access the website through the public DNS address of the **Application Load Balancer (ALB)**.

2. All user requests are sent directly over HTTP port 80 to the **Application Load Balancer (ALB)**.

3. The ALB distributes traffic to containers running on **Amazon ECS Fargate**.

4. The Node.js application processes business logic and communicates with **MongoDB Atlas** to store and retrieve data.

5. Product images are uploaded and stored in **Amazon S3**.

6. Sensitive configuration information, such as the database connection string, is retrieved from **AWS Secrets Manager**.

7. Application logs and system metrics are sent to **Amazon CloudWatch** for monitoring and troubleshooting.

8. A Docker image is built locally, pushed to **Amazon ECR**, and deployed as a new version on **Amazon ECS**.


---

## 4. Services Used

This workshop uses the following AWS services:

### Network Infrastructure

- Amazon VPC
- Public Subnet
- Internet Gateway
- Security Groups

### Compute Services

- Amazon ECS Fargate
- Application Load Balancer

### Storage

- Amazon S3
- MongoDB Atlas

### Container

- Docker
- Amazon Elastic Container Registry (Amazon ECR)

### Security

- AWS IAM
- AWS Secrets Manager

### Monitoring

- Amazon CloudWatch

---

## 5. Learning Outcomes

After completing this workshop, you will be able to:

- Deploy a Node.js application as a container on Amazon ECS Fargate.
- Build network infrastructure using Amazon VPC and an Internet Gateway.
- Connect to and use MongoDB Atlas as the database.
- Store product images in Amazon S3.
- Protect configuration information using AWS Secrets Manager.
- Configure traffic distribution using the Application Load Balancer (ALB).
- Build a Docker image and manage its versions in Amazon ECR.
- Monitor application activity and logs through Amazon CloudWatch.
- Delete all AWS resources after completing the workshop to avoid unnecessary costs.