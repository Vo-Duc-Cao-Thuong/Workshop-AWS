---
title : "Triển khai Backend Docker trên Amazon EC2"
date : 2026-07-24
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

#### Bước 1: Kết nối SSH vào máy chủ EC2 Instance

Mở Terminal / PowerShell ở máy local và thực thi:

```bash
ssh -i ec2_key.pem ubuntu@52.63.251.110
```

#### Bước 2: Clone Mã nguồn Dự án từ GitHub

Trực tiếp trên SSH EC2:

```bash
git clone https://github.com/RuMeoDiNhau/Favourite-Web.git
cd ~/Favourite-Web
```

#### Bước 3: Tạo File Môi trường `.env` trên EC2

Tạo file `.env` tại thư mục gốc `~/Favourite-Web/.env` chứa thông tin cấu hình AWS S3 và Secret key:

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

#### Bước 4: Build Docker Image Backend FastAPI

```bash
cd ~/Favourite-Web/backend
docker build -t fav-web-backend .
```

#### Bước 5: Khởi tạo Thư mục Persist Volume & Khởi chạy Container

Để giữ lại cơ sở dữ liệu SQLite và tệp lưu trữ media khi rebuild container:

```bash
mkdir -p ~/Favourite-Web/database
mkdir -p ~/Favourite-Web/static/logs
mkdir -p ~/Favourite-Web/backend/ai_core/data/embeddings

# Stop & remove container cũ nếu có
docker stop backend-service || true
docker rm backend-service || true

# Khởi chạy Backend Container với Volume mounts
docker run -d \
  --name backend-service \
  -p 80:8000 \
  --env-file ~/Favourite-Web/.env \
  -v ~/Favourite-Web/database:/app/database \
  -v ~/Favourite-Web/static:/app/static \
  -v ~/Favourite-Web/backend/ai_core/data:/app/backend/ai_core/data \
  fav-web-backend
```

#### Bước 6: Kiểm tra Trạng thái Khởi chạy Backend

```bash
docker ps
curl -i http://localhost/
```
Response mong đợi: `{"message": "Backend is running"}`.
