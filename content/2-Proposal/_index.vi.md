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

---

### 5. Lộ trình triển khai & Các mốc thời gian (Timeline & Milestones)

**Lộ trình 8 tuần thực tập (FCAJ Internship Program):**
* **Tuần 1 - 2 (Lập kế hoạch & Thiết kế):** Nghiên cứu yêu cầu hệ thống, phân tích bài toán bảo mật cross-domain, thiết kế sơ đồ kiến trúc AWS (S3, EC2, RDS) và chuẩn bị môi trường Docker.
* **Tuần 3 - 4 (Phát triển Core Services):** Xây dựng Backend FastAPI (Authentication, Media Storage, Knowledge, Music/Games service) và đóng gói Docker Container.
* **Tuần 5 - 6 (Tích hợp AI Face ID & Frontend):** Xây dựng giao diện React/Vite, tích hợp module AI Face Recognition (`facenet-pytorch`/`insightface`), hệ thống Cookie + Bearer Token Dual Auth.
* **Tuần 7 (Triển khai Cloud & Tối ưu bảo mật):** Triển khai S3 Static Web Hosting, cấu hình EC2 Container, kết nối RDS PostgreSQL, cài đặt CORS Whitelist, CSP Headers và CloudWatch Logs/Alarms.
* **Tuần 8 (Kiểm thử, Đánh giá & Báo cáo):** Tiến hành kiểm thử E2E (End-to-End Test), viết tài liệu Workshop và chuẩn bị báo cáo tổng kết thực tập.

---

### 6. Dự toán chi phí hạ tầng AWS (Budget Estimation)

Dưới đây là bảng dự toán chi phí ước tính hàng tháng cho hệ thống **Fav Web Portal** (Áp dụng mức giá AWS Region ap-southeast-2):

| Dịch vụ AWS | Cấu hình & Quy mô sử dụng | Chi phí ước tính / Tháng (USD) |
| --- | --- | :---: |
| **Amazon S3** | Static Website Hosting & Storage (~10 GB Storage, 50,000 PUT/GET Requests) | $0.25 |
| **Amazon EC2** | `t2.micro` / `t3.micro` Instance (Free Tier Eligible, 750 giờ/tháng) | $0.00 |
| **Amazon RDS** | `db.t3.micro` PostgreSQL Instance (Free Tier Eligible, 750 giờ/tháng, 20 GB Storage) | $0.00 |
| **Data Transfer** | Outbound Data Transfer (~5 GB/tháng) | $0.45 |
| **Amazon CloudWatch** | Log Group `/fav-web/backend` (~1 GB Logs) & 1 Metric Alarm | $0.50 |
| **Tổng chi phí ước tính** | **Hệ thống vận hành trong gói Free Tier / Chi phí phát sinh tối thiểu** | **~$1.20 USD / Tháng** |

---

### 7. Đánh giá rủi ro & Phương án dự phòng (Risk Assessment & Mitigation)

| Ma trận Rủi ro | Mức độ ảnh hưởng | Xác suất | Phương án khắc phục (Mitigation Strategy) |
| --- | :---: | :---: | --- |
| **Lỗi trình duyệt chặn Camera trên HTTP** | Cao | Cao | Hướng dẫn mở flag `chrome://flags` cho thử nghiệm local, triển khai CloudFront + ACM SSL Certificate cho HTTPS trên Production. |
| **Xung đột CORS / CSP Meta Tag** | Trung bình | Trung bình | Thiết lập CORS Origins Whitelist rõ ràng trên FastAPI và cấu hình Content Security Policy (CSP) linh hoạt cho phép nhúng nguồn S3/CloudWatch. |
| **Tải trọng CPU EC2 tăng đột biến khi AI nhận diện khuôn mặt** | Trung bình | Thấp | Cấu hình CloudWatch CPU Alarm cảnh báo khi CPU > 80%, tối ưu hóa bộ nhớ tạm RAM Caching cho vector đặc trưng khuôn mặt (`.npy`). |
| **Trôi Token / Mất phiên đăng nhập** | Thấp | Thấp | Áp dụng cơ chế **JWT Dual Authentication**: Tự động dùng HttpOnly Cookie an toàn chống XSS, tích hợp Bearer Token Header Fallback cho thiết bị di động. |

---

### 8. Kết quả kỳ vọng & Giá trị dự án (Expected Outcomes)

* **Về mặt kỹ thuật:**
  - Xây dựng thành công Cổng thông tin & Giải trí đa phương tiện hoạt động thực tế 100% trên hạ tầng điện toán đám mây AWS.
  - Phân tách kiến trúc Frontend tĩnh (S3) và Backend tính toán (EC2 Docker) giúp tối ưu hóa hiệu năng, giảm chi phí vận hành đến mức tối đa.
  - Đảm bảo an toàn bảo mật dữ liệu sinh trắc học và quản lý phiên làm việc người dùng tiêu chuẩn.

* **Giá trị thực tiễn & Lâu dài:**
  - Bộ tài liệu Workshop hoàn chỉnh là nguồn tài nguyên tham khảo chất lượng cho cộng đồng học tập AWS và sinh viên các khóa sau trong chương trình **First Cloud AI Journey (FCAJ)**.
  - Nền tảng dễ dàng mở rộng lên mô hình Serverless (AWS Lambda, CloudFront, ECS Fargate) khi lưu lượng người dùng tăng trưởng mạnh.