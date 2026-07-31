---
title : "Security, CORS & CSP Policy Configuration"
date : 2026-07-24
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

#### 1. EC2 Security Group Rules

Ensure **EC2 Inbound Rules** in the AWS Console permit the following traffic:

| Type | Protocol | Port Range | Source | Purpose |
|------|----------|------------|--------|---------|
| HTTP | TCP | 80 | `0.0.0.0/0` | Public Web API traffic from S3 Frontend |
| Custom TCP | TCP | 8000 | `0.0.0.0/0` | Uvicorn development port |
| SSH | TCP | 22 | `My IP` / `0.0.0.0/0` | Remote administration |

---

#### 2. CORS (Cross-Origin Resource Sharing) Setup

Because the S3 static frontend (`http://fav-web-frontend-bucket.s3-website-ap-southeast-2.amazonaws.com`) and EC2 backend (`http://52.63.251.110`) reside on separate origins, FastAPI configures middleware in `backend/main.py`:

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

#### 3. Content Security Policy (CSP) Configuration

To prevent browsers from blocking cross-origin API calls, `frontend/index.html` and `backend/middleware/csp.py` configure permissive `connect-src` directives:

```html
<meta http-equiv="Content-Security-Policy"
      content="default-src 'self'; img-src 'self' data: https: http:; script-src 'self' 'unsafe-inline' https://cdn.jsdelivr.net; style-src 'self' 'unsafe-inline' https://cdn.jsdelivr.net https://fonts.googleapis.com; font-src 'self' https://fonts.gstatic.com; frame-src 'self' http: https:; connect-src 'self' http: https: ws: wss:;" />
```

---

#### 4. Dual JWT Authentication Mechanism (Cookie + Bearer Token Fallback)

To bypass modern browser restrictions against cross-origin unencrypted HTTP cookies, the authentication pipeline implements dual delivery:
1. **Login Response:** Returns the `fw_auth` cookie and includes a `token` inside the JSON response payload.
2. **Request Interceptor:** Axios automatically attaches `Authorization: Bearer <token>` for all outgoing API calls.
