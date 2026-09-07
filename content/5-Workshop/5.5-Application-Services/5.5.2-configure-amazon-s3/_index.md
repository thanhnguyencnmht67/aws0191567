---
title : "Configure Amazon S3"
date : 2026-01-01
weight : 2
chapter : false
pre : " <b> 5.5.2. </b> "
---

## Configure Amazon S3

In this section, you will create an Amazon S3 bucket to store product images, documents, and attachments for the Warehouse Inventory Management application.

Amazon S3 provides highly durable, available, and scalable object storage.

---

## Create an S3 Bucket

Navigate to:

**AWS Console → Amazon S3 → Buckets → Create bucket**

Configure the bucket using the following settings.

| Property | Value |
|----------|-------|
| AWS Region | ap-southeast-1 (Singapore) |
| Bucket name | inventory-warehouse-media-<your-name> |
| Object Ownership | ACLs disabled (recommended) |
| Block Public Access | Disable Block all public access |
| Default Encryption | SSE-S3 |

Confirm the public access warning and choose **Create bucket**.

![Create S3 Bucket](/images/5-Workshop/5.5-Application-Services/create-s3-bucket.png)

## Configure the Bucket Policy

To allow users to view inventory images directly in the web interface, configure a public read policy for `s3:GetObject`.

Navigate to **the bucket → Permissions → Bucket policy → Edit** and replace `<your-bucket-name>` with the actual bucket name:

```json
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "PublicReadGetObject",
			"Effect": "Allow",
			"Principal": "*",
			"Action": "s3:GetObject",
			"Resource": "arn:aws:s3:::<your-bucket-name>/*"
		}
	]
}
```

Choose **Save changes**.

---

## Upload Product Images

Open the bucket and choose **Upload**.

Upload one or more product images and documents that will be used by the application.

After the upload is complete, verify that the objects appear in the bucket.

![Upload Objects](/images/5-Workshop/5.5-Application-Services/upload-images.png)

---

## Verify Bucket Content

Navigate to:

**Amazon S3 → Buckets → Your Bucket**

Confirm that the uploaded images are available in the bucket.

These images will be accessed by the application when displaying product information.

![Bucket Objects](/images/5-Workshop/5.5-Application-Services/bucket-object.png)

---

## Expected Result

After completing this section, you will have:

- An Amazon S3 bucket created.
- Product images uploaded successfully.
- Image objects stored in Amazon S3 and ready to be accessed by the application.