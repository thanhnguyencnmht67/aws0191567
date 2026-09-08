---
title: "Testing"
date: 2026-09-07
weight: 9
chapter: false
pre: " <b> 4.9. </b> "
---

# 4.9. Testing

This section demonstrates the main workflows of the **Warehouse Inventory Management** application after deployment to AWS. The application runs on Amazon ECS Fargate behind an Application Load Balancer and uses MongoDB Atlas, Amazon S3, Amazon ECR, and Amazon CloudWatch.

---

## Demo Video

Watch the complete system demonstration here:

**YouTube:** https://www.youtube.com/watch?v=rQFgAupfTeA

---

# 1. Inventory Management Interface

The application is a single-page interface that combines the inventory dashboard, item entry form, and stock management controls.

## A. Dashboard and Inventory Summary

The dashboard displays three key metrics:

- **Total item categories:** The number of item types currently registered.
- **Total inventory quantity:** The total number of units stored in the warehouse.
- **Items requiring restock:** A warning shown when an item's quantity falls below the safe level.

### Infrastructure Integration

The Node.js Express application runs in a container on **Amazon ECS Fargate** and is exposed through an **Application Load Balancer**. Inventory statistics are queried from **MongoDB Atlas**.

## Data Flow

Users access the application through the load balancer DNS name.

1. The Application Load Balancer receives the HTTP request and forwards it to an ECS task.
2. The container running on ECS Fargate queries MongoDB Atlas.
3. The application renders the dashboard and inventory list.

---

## B. Add an Item and Upload an Image

An administrator can add an item by entering its **SKU**, **product name**, **initial quantity**, and **product image**.

### Infrastructure Integration

- **Image storage:** The Node.js backend uploads the image to an Amazon S3 bucket using the AWS SDK.
- **Application data:** The SKU, item name, quantity, and image URL are stored in MongoDB Atlas.
- **IAM task role:** The ECS task role provides the permissions required to write the image to S3.

---

## C. Stock In and Stock Out Actions

The inventory table provides two actions for each item:

- **Stock in (+1):** Increases the item quantity by one unit.
- **Stock out (-1):** Decreases the item quantity by one unit. The restock warning is activated when the quantity reaches the configured threshold.

### Infrastructure Integration

When a user selects Stock in or Stock out, an HTTP request is sent through the load balancer to ECS. The container updates the quantity in MongoDB Atlas and refreshes the displayed inventory statistics.

---

# 2. AWS Services Used

| AWS service | Purpose |
|-------------|----------|
| Amazon ECS Fargate | Runs the Node.js Express application |
| Amazon ECR | Stores the Docker image |
| Application Load Balancer | Receives HTTP traffic and routes requests to ECS tasks |
| Target Group | Registers Fargate task IP addresses and performs health checks |
| Amazon S3 | Stores uploaded item images |
| MongoDB Atlas | Stores item information, inventory quantities, and image URLs |
| Amazon CloudWatch Logs | Collects container runtime logs |
| Amazon CloudWatch Alarms | Monitors ECS service CPU utilization |
| AWS IAM | Controls task execution and application permissions |

Successful dashboard loading, item creation, image upload, and stock updates through the load balancer confirm that the **Warehouse Inventory Management** application is deployed and operating correctly on AWS.
