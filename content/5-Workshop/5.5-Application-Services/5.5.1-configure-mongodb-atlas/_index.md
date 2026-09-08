---
title : "Configure MongoDB Atlas"
date: 2026-09-07
weight : 1
chapter : false
pre : " <b> 4.5.1. </b> "
---

## Configure MongoDB Atlas

In this section, you will configure MongoDB Atlas as the cloud NoSQL database for the Warehouse Inventory Management application.

MongoDB Atlas stores product information, inventory categories, stock quantities, and inventory receipt and issue history.

---

## Create a Database Cluster

1. Sign in to the [MongoDB Atlas Console](https://cloud.mongodb.com/).
2. Navigate to:

**Deployment → Database**

3. Choose the **M0 (Free Tier)**, select **AWS**, and choose **Singapore (ap-southeast-1)** to reduce latency from the VPC.
4. Enter a cluster name, such as Cluster0 or InventoryCluster, and choose **Create Deployment**.

5. After creation, verify that the cluster status is **Available** or **Active**.


---

## Create a Database User

Navigate to:

**Security → Database Access**

Create a database user with the following configuration:

| Property | Value |
|----------|-------|
| Authentication Method | Password |
| Username | inventory_admin |
| Database User Privileges | Read and write to any database |

Save the username and password for later use.


---

## Configure Network Access

Navigate to:

**Security → Network Access**

Add the IP addresses that are allowed to connect to the database.

For development purposes, you may temporarily allow access from all IP addresses.

| Property | Value |
|----------|-------|
| Access List Entry | 0.0.0.0/0 |
| Comment | Allow ECS tasks and local development |

After deployment, replace this with the appropriate public IP address or CIDR range.


---

## Obtain the Connection String

1. In **Database Deployments**, choose **Connect** for your cluster.

2. Choose **Drivers** for Node.js and copy the MongoDB connection string.

Example:

```text
mongodb+srv://inventory_admin:<password>@cluster0.xxxxx.mongodb.net/warehouse_db?retryWrites=true&w=majority
```

This connection string will be stored securely using AWS Secrets Manager in a later section.


---

## Expected Result

After completing this section, you will have:

- A MongoDB Atlas cluster ready for use.
- A database user configured.
- Network access configured.
- A MongoDB connection string ready for the application.