---
title : "Các bước chuẩn bị"
date : 2026-07-24
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

#### Các công cụ & Môi trường cần chuẩn bị

Để thực hiện workshop triển khai **Fav Web Portal** lên AWS, bạn cần chuẩn bị các công cụ và tài khoản sau:

1. **Tài khoản AWS (AWS Account):**
   - Đã khởi tạo và có quyền quản trị (AdministratorAccess).
   - Quyền truy cập các dịch vụ: Amazon S3, Amazon EC2, AWS IAM, Amazon CloudWatch.

2. **Môi trường phát triển ở Máy Local:**
   - **Git:** Đã cài đặt Git CLI (`git --version`).
   - **Node.js & npm:** Phiên bản Node.js 18.x trở lên (`node -v` và `npm -v`).
   - **Python:** Phiên bản Python 3.10 trở lên (`python --version`).
   - **SSH Client:** PowerShell (Windows) hoặc OpenSSH Terminal để kết nối tới EC2.

3. **Tài nguyên AWS EC2:**
   - Đã tạo **EC2 Key Pair** (tệp `.pem`, ví dụ: `ec2_key.pem`) dùng để SSH vào máy chủ.
   - Chọn OS **Ubuntu 22.04 LTS / Ubuntu 24.04 LTS** trên EC2 Instance.

4. **Tải Mã nguồn Dự án:**
   ```bash
   git clone https://github.com/RuMeoDiNhau/Favourite-Web.git
   cd Favourite-Web
   ```