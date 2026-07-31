---
title: "Bản đề xuất"
date: 2026-07-24
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Fav Web Portal
## Cổng thông tin & Giải trí đa phương tiện tích hợp AI Nhận diện khuôn mặt trên Cloud

### 1. Tóm tắt điều hành
Dự án **Fav Web Portal** được phát triển nhằm cung cấp một hệ thống Cổng thông tin & Giải trí đa dịch vụ tích hợp công nghệ trí tuệ nhân tạo (AI/ML Face Recognition) và kiến trúc điện toán đám mây linh hoạt trên **Amazon Web Services (AWS)**. Hệ thống kết hợp khả năng xác thực sinh trắc học (Face ID) với các dịch vụ mạng xã hội đa phương tiện (Bảng tin feed, Kho nhạc trực tuyến, Tin tức game, Thư viện chia sẻ kiến thức, Hệ thống bookmark, bình luận và phản hồi thời gian thực).

### 2. Tuyên bố vấn đề

**Vấn đề hiện tại:**
- Các ứng dụng web hiện nay thường tách rời giữa dịch vụ giải trí/thông tin và cơ chế xác thực sinh trắc học hiện đại.
- Việc lưu trữ dữ liệu truyền thông đa phương tiện (hình ảnh, âm thanh, bài viết) và các mô hình vector nhận diện khuôn mặt sinh trắc học đòi hỏi hạ tầng lưu trữ đám mây có độ tin cậy cao, chi phí tối ưu và khả năng mở rộng tốt.
- Vấn đề bảo mật token/cookie xác thực khi triển khai frontend tĩnh (Static Web Hosting) kết hợp backend API cross-domain trên cloud dễ bị trình duyệt chặn nếu không cấu hình đúng CORS/CSP và cơ chế Fallback (JWT + Bearer Token).

**Giải pháp:**
- Xây dựng **Fav Web Portal** sử dụng **AWS S3** làm hạ tầng lưu trữ tệp tin tĩnh (Static Web Hosting) và lưu trữ tệp đa phương tiện/vector khuôn mặt.
- Triển khai **AWS EC2** để vận hành Backend Container hóa (Docker) chạy framework **FastAPI / Python** tích hợp thư viện Deep Learning nhận diện khuôn mặt (`facenet-pytorch` / `insightface`).
- Sử dụng **AWS RDS PostgreSQL** (hoặc SQLite linh hoạt) để lưu trữ dữ liệu quan hệ an toàn.
- Cấu hình cơ chế bảo mật xác thực kép (HttpOnly Cookie kết hợp Bearer Token Header Fallback) và tích hợp các chính sách bảo mật CORS, Content Security Policy (CSP) chặt chẽ.

---

### 3. Kiến trúc giải pháp (AWS Architecture)

![Fav Web Architecture](/images/aws_architecture.png)

**Các dịch vụ AWS sử dụng:**
- **Amazon S3 (Simple Storage Service):**
  - Hosting trang web tĩnh React/Vite (`fav-web-frontend-bucket`).
  - Lưu trữ ảnh người dùng, bài đăng đa phương tiện, file âm thanh nhạc và dữ liệu vector đặc trưng khuôn mặt (`.npy`).
- **Amazon EC2 (Elastic Compute Cloud):**
  - Chạy Docker Container cho Backend FastAPI (Web API service & AI Inference Model).
- **Amazon RDS PostgreSQL:**
  - Cơ sở dữ liệu quan hệ đám mây lưu trữ người dùng, bài viết, nhạc, game, bình luận và nhật ký hoạt động.
- **Amazon CloudWatch:**
  - Giám sát log ứng dụng và tài nguyên hệ thống.

---

### 4. Triển khai kỹ thuật & Tính năng cốt lõi

**Các thành phần chính:**
1. **Module AI Face ID:** Đăng ký và đăng nhập nhanh bằng Camera máy tính/điện thoại qua thuật toán trích xuất vector khuôn mặt.
2. **Module Media & Feed:** Đăng bài đa phương tiện, bình luận, reaction, tương tác thời gian thực.
3. **Module Knowledge & Collections:** Chia sẻ tài liệu kiến thức, lưu bookmark, phân loại bộ sưu tập.
4. **Module Music & Games:** Phát nhạc trực tuyến, xem và tương tác tin tức/trò chơi giải trí.
5. **Hệ thống Bảo mật & Phân quyền (RBAC):** Quản lý quyền Admin/User, lọc nội dung và chống tấn công XSS/CSRF.