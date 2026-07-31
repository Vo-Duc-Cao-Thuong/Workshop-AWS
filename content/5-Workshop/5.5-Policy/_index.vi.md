---
title : "Cấu hình Bảo mật, CORS & CSP Policy"
date : 2026-07-24
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

#### 1. EC2 Security Group Rules

Đảm bảo **EC2 Inbound Rules** trong AWS Management Console cho phép các cổng sau:

| Type | Protocol | Port Range | Source | Mục đích |
|------|----------|------------|--------|----------|
| HTTP | TCP | 80 | `0.0.0.0/0` | Giao tiếp Web API công khai với Frontend S3 |
| Custom TCP | TCP | 8000 | `0.0.0.0/0` | Cổng Uvicorn dev / thử nghiệm |
| SSH | TCP | 22 | `My IP` / `0.0.0.0/0` | Quản trị từ xa |

---

#### 2. Cấu hình CORS (Cross-Origin Resource Sharing)

Vì Frontend tĩnh nằm ở S3 (`http://fav-web-frontend-bucket.s3-website-ap-southeast-2.amazonaws.com`) và Backend ở EC2 (`http://52.63.251.110`), FastAPI Backend cấu hình middleware trong `backend/main.py`:

```python
DEV_ORIGINS = [
    'http://localhost:5173',
    'http://127.0.0.1:5173',
    'http://fav-web-frontend-bucket.s3-website-ap-southeast-2.amazonaws.com',
]

app.add_middleware(
    CORSMiddleware,
    allow_origins=ALLOWED_ORIGINS,
    allow_origin_regex=r"https?://.*",
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
```

---

#### 3. Cấu hình Content Security Policy (CSP) & Meta Tag

Để tránh trình duyệt chặn các yêu cầu kết nối `fetch` Cross-Origin từ S3 tới EC2, thẻ `<meta>` trong `frontend/index.html` và Middleware `backend/middleware/csp.py` được nới rộng `connect-src`:

```html
<meta http-equiv="Content-Security-Policy"
      content="default-src 'self'; img-src 'self' data: https: http:; script-src 'self' 'unsafe-inline' https://cdn.jsdelivr.net; style-src 'self' 'unsafe-inline' https://cdn.jsdelivr.net https://fonts.googleapis.com; font-src 'self' https://fonts.gstatic.com; frame-src 'self' http: https:; connect-src 'self' http: https: ws: wss:;" />
```

---

#### 4. Cơ chế Bảo mật Xác thực JWT Dual (Cookie + Bearer Token Fallback)

Do trình duyệt chặn gửi `HttpOnly Cookie` qua kết nối HTTP không mã hóa giữa 2 domain khác nhau (S3 & EC2), hệ thống áp dụng cơ chế xác thực kép:
1. **Response Login:** Server trả về Cookie `fw_auth` đồng thời trả về `token` trong JSON payload.
2. **Request Interceptor:** Axios đính kèm `Authorization: Bearer <token>` nếu phát hiện có token lưu tại `localStorage`.
