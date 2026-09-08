---
title : "Prerequisite"
date: 2026-09-07
weight : 2
chapter : false
pre : " <b> 4.2. </b> "
---

### Goal

Ensure readers can access the AWS Management Console, create a MongoDB Atlas database account, prepare the required development tools, and set up the Warehouse Inventory Management project source code before deploying to the cloud infrastructure.

---

## 1. Tools to Prepare

This workshop uses the **AWS Management Console (Web UI)** together with basic **Terminal/Command line** tools to build containers and manage AWS resources.

Please prepare the following software and accounts:

- **Node.js (v18+)**: Required for running the application locally.
- **Docker Desktop**: Required for building Docker images.
- **AWS CLI (v2)**: Required to authenticate Docker with the **Amazon ECR** registry from the local machine.
- **MongoDB Compass**: A visual interface for connecting to and inspecting inventory data.
- **MongoDB Atlas account (Cloud)**: A cloud NoSQL database service using the M0 Free Tier.
- **Visual Studio Code (or any preferred IDE)**: For editing the project source code.

---

## 2. Steps

**Log in to AWS Console:** Sign in to the AWS Management Console using your AWS account and ensure the Region is set to **ap-southeast-1 (Singapore)**.

**Checkpoint:** Confirm that the console is using **ap-southeast-1** before creating any resources.

**Verify Local Tools:** Make sure the required software is installed successfully.

```bash
node --version
npm --version
aws --version
docker --version
```

**Checkpoint:** All commands should return valid version numbers.

---

## 3. Expected Result

- Successfully sign in to the AWS Management Console.
- Prepare the complete development environment.
- Complete all prerequisites before proceeding to the next chapter.