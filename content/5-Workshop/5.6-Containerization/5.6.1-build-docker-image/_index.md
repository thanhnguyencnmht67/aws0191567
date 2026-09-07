---
title : "Build Docker Image"
date : 2026-01-01
weight : 1
chapter : false
pre : " <b> 5.6.1. </b> "
---

## Build Docker Image

In this section, you will create a Dockerfile, a `.dockerignore` file, and build a Docker image for the Warehouse Inventory Management application.

Docker packages the application source code and its dependencies into an isolated container, ensuring a consistent runtime environment between the local development machine and Amazon ECS Fargate.

## Create the .dockerignore File

In the project root directory, create a file named **.dockerignore**. This prevents large directories, sensitive configuration files, and temporary files from being copied into the container image:

```text
node_modules
npm-debug.log
.env
.git
.gitignore
README.md
```

---

## Create the Dockerfile

Open the project folder and create a file named **Dockerfile** in the root directory.

The Dockerfile used in this project is shown below.

```dockerfile
FROM node:20-alpine

# Working directory inside the container
WORKDIR /app

# Copy dependency files first to use the Docker cache
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the application source code
COPY . .

# Expose port 80 for the web application
EXPOSE 80

# Start the application
CMD ["npm", "start"]
```

Save the Dockerfile after completing the configuration.

![Dockerfile](/images/5-Workshop/5.6-Containerization/dockerfile.png)

---

## Build the Docker Image

After creating the Dockerfile, open a terminal in the project root directory and build the Docker image.

Run the following command:

```bash
docker build -t inventory-app .
```

Docker performs the following operations during the build process:

1. Downloads the Node.js 20 Alpine base image from Docker Hub if it is not available locally.
2. Creates the `/app` working directory inside the container.
3. Installs the application dependencies using **npm install**.
4. Copies the project source code into the container, excluding files listed in `.dockerignore`.
5. Packages the application into a complete Docker image.

To verify that the image was created successfully, run:

```bash
docker images
```

The command displays all Docker images stored on the local machine. Confirm that the newly created **inventory-app** image appears in the list with the **latest** tag.

---

## Expected Result

After completing this section, you will have:

- A standardized `.dockerignore` file and Dockerfile for the inventory management application.
- A Docker image named **inventory-app** built successfully on the local machine.
- A container image ready to be tagged and pushed to Amazon Elastic Container Registry (Amazon ECR) in the next section.