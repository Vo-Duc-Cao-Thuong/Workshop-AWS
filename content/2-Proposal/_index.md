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
- **Amazon S3:** Static web hosting for React/Vite frontend and media/embeddings storage.
- **Amazon EC2:** Virtual machine hosting the Dockerized FastAPI Backend and AI inference pipeline.
- **Amazon RDS:** Relational database for persistent storage of users, posts, music, games, and activity logs.
- **Amazon CloudWatch:** System monitoring and log collection.