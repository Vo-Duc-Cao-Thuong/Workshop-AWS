---
title: "Workshop"
date: 2026-07-24
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Xây dựng & Triển khai Fav Web Portal trên AWS

#### Tổng quan

Trong chuỗi bài hướng dẫn thực hành (Workshop) này, bạn sẽ từng bước xây dựng và triển khai hoàn chỉnh ứng dụng **Fav Web Portal** (Hệ thống Cổng thông tin đa phương tiện tích hợp AI Nhận diện khuôn mặt Face ID) lên hạ tầng điện toán đám mây **Amazon Web Services (AWS)**.

Hệ thống kết hợp các dịch vụ đám mây cốt lõi của AWS bao gồm **Amazon S3** (Static Web Hosting & Object Storage), **Amazon EC2** (Containerized FastAPI Backend), **Amazon RDS** (Relational Database) cùng các kỹ thuật bảo mật hiện đại (CORS, CSP, JWT Bearer Fallback).

#### Nội dung thực hành:

1. [Tổng quan về workshop & Kiến trúc AWS](5.1-Workshop-overview/)
2. [Chuẩn bị môi trường & Công cụ](5.2-Prerequiste/)
3. [Triển khai Frontend React/Vite trên Amazon S3](5.3-S3-vpc/)
4. [Triển khai Backend FastAPI Docker trên Amazon EC2](5.4-S3-onprem/)
5. [Cấu hình Bảo mật, IAM Policy, CORS & CSP Header](5.5-Policy/)
6. [Kiểm thử & Kiểm tra kết quả (Test & Validation)](5.6-Test/)
7. [Dọn dẹp tài nguyên AWS](5.7-Cleanup/)