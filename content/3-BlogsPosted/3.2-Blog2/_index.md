---
title: "Blog 2: Building a Three-Tier Architecture for Fav Web on AWS"
date: 2026-07-24
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# Building a Three-Tier Architecture for Fav Web on AWS

> *Article published on the [AWS Study Group VN](https://www.facebook.com/groups/awsstudygroupfcj) community.*

During the development of the **Fav Web** project, our team asked a simple question: *How can we deploy a web application on AWS that is easy to manage, cost-optimized, and scalable as user traffic grows?*

While researching, we referenced the article *"Building a three-tier architecture on a budget"* on the AWS Architecture Blog. It suggested building a Three-Tier Architecture with AWS services prioritizing simplicity and scalability.

Based on that concept, our team designed a custom architecture for **Fav Web**, tailored to our tech stack and project requirements.

---

### OVERALL ARCHITECTURE

The Fav Web architecture consists of three core layers:
- **Presentation Layer**
- **Application Layer**
- **Data Layer**

Additionally, supporting services such as **IAM** and **CloudWatch** manage access permissions and system monitoring.

Unlike the serverless example in the AWS Architecture Blog (API Gateway + Lambda + DynamoDB), we selected **EC2, Docker, and RDS** to maintain full control over the deployment environment while matching our hands-on project scope.

---

### PRESENTATION LAYER - FRONTEND ON AMAZON S3

Fav Web's Frontend is built with React.  
After compilation, all static HTML, CSS, and JS files are deployed to **Amazon S3 Static Website Hosting**.

**Why we chose S3:**
- Rapid deployment
- No web server setup required
- Low cost
- Easy version updates

When users visit the website, S3 serves the static assets, and the frontend communicates via REST APIs to the backend.

---

### APPLICATION LAYER - DOCKER ON AMAZON EC2

Fav Web's Backend is written in FastAPI and containerized with Docker.  
The container is deployed on an **Amazon EC2 Instance** inside a VPC.

**Backend responsibilities:**
- User authentication & Face ID
- RBAC (Role-Based Access Control)
- Media upload/download handling
- REST API endpoints for Frontend

**Benefits of Docker:**
- Streamlined deployment
- Identical Development and Production environments
- Seamless future upgrades to Amazon ECS or Kubernetes.

---

### DATA LAYER - AMAZON RDS POSTGRESQL

Application data is stored in **Amazon RDS PostgreSQL**.  
The backend connects directly to RDS for:
- User credentials & profile data
- Media metadata & post content
- Role-based permissions

**Using RDS instead of self-managed PostgreSQL on EC2 reduces operational overhead:**
- Automated backups & version upgrades
- Integrated monitoring & point-in-time recovery

---

### AMAZON S3 - MEDIA STORAGE

Our architecture avoids storing user images on the EC2 instance filesystem.  
Workflow: `User Upload` ➔ `Backend Processing` ➔ `IAM Role Verification` ➔ `S3 Object Store` ➔ `Database URL Storage`.

---

### IAM AND CLOUDWATCH

EC2 instances use **IAM Roles** instead of hardcoded Access Keys. Application logs (API Errors, Auth Logs, Exceptions) stream directly to **Amazon CloudWatch** for centralized debugging.

---

### CONCLUSION & REFERENCES

1. Nemeth, A., et al. (2024). *Building a three-tier architecture on a budget*. AWS Architecture Blog.
2. Re Ferre, M. (2018). *Compute abstractions on AWS*. AWS Architecture Blog.
3. Gao, Z. (2022). *Web application access control patterns*. AWS Architecture Blog.

![Architecture Diagram](/images/aws_architecture.png)
