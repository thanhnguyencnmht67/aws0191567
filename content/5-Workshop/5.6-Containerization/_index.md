---
title : "Containerization"
date : 2026-01-01
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

### Goal

Containerize the Warehouse Inventory Management application and push the container image to Amazon Elastic Container Registry (Amazon ECR) for deployment on Amazon ECS Fargate.

---

## 1. Overview

In this chapter, you will package the web inventory application into a complete container image:

- **Dockerfile and .dockerignore:** Define the runtime environment and exclude unnecessary files to optimize the image.
- **Docker build:** Build and test the container image locally.
- **Amazon ECR:** Create a private repository, authenticate with the AWS CLI, and push the image to AWS.

After completion, the image stored in Amazon ECR will be the primary artifact that Amazon ECS Fargate pulls and runs as a task.

---

## 2. Practice Content

Complete the following sections in order:

- **5.6.1 Create the Dockerfile and .dockerignore** (define the container build process)
- **5.6.2 Create a private repository on Amazon ECR** (create the AWS image repository)
- **5.6.3 Build and push the Docker image to Amazon ECR** (authenticate the CLI, build for amd64, and push the image)

---

## 3. Expected Result

After completing this chapter, you will have:

- A standardized Dockerfile and `.dockerignore` for the inventory application.
- An Amazon ECR private repository named **inventory-app**.
- A Docker container image built successfully for the `linux/amd64` architecture.
- An image tagged and securely stored in Amazon ECR, ready for configuring the ECS task definition in Chapter 5.7.