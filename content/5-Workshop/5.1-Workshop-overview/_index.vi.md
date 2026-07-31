---
title : "Tổng quan Workshop & Kiến trúc"
date : 2026-07-24
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

#### Giới thiệu về Fav Web Portal

**Fav Web Portal** là một ứng dụng Web đa dịch vụ được thiết kế với kiến trúc hiện đại, kết hợp khả năng xác thực sinh trắc học (Face ID AI Recognition) và các dịch vụ truyền thông đa phương tiện.

Ứng dụng đáp ứng các yêu cầu:
- **Tính sẵn sàng cao & Tối ưu chi phí:** Phân tách Frontend tĩnh (Amazon S3 Static Website Hosting) và Backend tính toán (Amazon EC2 Docker Container).
- **An toàn bảo mật:** Áp dụng mô hình xác thực sinh trắc học + JWT token với cơ chế cookie & Bearer token header fallback, tuân thủ nghiêm ngặt quy định CORS và Content Security Policy (CSP).
- **Lưu trữ dữ liệu mở rộng:** Sử dụng Amazon S3 lưu trữ các tệp media và vector đặc trưng khuôn mặt (`.npy`).

#### Giao diện thực tế Ứng dụng (Fav Web Portal)

![Giao diện Trang chủ Fav Web Portal](/images/dashboard.png)

#### Tổng quan về Mô hình Triển khai AWS Architecture

![Architecture](/images/aws_architecture.png)

1. **Client (Browser):** Người dùng truy cập website qua tên miền S3 Bucket Static Hosting (`fav-web-frontend-bucket`).
2. **Frontend Layer (AWS S3 Static Web):** Chạy ứng dụng React/Vite được build tối ưu, tự động gọi API tới Backend EC2.
3. **Backend Layer (AWS EC2 Instance):** Vận hành container Docker chứa ứng dụng FastAPI + Uvicorn + Mô hình Deep Learning Face Recognition (`facenet-pytorch`/`insightface`).
4. **Database & Storage Layer (AWS RDS / S3):** Lưu trữ dữ liệu quan hệ người dùng, bài đăng, bản ghi âm nhạc/game và lưu trữ tệp đa phương tiện trên S3 Object Storage.
