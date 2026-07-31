---
title: "Blog 3: Bắt đầu với AWS: Làm quen với Amazon S3"
date: 2026-07-24
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# Bắt đầu với AWS: Làm quen với Amazon S3

> _Bài viết được chia sẻ bởi tác giả trên cộng đồng [AWS Study Group VN](https://www.facebook.com/groups/awsstudygroupfcj)._

Khi mới tìm hiểu AWS, một trong những dịch vụ đầu tiên mình gặp là Amazon S3. Ban đầu mình chỉ hiểu đơn giản S3 là nơi để lưu file trên Cloud. Tuy nhiên, sau khi tìm hiểu thêm, mình nhận ra S3 không chỉ là một nơi lưu trữ dữ liệu, mà còn là một phần quan trọng trong nhiều hệ thống được xây dựng trên AWS.

Trong bài viết này, mình chia sẻ những gì mình tìm hiểu được về Amazon S3 dưới góc nhìn của một người mới bắt đầu làm quen với AWS. Nếu có nội dung nào mình hiểu chưa đúng hoặc còn thiếu sót, mình rất mong nhận được góp ý từ mọi người.

### AMAZON S3 LÀ GÌ?

Amazon S3 (Simple Storage Service) là một dịch vụ lưu trữ dữ liệu dạng object trên AWS.
Nếu như trong máy tính cá nhân, mình thường lưu file trong các thư mục thì S3 có một cách tổ chức khác. Dữ liệu được lưu dưới dạng object và được quản lý trong các bucket.

Có thể hình dung:

- Bucket giống như một nơi chứa dữ liệu.
- Object là các file được lưu bên trong bucket.

Ví dụ, một website bán hàng có thể sử dụng S3 để lưu:

- Hình ảnh sản phẩm.
- Video.
- File tài liệu.
- File người dùng tải lên.

Điểm khác biệt là thay vì phải tự quản lý ổ cứng hoặc server lưu trữ, AWS sẽ đảm nhiệm phần hạ tầng phía dưới.

### VÌ SAO KHÔNG LƯU TẤT CẢ DỮ LIỆU TRÊN SERVER?

Trước khi tìm hiểu Cloud, mình thường nghĩ rằng một website có thể lưu mọi thứ trên cùng một server:

- Code chạy trên server.
- Database trên server.
- Hình ảnh cũng lưu trên server.

Tuy nhiên, khi tìm hiểu cách các hệ thống thực tế được xây dựng, mình nhận ra việc tách riêng từng phần sẽ có nhiều lợi ích hơn.
Ví dụ:

- Backend tập trung xử lý logic.
- Database tập trung lưu dữ liệu có cấu trúc.
- S3 đảm nhiệm việc lưu trữ file.

Cách tiếp cận này giúp hệ thống dễ quản lý hơn và phù hợp khi cần mở rộng.

### MỘT VÀI KHÁI NIỆM CƠ BẢN TRONG S3

Bucket
Bucket là nơi chứa các object trên S3.
Khi sử dụng S3, bước đầu tiên thường là tạo một bucket để lưu trữ dữ liệu.
Một bucket có thể chứa nhiều loại dữ liệu khác nhau, nhưng trong thực tế người dùng thường tổ chức bucket theo mục đích.
Ví dụ:

- Bucket lưu ảnh website.
- Bucket lưu file backup.
- Bucket lưu dữ liệu phục vụ ứng dụng.

### Object

Object là đơn vị dữ liệu được lưu trong S3.
Một object bao gồm:

- Nội dung file.
- Metadata mô tả thông tin của file.
- Key dùng để xác định vị trí của object trong bucket.

Ví dụ, một hình ảnh có thể được lưu với đường dẫn:
images/product01.png
S3 sẽ sử dụng key này để quản lý object thay vì cấu trúc thư mục vật lý như trên máy tính.

### S3 VÀ VẤN ĐỀ QUYỀN TRUY CẬP

Một phần mình thấy quan trọng khi tìm hiểu S3 là vấn đề bảo mật.
Ban đầu mình nghĩ việc lưu file lên Cloud chỉ cần quan tâm đến dung lượng và tốc độ. Nhưng thực tế, việc kiểm soát ai có thể truy cập dữ liệu cũng rất quan trọng.
AWS cung cấp các cơ chế như:

- IAM để quản lý quyền của người dùng và service.
- Bucket Policy để kiểm soát quyền truy cập vào bucket.
- Access Control để quản lý quyền đối với object.

Ví dụ:
Một website có thể cho phép mọi người xem hình ảnh sản phẩm, nhưng không nên để file dữ liệu cá nhân của người dùng bị truy cập công khai.
Qua việc tìm hiểu S3, mình nhận ra việc lưu trữ dữ liệu luôn đi kèm với việc quản lý quyền truy cập.

### S3 KHÔNG CHỈ DÙNG ĐỂ LƯU FILE

Lúc đầu mình nghĩ S3 chỉ phù hợp để lưu hình ảnh hoặc tài liệu.
Nhưng khi tìm hiểu thêm, mình nhận ra S3 còn được sử dụng trong nhiều trường hợp khác:

- Lưu trữ dữ liệu backup.
- Lưu log của hệ thống.
- Lưu dữ liệu phục vụ phân tích.
- Lưu file cho các ứng dụng web/mobile.

Một điểm mình thấy hay là S3 có thể kết hợp với nhiều dịch vụ khác trong AWS.
Ví dụ:

- Ứng dụng sử dụng S3 để lưu file.
- Lambda xử lý dữ liệu khi có file mới được tải lên.
- CloudFront phân phối nội dung nhanh hơn đến người dùng.

### MỘT VÀI ĐIỀU MÌNH NHẬN RA KHI TÌM HIỂU S3

Điều mình thấy thú vị nhất ở S3 là AWS không chỉ cung cấp một nơi để lưu dữ liệu, mà còn cung cấp cách để quản lý dữ liệu đó một cách linh hoạt.
Ban đầu mình tiếp cận S3 như một "ổ cứng trên Cloud". Nhưng sau khi tìm hiểu thêm, mình hiểu rằng S3 là một thành phần có thể đóng vai trò quan trọng trong kiến trúc của nhiều ứng dụng.
Với người mới bắt đầu tìm hiểu AWS, mình nghĩ S3 là một service khá phù hợp để làm quen vì nó giúp hiểu được một trong những ý tưởng quan trọng của Cloud: tách việc lưu trữ dữ liệu khỏi việc xử lý ứng dụng.

### KẾT LẠI

Hiện tại mình vẫn đang trong quá trình tìm hiểu AWS và Amazon S3 chỉ là một trong những dịch vụ đầu tiên mình tiếp cận.
Qua việc tìm hiểu S3, mình không chỉ biết thêm về một dịch vụ lưu trữ, mà còn hiểu hơn về cách các hệ thống Cloud được thiết kế: mỗi thành phần có một nhiệm vụ riêng và có thể kết hợp với nhau để tạo thành một hệ thống hoàn chỉnh.
Đây là những gì mình tìm hiểu được về Amazon S3 ở thời điểm hiện tại. Nếu có phần nào chưa chính xác hoặc có thêm kinh nghiệm thực tế, mình rất mong nhận được chia sẻ từ mọi người.

### 📚 NGUỒN THAM KHẢO

- Amazon S3 Documentation:
  https://docs.aws.amazon.com/s3/

- Amazon S3 Overview:
  https://aws.amazon.com/s3/
