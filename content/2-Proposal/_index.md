---
title: "Project Proposal"
date: 2026-09-07
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Warehouse Inventory Management

## A Cloud-Native Warehouse Inventory System on AWS

---

# 1. Executive Summary

Warehouse Inventory Management is a cloud-based web application for managing product categories, tracking inventory quantities, storing product images, and viewing stock statistics. The system uses AWS managed services to provide secure, highly available, and cost-efficient operations.

The application is built with **Node.js**, **Express.js**, **MongoDB Atlas**, and **EJS**. It is packaged with **Docker** and deployed as a serverless container on **Amazon ECS Fargate** behind an **Application Load Balancer (ALB)**. Docker images are stored in **Amazon ECR**, while product images are uploaded to **Amazon S3** through an IAM task role.

**Amazon VPC** isolates the network, **AWS IAM** controls permissions, and **Amazon CloudWatch** collects logs, metrics, and alarms.

---

# 2. Problem and Solution

## Current Problem

Small and medium-sized businesses often manage inventory with local spreadsheets or on-premises applications. This can cause inaccurate stock data, unreliable image storage, difficult maintenance, and service interruptions when the system grows or is updated.

## Proposed Solution

The proposed solution is a cloud-native warehouse management system using AWS managed services:

- **Data storage:** MongoDB Atlas stores item information, quantities, and transaction data.
- **Image storage:** Amazon S3 stores uploaded product images durably and securely.
- **Runtime environment:** Amazon ECS Fargate runs the application without server management.
- **Routing and load balancing:** An Application Load Balancer routes Internet traffic to ECS tasks.
- **Monitoring:** Amazon CloudWatch collects container logs and monitors CPU utilization.

## Benefits

- Standardized deployment with Docker.
- High availability through load balancing.
- Durable product image storage with Amazon S3.
- Reduced operational overhead with serverless Fargate.
- Continuous monitoring through Amazon CloudWatch.

---

# 3. Solution Architecture

The system uses a layered, cloud-native container architecture on AWS.


## AWS Services Used

- Amazon VPC and Security Groups
- AWS IAM
- Amazon ECS Fargate
- Amazon ECR
- Amazon S3
- Application Load Balancer
- Amazon CloudWatch
- MongoDB Atlas

## Technical Components

### Frontend

- HTML5, CSS3, and JavaScript
- EJS Template Engine

### Backend

- Node.js and Express.js
- AWS SDK for JavaScript
- Multer for multipart uploads
- Mongoose for MongoDB connectivity

### Database and Storage

- MongoDB Atlas
- Amazon S3

---

# 4. Technical Implementation

The project is implemented through these phases:

1. Create the VPC, subnets, Internet Gateway, and security groups.
2. Configure MongoDB Atlas and create the Amazon S3 bucket.
3. Create the Dockerfile, build the image, and test the application.
4. Create an Amazon ECR repository and push the Docker image.
5. Configure the ECS task execution role and task role.
6. Create the target group, Application Load Balancer, ECS cluster, task definition, and service.
7. Configure CloudWatch Logs and a CPU utilization alarm.
8. Test the application through the load balancer DNS, add inventory items, upload images to S3, and verify data in MongoDB Atlas.

---

# 5. Estimated Operating Cost

| Service | Estimated usage | Estimated cost |
|:---|:---|:---|
| Amazon ECS Fargate | 1 task, 0.25 vCPU, 0.5 GB RAM | ~0.30 USD/month |
| Application Load Balancer | 1 test ALB | ~0.20 USD/month |
| Amazon S3 | Less than 1 GB and several thousand requests | ~0.05 USD/month |
| Amazon ECR | 1 Docker image under 500 MB | ~0.03 USD/month |
| Amazon CloudWatch | 1 metric alarm and basic logs | ~0.02 USD/month |
| MongoDB Atlas | Shared M0 free cluster | 0.00 USD |
| **Estimated total** | | **~0.60 USD/month** |

---

# 6. Risks and Mitigation

- **Missing IAM permissions:** Grant the task role the permissions required to upload files to Amazon S3.
- **Missing environment variables:** Configure S3_BUCKET_NAME, AWS_REGION, and MONGODB_URI in the ECS task definition.
- **Unhealthy target group:** Verify that the container responds with HTTP 200 on the health check path.
- **Unexpected charges:** Delete the ECS service, cluster, load balancer, target group, and S3 bucket after testing.

---

# 7. Expected Result

- A complete Warehouse Inventory Management application deployed on AWS using containers.
- Stable traffic routing through an Application Load Balancer.
- Product data and images stored securely in MongoDB Atlas and Amazon S3.
- Application health monitored through Amazon CloudWatch.
