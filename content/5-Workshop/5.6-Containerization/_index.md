---
title : "Containerization"
date: 2026-09-07
weight : 6
chapter : false
pre : " <b> 4.6. </b> "
---

### Goal

Containerize the Warehouse Inventory Management application and push the container image to Amazon Elastic Container Registry (Amazon ECR) in preparation for deployment on Amazon ECS Fargate.

---

## 1. Overview

In this chapter, you will package the web inventory application into a complete container image:

- **Dockerfile and .dockerignore:** Define the standard runtime environment, including the Node.js LTS runtime, dependencies, and source code, while excluding unnecessary files to optimize the image.
- **Docker build on AWS CloudShell:** Use the built-in Docker engine to build and test a container image compatible with the Linux x86_64 infrastructure used by Amazon ECS Fargate.
- **Amazon ECR:** Create a private repository, authenticate with the AWS CLI, and push the image to the secure AWS registry.

After completion, the container image stored in Amazon ECR will be the primary artifact that Amazon ECS Fargate pulls and runs as a task.

---

## 2. Practice Content

Complete the following sections in order:

- **4.6.1 Build the Docker image** (create the Dockerfile and `.dockerignore`, then build the image on AWS CloudShell)
- **4.6.2 Create a private repository and push the Docker image to Amazon ECR** (create the repository, authenticate Docker, tag the image, and push it to ECR)

---

## 3. Expected Result

After completing this chapter, you will have:

- A standardized Dockerfile and `.dockerignore` for the inventory application.
- An Amazon ECR private repository named **inventory-app**.
- A Docker container image built successfully for the `linux/amd64` architecture on AWS CloudShell.
- An image tagged and securely stored in Amazon ECR, ready for configuring the ECS task definition in Chapter 4.7.