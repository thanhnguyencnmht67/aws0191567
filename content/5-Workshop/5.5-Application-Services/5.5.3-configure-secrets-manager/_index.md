---
title : "Configure AWS Secrets Manager"
date: 2026-09-07
weight : 3
chapter : false
pre : " <b> 4.5.3. </b> "
---

## Configure AWS Secrets Manager

In this section, you will use AWS Secrets Manager to securely store sensitive configuration values and environment variables for the Warehouse Inventory Management application.

This protects the database connection string and credentials from being hardcoded in the source code or Dockerfile.

---

## Create a Secret

Navigate to:

**AWS Console → AWS Secrets Manager → Secrets → Store a new secret**

Select **Other type of secret**.

Enter the following application configuration values. Replace the example values with your own:

| Key | Example value |
| :--- | :--- |
| PORT | 80 |
| MONGODB_URI | mongodb+srv://inventory_admin:<password>@cluster0... |
| AWS_REGION | ap-southeast-1 |
| S3_BUCKET_NAME | <your-bucket-name> |
| SESSION_SECRET | <generate-a-strong-secret> |

Choose **Next** to continue.


---

## Configure Secret Details

Provide a name for the secret.

Example:

| Property | Value |
|----------|-------|
| Secret name | inventory-app-secrets |
| Description | Environment variables for Warehouse Inventory Management |

Choose **Next** and keep the remaining settings as default.


Keep automatic rotation disabled unless a rotation strategy has been configured, then choose **Store**.

## Get the Secret ARN

Open inventory-app-secrets, copy its **Secret ARN**, and use that ARN when configuring the Amazon ECS task definition.

---

## Verify the Secret

Navigate to:

**AWS Console → Secrets Manager → Secrets**

Confirm that inventory-app-secrets appears in the list.

The application will retrieve this secret during deployment on Amazon ECS.


---

## Expected Result

After completing this section, you will have:

- A secret created in AWS Secrets Manager.
- The application environment variables securely stored.
- The Secret ARN ready to be used by the Amazon ECS task.