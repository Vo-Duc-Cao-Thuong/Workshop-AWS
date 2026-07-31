---
title : "Resource Cleanup"
date : 2026-07-24
weight : 7
chapter : false
pre : " <b> 5.7. </b> "
---

#### Cleaning Up AWS Resources

After finishing the workshop and documenting your test results, clean up all provisioned AWS resources to prevent unnecessary cloud costs:

#### 1. Stop & Remove Docker Container on EC2

SSH into EC2 shell:
```bash
docker stop backend-service
docker rm backend-service
```

#### 2. Terminate or Stop Amazon EC2 Instance

1. Open **AWS Management Console** ➔ Navigate to **EC2** ➔ **Instances**.
2. Select your Fav Web Backend EC2 Instance.
3. Click **Instance state** ➔ Choose **Stop instance** or **Terminate instance**.

#### 3. Delete Amazon S3 Buckets

1. Open **Amazon S3 Console**.
2. Select `fav-web-frontend-bucket` (and media/embeddings storage bucket).
3. Click **Empty** to clear all stored objects.
4. Click **Delete** to delete the bucket.

#### 4. Delete EC2 Key Pair & Security Group (Optional)

1. Navigate to **EC2 Console** ➔ **Key Pairs** ➔ Delete `ec2_key.pem`.
2. Navigate to **Security Groups** ➔ Delete lab Security Group.