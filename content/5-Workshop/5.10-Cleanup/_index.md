---
title: "Cleanup Resources"
date: 2026-09-07
weight: 10
chapter: false
pre: "<b> 4.10. </b>"
---

# 4.10. Cleanup

## Overview

After successfully deploying and testing the Warehouse Inventory Management application, the AWS resources created during this workshop should be removed to avoid unnecessary charges.

This section guides you through deleting the deployed infrastructure in a safe order.

---

## Cleanup Steps

The following AWS resources should be removed in sequence:

1. Amazon ECS Service
2. Amazon ECS Cluster
3. Amazon ECR Repository
4. Amazon S3 Bucket
5. Application Load Balancer
6. Target Group
7. Amazon CloudWatch Alarm
8. AWS CodeBuild Project
9. AWS Certificate Manager (ACM) Certificate
10. Amazon Route 53 Hosted Zone

---

## 1. Delete ECS Service

Navigate to:

**Amazon ECS → Clusters → inventory-cluster → Services**

Select:

- inventory-service

Choose:

**Delete Service**

Wait until the service status becomes **Inactive**.


---

## 2. Delete ECS Cluster

Navigate to:

**Amazon ECS → Clusters**

Select:

- inventory-cluster

Choose:

**Delete Cluster**



---

## 3. Delete Amazon ECR Repository

Navigate to:

**Amazon ECR → Private Repositories**

Select:

- inventory-app

Choose:

**Delete**

Confirm repository deletion.


---

## 4. Delete Amazon S3 Bucket

Navigate to:

**Amazon S3**

Select:

- inventory-uploads

Empty the bucket.

Delete the bucket.


---

## 5. Delete Application Load Balancer

Navigate to:

**EC2 → Load Balancers**

Select:

- inventory-alb

Choose:

**Delete**


---

## 6. Delete Target Group

Navigate to:

**EC2 → Target Groups**

Select:

- inventory-tg

Choose:

**Delete**



---

## Result

After completing all cleanup steps:

- Amazon ECS Service has been deleted.
- Amazon ECS Cluster has been deleted.
- Amazon ECR repository has been removed.
- Amazon S3 bucket has been removed.
- Application Load Balancer has been removed.
- Target Group has been removed.
- Amazon CloudWatch alarm has been removed.
