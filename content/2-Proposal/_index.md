---
title: "Proposal"
date: 2026-07-24
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Fav Web Portal
## Cloud-native Multimedia & AI Face Recognition Portal on AWS

### 1. Executive Summary
The **Fav Web Portal** project is designed to deliver a comprehensive cloud-native multi-service web portal integrated with AI-powered Face Recognition (Biometric Authentication) and scalable Cloud Infrastructure on **Amazon Web Services (AWS)**. The system merges biometric security with rich social and media services (Multimedia Feed, Streaming Music Player, Game Hub, Knowledge Base, Bookmarks, and Real-time Comments/Reactions).

### 2. Problem Statement

**Current Challenges:**
- Existing web applications often isolate entertainment/content services from modern AI biometric authentication.
- Storing rich media assets (images, audio, posts) alongside face embedding vectors requires scalable, reliable, and cost-effective cloud storage.
- Managing cross-domain authentication tokens/cookies between a static frontend (S3 Web Hosting) and an API backend (EC2) faces strict browser CORS/CSP restrictions if not properly configured.

**Proposed Solution:**
- Deploy **Amazon S3** for Static Website Hosting and object storage for user media and face vector embeddings (`.npy` files).
- Deploy **Amazon EC2** running Dockerized **FastAPI** backend integrated with Deep Learning face recognition models (`facenet-pytorch` / `insightface`).
- Utilize **Amazon RDS PostgreSQL** (or SQLite in local dev) for structured data storage.
- Implement dual authentication mechanisms (HttpOnly Cookies with Bearer Token fallback) alongside robust CORS and Content Security Policies (CSP).

---

### 3. Solution Architecture

![Fav Web Architecture](/images/aws_architecture.png)

**AWS Services Utilized:**
- **Amazon S3 (Simple Storage Service):** Static web hosting for React/Vite frontend (`fav-web-frontend-bucket`) and object storage for media & face vector embeddings (`.npy`).
- **Amazon EC2 (Elastic Compute Cloud):** Virtual machine hosting Dockerized FastAPI Backend (Web API & AI Inference Engine).
- **Amazon RDS PostgreSQL:** Relational database for persistent storage of users, posts, music, games, comments, and activity logs.
- **Amazon CloudWatch:** Application logging (`/fav-web/backend`) and system metrics monitoring (CPU Alarms).

---

### 4. Technical Implementation & Core Modules

**Key System Modules:**
1. **AI Face ID Module:** Fast biometric registration and login via webcam/camera using face feature vector extraction.
2. **Media & Feed Module:** Rich post publishing, interactive comments, emoji reactions, real-time activity feed.
3. **Knowledge & Collections Module:** Tech documentation sharing, bookmark management, custom collections.
4. **Music & Games Module:** Online music streaming player, game blog news and community hub.
5. **Security & Access Control (RBAC):** Role-based access control (Admin/User), XSS/CSRF mitigation policies.

---

### 5. Timeline & Milestones

**8-Week Development Roadmap (FCAJ Internship Program):**
* **Weeks 1 - 2 (Planning & Architecture):** System requirement analysis, cross-domain security planning, AWS architecture design (S3, EC2, RDS), Docker setup.
* **Weeks 3 - 4 (Core Services Development):** FastAPI Backend implementation (Authentication, Media Storage, Knowledge, Music/Games service) and Docker containerization.
* **Weeks 5 - 6 (AI Face ID & Frontend Integration):** React/Vite UI development, AI Face Recognition pipeline (`facenet-pytorch`/`insightface`) integration, Cookie + Bearer Token Dual Auth.
* **Week 7 (Cloud Deployment & Security Hardening):** S3 Static Web Hosting, EC2 Container deployment, RDS PostgreSQL integration, CORS Whitelist, CSP Headers, CloudWatch Logs/Alarms.
* **Week 8 (Testing, Validation & Reporting):** End-to-End testing, Workshop documentation authoring, and final internship report.

---

### 6. Budget Estimation (AWS Infrastructure Costs)

Estimated monthly operational expenses on AWS (ap-southeast-2 region):

| AWS Service | Configuration & Scale | Estimated Monthly Cost (USD) |
| --- | --- | :---: |
| **Amazon S3** | Static Web Hosting & Object Storage (~10 GB Storage, 50k requests) | $0.25 |
| **Amazon EC2** | `t2.micro` / `t3.micro` Instance (Free Tier Eligible, 750 hrs/mo) | $0.00 |
| **Amazon RDS** | `db.t3.micro` PostgreSQL Instance (Free Tier Eligible, 750 hrs/mo, 20 GB Storage) | $0.00 |
| **Data Transfer** | Outbound Data Transfer (~5 GB/month) | $0.45 |
| **Amazon CloudWatch** | Log Group `/fav-web/backend` (~1 GB Logs) & 1 Metric Alarm | $0.50 |
| **Total Estimated Cost** | **Free Tier Operation / Minimal Supplemental Cost** | **~$1.20 USD / Month** |

---

### 7. Risk Assessment & Mitigation

| Risk Scenario | Impact | Probability | Mitigation Strategy |
| --- | :---: | :---: | --- |
| **Browser HTTP Camera Restriction** | High | High | Document `chrome://flags` workaround for local testing; deploy CloudFront + ACM SSL Certificate for Production HTTPS. |
| **CORS / CSP Header Conflicts** | Medium | Medium | Configure explicit CORS Allowed Origins in FastAPI; set flexible Content Security Policy (CSP) meta tags. |
| **EC2 CPU Spikes during AI Face Inference** | Medium | Low | Set CloudWatch CPU Alarm (> 80%); implement RAM Caching for face vector embeddings (`.npy`). |
| **Session Invalidation / Cookie Drop** | Low | Low | Implement **JWT Dual Authentication**: Automatic HttpOnly Cookie with Bearer Token Header Fallback. |

---

### 8. Expected Outcomes & Project Value

* **Technical Achievements:**
  - Successfully built and deployed a 100% production-ready cloud portal on AWS infrastructure.
  - Decoupled Static Frontend (S3) and Compute Backend (EC2 Docker) for maximum performance and cost optimization.
  - Ensured enterprise-grade biometric data security and session management.

* **Long-Term Value:**
  - Complete Workshop documentation serving as a high-quality reference for future AWS learners and FCAJ interns.
  - Serverless-ready architecture easily scalable to AWS Lambda, CloudFront, and ECS Fargate.