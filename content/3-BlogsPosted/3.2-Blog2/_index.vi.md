---
title: "Blog 2: Xây dựng kiến trúc Three-Tier cho Fav Web trên AWS"
date: 2026-07-24
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# Xây dựng kiến trúc Three-Tier cho Fav Web trên AWS

> *Bài viết được chia sẻ bởi tác giả trên cộng đồng [AWS Study Group VN](https://www.facebook.com/groups/awsstudygroupfcj).*

Trong quá trình thực hiện dự án **Fav Web**, nhóm mình đặt ra một câu hỏi khá đơn giản: *Làm thế nào để triển khai một ứng dụng web trên AWS vừa dễ quản lý, vừa tối ưu chi phí nhưng vẫn có khả năng mở rộng khi số lượng người dùng tăng lên?*

Trong lúc tìm hiểu, nhóm mình đã tham khảo bài viết *"Building a three-tier architecture on a budget"* trên AWS Architecture Blog. Bài viết gợi ý cách xây dựng một kiến trúc ba tầng (Three-Tier Architecture) với các dịch vụ AWS, ưu tiên tính đơn giản và khả năng mở rộng.

Từ ý tưởng đó, nhóm đã thiết kế kiến trúc riêng cho **Fav Web**, phù hợp với công nghệ và yêu cầu của dự án.

---

### KIẾN TRÚC TỔNG THỂ

Kiến trúc của Fav Web gồm ba tầng chính:
- **Presentation Layer**
- **Application Layer**
- **Data Layer**

Ngoài ra còn có các dịch vụ hỗ trợ như **IAM** và **CloudWatch** để quản lý quyền truy cập và giám sát hệ thống.

Khác với ví dụ trong AWS Architecture Blog sử dụng kiến trúc serverless (API Gateway + Lambda + DynamoDB), nhóm mình lựa chọn **EC2, Docker và RDS** vì muốn có nhiều quyền kiểm soát hơn đối với môi trường triển khai, đồng thời phù hợp với yêu cầu của một dự án thực hành.

---

### PRESENTATION LAYER - FRONTEND TRÊN AMAZON S3

Frontend của Fav Web được xây dựng bằng React.  
Sau khi build, toàn bộ file HTML, CSS và JavaScript được triển khai lên **Amazon S3 Static Website Hosting**.

**Lý do nhóm lựa chọn S3:**
- Triển khai rất nhanh
- Không cần cài đặt Web Server
- Chi phí thấp
- Dễ cập nhật phiên bản mới

Người dùng chỉ cần truy cập website, S3 sẽ trả về toàn bộ nội dung tĩnh và frontend sẽ bắt đầu gọi REST API tới backend. Đây là một trong những cách triển khai phổ biến cho các ứng dụng SPA (Single Page Application).

---

### APPLICATION LAYER - DOCKER CHẠY TRÊN AMAZON EC2

Phần Backend của Fav Web được viết bằng FastAPI và đóng gói bằng Docker.  
Container được triển khai trên một **Amazon EC2 Instance** nằm trong VPC.

**Backend chịu trách nhiệm xử lý:**
- Xác thực người dùng
- Face ID Authentication
- RBAC (Role-Based Access Control)
- Quản lý dữ liệu
- Upload và Download hình ảnh
- Cung cấp REST API cho Frontend

**Việc sử dụng Docker giúp nhóm:**
- Dễ triển khai
- Đồng nhất môi trường Development và Production
- Thuận tiện khi nâng cấp sau này sang Amazon ECS hoặc Kubernetes.

---

### DATA LAYER - AMAZON RDS POSTGRESQL

Dữ liệu của hệ thống được lưu trong **Amazon RDS PostgreSQL**.  
Backend kết nối trực tiếp tới RDS để:
- Lưu thông tin người dùng
- Lưu metadata của hình ảnh
- Lưu dữ liệu bài viết
- Quản lý phân quyền

**Thay vì tự cài PostgreSQL trên EC2, RDS giúp nhóm giảm rất nhiều công việc quản trị như:**
- Backup tự động
- Cập nhật phiên bản
- Monitoring
- Khôi phục dữ liệu

Nhờ vậy nhóm có thể tập trung nhiều hơn vào phát triển ứng dụng.

---

### AMAZON S3 - KHO LƯU TRỮ MEDIA

Một điểm mà nhóm khá hài lòng là **không lưu hình ảnh trực tiếp trên EC2**.  
Thay vào đó: `Người dùng Upload` ➔ `Backend xử lý` ➔ `IAM Role xác thực quyền` ➔ `Amazon S3 lưu Object` ➔ `Database chỉ lưu URL`.

**Thiết kế này giúp:**
- Giảm dung lượng EC2
- Dữ liệu media độc lập với application
- Dễ mở rộng khi số lượng file tăng lên

---

### IAM VÀ CLOUDWATCH

Để tăng tính bảo mật, EC2 được gán **IAM Role** thay vì sử dụng Access Key lưu trong source code. IAM chỉ cấp đúng các quyền cần thiết để backend truy cập bucket S3.

Bên cạnh đó, toàn bộ log của ứng dụng được gửi về **Amazon CloudWatch**, giúp nhóm dễ dàng theo dõi:
- API Error
- Upload Failure
- Authentication Log
- Exception

Việc có sẵn log tập trung giúp quá trình debug nhanh hơn rất nhiều.

---

### KẾT LUẬN

Dự án Fav Web là cơ hội để nhóm áp dụng những kiến thức đã học về AWS vào một hệ thống thực tế. Thông qua việc xây dựng kiến trúc ba tầng với Amazon S3, Amazon EC2, Docker, Amazon RDS, IAM và CloudWatch, nhóm không chỉ hiểu cách các dịch vụ AWS kết nối với nhau mà còn rèn luyện tư duy thiết kế hệ thống theo hướng đơn giản, dễ mở rộng và tối ưu chi phí.

Đối với nhóm mình, giá trị lớn nhất không nằm ở việc sử dụng thật nhiều dịch vụ AWS, mà là hiểu vì sao mỗi dịch vụ được lựa chọn, khi nào nên sử dụng và nó giải quyết vấn đề gì trong toàn bộ kiến trúc.

Nếu bạn cũng đang học AWS hoặc xây dựng một hệ thống theo mô hình Three-Tier Architecture, rất mong được trao đổi và học hỏi thêm từ mọi người.

---

### TÀI LIỆU THAM KHẢO

1. Nemeth, A., Vergona, F., & Sharma, V. (2024, September 25). *Building a three-tier architecture on a budget*. AWS Architecture Blog. [https://aws.amazon.com/blogs/aws-architecture/building-a-three-tier-architecture-on-a-budget/](https://aws.amazon.com/blogs/aws-architecture/building-a-three-tier-architecture-on-a-budget/)
2. Re Ferre, M. (2018, September 6). *Compute abstractions on AWS: A visual story*. AWS Architecture Blog. [https://aws.amazon.com/blogs/aws-architecture/compute-abstractions-on-aws-a-visual-story/](https://aws.amazon.com/blogs/aws-architecture/compute-abstractions-on-aws-a-visual-story/)
3. Gao, Z. (2022, August 5). *Web application access control patterns using AWS services*. AWS Architecture Blog. [https://aws.amazon.com/blogs/aws-architecture/web-application-access-control-patterns-using-aws-services/](https://aws.amazon.com/blogs/aws-architecture/web-application-access-control-patterns-using-aws-services/)
4. Beswick, J. (2023, May 3). *Patterns for building an API to upload files to Amazon S3*. AWS Compute Blog. [https://aws.amazon.com/blogs/compute/patterns-for-building-an-api-to-upload-files-to-amazon-s3/](https://aws.amazon.com/blogs/compute/patterns-for-building-an-api-to-upload-files-to-amazon-s3/)

![Architecture Diagram](/images/aws_architecture.png)
