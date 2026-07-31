---
title : "Dọn dẹp tài nguyên"
date : 2026-07-24
weight : 7
chapter : false
pre : " <b> 5.7. </b> "
---

#### Dọn dẹp tài nguyên trên AWS

Sau khi hoàn thành bài thực hành (Workshop) và chụp ảnh chứng minh kết quả, bạn cần tiến hành dọn dẹp các tài nguyên trên AWS để tránh phát sinh chi phí ngoài ý muốn:

#### 1. Dừng & Xóa Docker Container trên EC2

SSH vào EC2:
```bash
docker stop backend-service
docker rm backend-service
```

#### 2. Terminate hoặc Stop EC2 Instance

1. Mở **AWS Management Console** ➔ Truy cập **EC2** ➔ **Instances**.
2. Chọn EC2 Instance chạy Fav Web Backend.
3. Chọn **Instance state** ➔ Chọn **Stop instance** (tạm dừng) hoặc **Terminate instance** (xóa hẳn).

#### 3. Xóa Amazon S3 Buckets

1. Mở **Amazon S3 Console**.
2. Chọn bucket `fav-web-frontend-bucket` (và bucket lưu trữ media/embeddings).
3. Nhấn **Empty** để xóa toàn bộ các tệp tin bên trong bucket.
4. Nhấn **Delete** để xóa hẳn Bucket.

#### 4. Xóa EC2 Key Pair & Security Group (Tùy chọn)

1. Vào **EC2 Console** ➔ **Key Pairs** ➔ Xóa key pair `ec2_key.pem`.
2. Vào **Security Groups** ➔ Xóa Security Group đã tạo cho bài lab.