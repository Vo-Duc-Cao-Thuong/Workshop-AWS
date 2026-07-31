---
title : "Deploy FastAPI Docker Backend on Amazon EC2"
date : 2026-07-24
weight : 4
chapter: false
pre : " <b> 5.4. </b> "
---

#### Step 1: SSH into Amazon EC2 Instance

Open Terminal / PowerShell on your local machine:

```bash
ssh -i ec2_key.pem ubuntu@52.63.251.110
```

#### Step 2: Clone Project Repository

On the EC2 SSH shell:

```bash
git clone https://github.com/RuMeoDiNhau/Favourite-Web.git
cd ~/Favourite-Web
```

#### Step 3: Create Environment Configuration File `.env`

Create `~/Favourite-Web/.env` containing AWS credential configurations:

```bash
cat << 'EOF' > ~/Favourite-Web/.env
AWS_ACCESS_KEY_ID=YOUR_AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY=YOUR_AWS_SECRET_ACCESS_KEY
AWS_STORAGE_BUCKET_NAME=fav-web-storage-bucket
AWS_S3_REGION_NAME=ap-southeast-2
JWT_SECRET=super-secret-key-change-in-production
COOKIE_SECURE=false
EOF
```

#### Step 4: Build FastAPI Docker Image

```bash
cd ~/Favourite-Web/backend
docker build -t fav-web-backend .
```

#### Step 5: Create Persist Volume Directories & Run Container

```bash
mkdir -p ~/Favourite-Web/database
mkdir -p ~/Favourite-Web/static/logs
mkdir -p ~/Favourite-Web/backend/ai_core/data/embeddings

# Stop & remove old container if present
docker stop backend-service || true
docker rm backend-service || true

# Run Backend Container with volume mounts
docker run -d \
  --name backend-service \
  -p 80:8000 \
  --env-file ~/Favourite-Web/.env \
  -v ~/Favourite-Web/database:/app/database \
  -v ~/Favourite-Web/static:/app/static \
  -v ~/Favourite-Web/backend/ai_core/data:/app/backend/ai_core/data \
  fav-web-backend
```

#### Step 6: Verify Backend Health

```bash
docker ps
curl -i http://localhost/
```
Expected Output: `{"message": "Backend is running"}`.
