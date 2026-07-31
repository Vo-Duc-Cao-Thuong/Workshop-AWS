---
title : "Testing & Validation"
date : 2026-07-24
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

#### System Testing & Validation

After completing the deployment of **Frontend on S3**, **Backend Docker on EC2**, and configuring **CORS/CSP Security Headers**, perform end-to-end testing of the **Fav Web Portal** application.

---

#### 1. Test Authentication & Face ID Login

1. Access the Frontend S3 Website URL:
   `http://fav-web-frontend-bucket.s3-website-ap-southeast-2.amazonaws.com`

2. Log in using default credentials:
   - **Username**: `admin`
   - **Password**: `123456`

3. Click **"📷 Activate Face ID"**:
   - The system opens the camera and captures 5 continuous face samples.
   - Log out ➔ Test camera sign-in ➔ Successfully authenticated via facial recognition.

---

#### 2. Test Background Audio Playback & Control Modes

1. Navigate to **🎵 Music** tab ➔ Play any audio track.
2. Test player modes:
   - **🔀 Shuffle Mode:** Automatically selects a random track upon song completion.
   - **🔁 / 🔂 Repeat Mode:** Repeat single track or loop full playlist.
3. Switch to other pages (**Home**, **Feed**, **Knowledge**, **Games**...):
   - **Expected Result:** Audio continues playing seamlessly in the background without interruption.

---

#### 3. Test Post Publishing & Article Deletion

1. Click **"✏️ Post New"** ➔ Attach image/video/audio ➔ Click **Publish**.
2. Verify post appears on the **Feed**.
3. Test **`🗑️ Delete`** post button:
   - Click delete ➔ Confirm deletion ➔ Post and attached media file removed permanently from server.

---

#### 4. Test Security Headers (CORS & CSP)

Inspect HTTP Response Headers from the EC2 Backend:

```bash
curl -i http://<EC2_PUBLIC_IP>/
```

**Expected Result:**
- HTTP `200 OK`
- Response header contains `Content-Security-Policy: default-src 'self' ...`
- JSON payload: `{"message": "Backend is running"}`
