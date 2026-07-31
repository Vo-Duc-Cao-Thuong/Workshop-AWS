---
title : "Prerequisites"
date : 2026-07-24
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

#### Required Tools & Environment Setup

To complete this hands-on workshop deploying **Fav Web Portal** to AWS, prepare the following requirements:

1. **AWS Account:**
   - Active AWS Account with AdministratorAccess permissions.
   - Access to services: Amazon S3, Amazon EC2, AWS IAM, Amazon CloudWatch.

2. **Local Development Environment:**
   - **Git CLI:** Installed (`git --version`).
   - **Node.js & npm:** Version 18.x or higher (`node -v` & `npm -v`).
   - **Python:** Version 3.10 or higher (`python --version`).
   - **SSH Client:** PowerShell or OpenSSH Terminal.

3. **AWS EC2 Key Pair:**
   - Created **EC2 Key Pair** (`.pem` file, e.g. `ec2_key.pem`) for SSH authentication.
   - Operating System: **Ubuntu 22.04 LTS / Ubuntu 24.04 LTS**.

4. **Clone Project Repository:**
   ```bash
   git clone https://github.com/RuMeoDiNhau/Favourite-Web.git
   cd Favourite-Web
   ```