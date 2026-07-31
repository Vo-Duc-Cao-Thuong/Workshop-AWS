---
title : "Workshop Overview & Architecture"
date : 2026-07-24
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

#### Introduction to Fav Web Portal

**Fav Web Portal** is a multi-service web application designed with modern architecture, integrating AI Biometric Authentication (Face ID) with rich multimedia content services.

Key Capabilities:
- **High Availability & Cost Efficiency:** Decouples static frontend (Amazon S3 Static Website Hosting) from compute backend (Amazon EC2 Docker Container).
- **Security:** Dual authentication model (biometrics + JWT cookie/Bearer token header fallback), adhering strictly to CORS and Content Security Policy (CSP).
- **Scalable Storage:** Utilizes Amazon S3 for media assets and facial embedding vector `.npy` files.

#### Production Application Interface (Fav Web Portal)

![Fav Web Portal Dashboard](/images/dashboard.png)

#### AWS Deployment Architecture Overview

![Architecture](/images/aws_architecture.png)

1. **Client (Browser):** Users access the portal via Amazon S3 Static Web Hosting URL (`fav-web-frontend-bucket`).
2. **Frontend Layer (AWS S3 Static Web):** Serves optimized React/Vite web assets interacting with EC2 backend API endpoints.
3. **Backend Layer (AWS EC2 Instance):** Runs a Docker container with FastAPI + Uvicorn server + Deep Learning Face Recognition models (`facenet-pytorch`/`insightface`).
4. **Database & Storage Layer (AWS RDS / S3):** Manages relational data (users, posts, music, games, logs) alongside Amazon S3 object storage for media files and embeddings.