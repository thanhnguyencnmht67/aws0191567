---
title : "Prepare Project"
date : 2026-01-01
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

## Prepare the Project

In this section, you will prepare the **Warehouse Inventory Management** application source code, install the required dependencies, configure the environment variables, and successfully test the application locally before building the Docker image for AWS.

---

## Download the Project Source Code

Open a Terminal on your local computer and navigate to the project working directory:

```bash
cd quanlkhohang
```

---

## Install the Dependencies

Install all required Node.js packages.

```bash
npm install
```

Wait until the installation completes successfully.

---

## Configure the Environment Variables

Create a `.env` file in the project root directory and provide the service connection information.

Example:

```text
PORT=80
MONGODB_URI=<your-mongodb-uri>
AWS_REGION=ap-southeast-1
S3_BUCKET_NAME=<your-s3-bucket>
```

![Configure Environment Variables](/images/5-Workshop/5.3-Project-foundation/env-file.png)

---

## Start the Application

Start the application using the following command:

```text
node server.js
```

After the Terminal displays successful connection messages:

```text
Inventory App running on port 80
Connected to MongoDB Atlas
```

Open a web browser and navigate to:

```text
http://localhost
```

![Run the Application](/images/5-Workshop/5.3-Project-foundation/run-localhost.png)

---

## Expected Outcome

After completing this section, you will have:

- The complete source structure for the Warehouse Inventory Management application.
- All required dependencies installed in `node_modules`.
- A correctly configured `.env` file connected to MongoDB Atlas and Amazon S3.
- The application running successfully locally, with inventory in/out functions and the user interface tested.