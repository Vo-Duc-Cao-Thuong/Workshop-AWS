---
title : "Kiểm thử & Kiểm tra kết quả"
date : 2026-07-24
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

#### Kiểm thử & Xác thực hệ thống (Test & Validation)

Sau khi hoàn tất triển khai **Frontend trên S3**, **Backend Docker trên EC2** và cấu hình **Bảo mật CORS/CSP Policy**, tiến hành kiểm thử toàn bộ tính năng end-to-end của hệ thống **Fav Web Portal**.

---

#### 1. Kiểm thử Đăng nhập & Xác thực Face ID

1. Truy cập vào đường dẫn Website S3 của Frontend:
   `http://fav-web-frontend-bucket.s3-website-ap-southeast-2.amazonaws.com`

2. Đăng nhập bằng tài khoản mặc định:
   - **Username**: `admin`
   - **Password**: `123456`

3. Bấm **"📷 Kích hoạt Face ID ngay"**:
   - Hệ thống mở Camera ➔ Quét 5 ảnh khuôn mặt liên tiếp để đăng ký mẫu khuôn mặt.
   - Đăng xuất ➔ Thử đăng nhập lại bằng Camera ➔ Đăng nhập thành công vào hệ thống.

---

#### 2. Kiểm thử Trình phát nhạc ngầm liên tục (Background Audio Playback)

1. Vào tab **🎵 Âm nhạc** ➔ Bấm phát một bài hát bất kỳ.
2. Thử nghiệm các tính năng điều khiển:
   - **🔀 Phát ngẫu nhiên (Shuffle):** Tự động chọn ngẫu nhiên bài tiếp theo khi kết thúc bài hát.
   - **🔁 / 🔂 Chế độ Lặp (Repeat):** Lặp lại 1 bài hát duy nhất hoặc lặp lại toàn bộ danh sách phát.
3. Chuyển sang các mục khác (**Trang chủ**, **Bảng tin**, **Kiến thức**, **Trò chơi**...):
   - **Kết quả mong đợi:** Âm thanh tiếp tục phát mượt mà ngầm trong nền không bị gián đoạn hay ngắt bài.

---

#### 3. Kiểm thử Đăng bài & Quản lý xóa bài viết

1. Bấm **"✏️ Đăng bài mới"** ➔ Chọn tệp đính kèm (Ảnh/Video/Audio) ➔ Bấm **Đăng bài**.
2. Kiểm tra bài viết xuất hiện ngay trên **Bảng tin (Feed)**.
3. Thử nghiệm nút **`🗑️ Xóa`** bài viết:
   - Bấm nút xóa ➔ Xác nhận xóa ➔ Bài đăng và tệp media đính kèm bị gỡ vĩnh viễn khỏi server.

---

#### 4. Kiểm thử Bảo mật Header (CORS & CSP Header)

Mở terminal kiểm tra HTTP Response Header từ EC2 Backend:

```bash
curl -i http://<EC2_PUBLIC_IP>/
```

**Kết quả mong đợi:**
- Trả về HTTP `200 OK`
- Phản hồi chứa Header `Content-Security-Policy: default-src 'self' ...`
- Trả về JSON: `{"message": "Backend is running"}`
