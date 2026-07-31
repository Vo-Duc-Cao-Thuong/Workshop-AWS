---
title : "Deploy Frontend on Amazon S3"
date : 2026-07-24
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

#### Step 1: Create an Amazon S3 Bucket for Static Web Hosting

1. Open **AWS Management Console** ➔ Navigate to **Amazon S3**.
2. Click **Create bucket**.
   - **Bucket name:** `fav-web-frontend-bucket` (or any unique bucket name).
   - **AWS Region:** Select `ap-southeast-2` (Sydney) or your preferred region.
   - **Object Ownership:** ACLs disabled (recommended).
3. Under **Block Public Access settings for this bucket**:
   - Uncheck **Block *all* public access** to allow public web access.
   - Acknowledge the confirmation warning.
4. Click **Create bucket**.

#### Step 2: Enable Static Website Hosting

1. Select your created bucket ➔ Go to the **Properties** tab.
2. Scroll to the bottom to **Static website hosting** ➔ Click **Edit**.
   - Select **Enable**.
   - Hosting type: **Host a static website**.
   - **Index document:** `index.html`.
   - **Error document:** `index.html`.
3. Click **Save changes**.

#### Step 3: Build Frontend Targeting EC2 Backend IP

On your local machine, open PowerShell inside the `frontend/` directory:

```powershell
cd d:\file_hoc_tap\Fav_Web\frontend

# Set VITE_API_URL targeting your Public EC2 IP
$env:VITE_API_URL="http://52.63.251.110/api/v1"

# Build production assets
npm run build
```

Upon build completion, the output directory `frontend/dist/` will contain `index.html` and assets.

#### Step 4: Upload `frontend/dist/` Contents to S3

1. Inside your S3 Bucket `fav-web-frontend-bucket`, switch to the **Objects** tab.
2. Click **Upload** ➔ Drag and drop all files and folders inside `frontend/dist/`.
3. Click **Upload** to finish.