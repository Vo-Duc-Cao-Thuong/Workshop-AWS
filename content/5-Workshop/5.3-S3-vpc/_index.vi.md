---
title : "Triển khai Frontend trên Amazon S3"
date : 2026-07-24
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

#### Bước 1: Tạo Amazon S3 Bucket cho Static Web Hosting

1. Mở **AWS Management Console** ➔ Truy cập dịch vụ **Amazon S3**.
2. Nhấn **Create bucket**.
   - **Bucket name:** `fav-web-frontend-bucket` (hoặc tên duy nhất bất kỳ).
   - **AWS Region:** Chọn `ap-southeast-2` (Sydney) hoặc khu vực mong muốn.
   - **Object Ownership:** ACLs disabled (recommended).
3. Tại phần **Block Public Access settings for this bucket**:
   - Bỏ chọn **Block *all* public access** để cho phép công khai trang web tĩnh.
   - Đánh dấu xác nhận cảnh báo.
4. Nhấn **Create bucket**.

#### Bước 2: Bật Static Website Hosting trên S3 Bucket

1. Chọn bucket vừa tạo ➔ Chuyển sang tab **Properties**.
2. Cuộn xuống cuối trang đến mục **Static website hosting** ➔ Nhấn **Edit**.
   - Chọn **Enable**.
   - Hosting type: **Host a static website**.
   - **Index document:** `index.html`.
   - **Error document:** `index.html`.
3. Nhấn **Save changes**.

#### Bước 3: Build Frontend với IP Backend EC2

Ở máy local, mở PowerShell trong thư mục `frontend/`:

```powershell
cd d:\file_hoc_tap\Fav_Web\frontend

# Thiết lập biến VITE_API_URL trỏ tới IP Public EC2 của bạn
$env:VITE_API_URL="http://52.63.251.110/api/v1"

# Tiến hành Build sản phẩm tối ưu
npm run build
```

Sau khi build thành công, thư mục `frontend/dist/` sẽ chứa các file `index.html`, `assets/*.js`, `assets/*.css`.

#### Bước 4: Upload toàn bộ nội dung trong `frontend/dist/` lên S3

1. Trong S3 Bucket `fav-web-frontend-bucket`, chuyển sang tab **Objects**.
2. Nhấn **Upload** ➔ Kéo thả toàn bộ nội dung (file & folder) bên trong thư mục `frontend/dist/`.
3. Nhấn **Upload** để hoàn tất.

Trang web tĩnh của bạn giờ đây đã sẵn sàng tại URL Static Website của S3!