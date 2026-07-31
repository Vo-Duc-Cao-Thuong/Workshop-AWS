---
title: "Blog 1: Sau khoảng 2 tháng tìm hiểu AWS, mình hiểu EC2 như thế nào?"
date: 2026-07-24
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Sau khoảng 2 tháng tìm hiểu AWS, mình hiểu EC2 như thế nào?

> *Bài viết được chia sẻ bởi sinh viên trên cộng đồng [AWS Study Group VN](https://www.facebook.com/groups/awsstudygroupfcj).*

EC2 là một trong những service đầu tiên mình dành thời gian tìm hiểu khi bắt đầu học AWS. Bài viết này không phải là hướng dẫn sử dụng hay chia sẻ từ góc nhìn của một người có nhiều kinh nghiệm, mà chỉ là những gì mình tổng hợp và hiểu được sau khoảng 2 tháng đọc tài liệu, xem workshop và tự tìm hiểu về EC2. Hy vọng bài viết sẽ hữu ích với những bạn cũng đang bắt đầu như mình. Nếu có nội dung nào mình hiểu chưa đúng hoặc còn thiếu sót, mình rất mong nhận được góp ý từ mọi người để có thể học hỏi và hoàn thiện hơn.

---

### BẮT ĐẦU TỪ EC2

Khi mới mở AWS Console, điều đầu tiên mình cảm nhận là... khá ngợp. Có rất nhiều service với những cái tên hoàn toàn mới như EC2, S3, IAM, VPC, Lambda,... nên mình cũng không biết nên bắt đầu từ đâu.

Sau khi xem một vài workshop và đọc thêm tài liệu, mình nhận ra EC2 xuất hiện rất thường xuyên. Từ việc host website, chạy backend cho đến các bài lab cơ bản, hầu như đều có sự xuất hiện của EC2. Có lẽ vì vậy mà mình quyết định tìm hiểu service này trước.

---

### EC2 KHÔNG CHỈ LÀ MỘT "MÁY ẢO"

Lúc đầu, mình chỉ hiểu đơn giản EC2 là một máy ảo chạy trên cloud. Cách hiểu này không sai, nhưng sau khi đọc thêm thì mình thấy nó vẫn còn khá chung chung.

Theo cách mình hình dung, EC2 giống như việc AWS cho mình "thuê" một chiếc máy tính trên Internet. Điểm khác là mình có thể lựa chọn hệ điều hành, cấu hình CPU, RAM, dung lượng lưu trữ và chỉ sử dụng đúng lượng tài nguyên mình cần. Điều này giúp việc triển khai ứng dụng trở nên linh hoạt hơn mà không cần chuẩn bị một máy chủ vật lý.

Có một điều mình khá thích là AWS cho phép người dùng chủ động lựa chọn gần như mọi thứ ngay từ đầu. Ban đầu mình thấy có quá nhiều bước khi khởi tạo một EC2, nhưng sau này mới hiểu mỗi lựa chọn đều có lý do riêng.

---

### NHỮNG ĐIỀU MÌNH THẤY ĐÁNG CHÚ Ý

Trong quá trình tìm hiểu, có hai khái niệm mình dành thời gian đọc nhiều hơn một chút.

- **Instance Type:** Trước đây mình cứ nghĩ chỉ cần chọn cấu hình càng mạnh càng tốt. Nhưng tìm hiểu thêm thì mình mới biết mỗi loại instance được thiết kế cho những nhu cầu khác nhau. Nếu chỉ học tập hoặc thử nghiệm thì không nhất thiết phải chọn cấu hình cao, vừa đủ dùng cũng là một cách tiết kiệm chi phí.
- **Security Group:** Ban đầu mình chỉ xem đây là một bước cấu hình khi tạo EC2. Sau khi đọc thêm, mình mới hiểu nó đóng vai trò như một lớp kiểm soát các kết nối đến và đi từ instance. Điều này khiến mình nhận ra rằng bảo mật không phải là thứ chỉ cần quan tâm khi hệ thống đã hoạt động, mà đã được AWS đặt vào ngay từ bước khởi tạo.

---

### CÀNG TÌM HIỂU CÀNG THẤY MỌI THỨ ĐỀU LIÊN QUAN VỚI NHAU

Một điều mình không ngờ là khi tìm hiểu EC2 thì lại biết thêm khá nhiều service khác.

Đọc về quyền truy cập thì gặp **IAM**, tìm hiểu về mạng thì gặp **VPC**, còn khi muốn theo dõi tài nguyên thì lại thấy **CloudWatch**. Ban đầu mình hơi nản vì cảm giác học một service lại phải biết thêm vài service khác. Nhưng sau một thời gian, mình thấy đây cũng là điểm thú vị của AWS: các service được thiết kế để phối hợp với nhau thay vì hoạt động riêng lẻ.

Có lẽ vì vậy mà mình không còn cố gắng học thật nhiều service trong thời gian ngắn. Thay vào đó, mình chọn tìm hiểu từng service trước, hiểu được vai trò của nó rồi mới mở rộng sang những phần liên quan.

---

### MỘT VÀI SUY NGHĨ SAU 2 THÁNG

Sau khoảng 2 tháng tìm hiểu, mình vẫn xem mình là người mới với AWS và chắc chắn còn rất nhiều điều phải học. Tuy nhiên, EC2 là service giúp mình có cái nhìn rõ ràng hơn về cloud và cũng là điểm khởi đầu khá phù hợp để làm quen với hệ sinh thái AWS.

Mình nghĩ điều quan trọng nhất khi mới học không phải là cố gắng nhớ thật nhiều khái niệm, mà là hiểu được mỗi service được tạo ra để giải quyết vấn đề gì. Khi nhìn theo cách đó, việc học AWS trở nên dễ tiếp cận hơn rất nhiều.

Đó là những gì mình hiểu được về EC2 ở thời điểm hiện tại. Nếu mọi người có thêm góc nhìn hoặc kinh nghiệm về service này, mình rất mong được đọc và học hỏi thêm trong phần bình luận.

**Trong quá trình tìm hiểu, mình có tham khảo một số nguồn sau:**
* **AWS Documentation – Amazon EC2 User Guide:** https://docs.aws.amazon.com/ec2/
* **Amazon EC2 – AWS Product Overview:** https://aws.amazon.com/ec2/
* **AWS Study Group Youtube:** https://www.youtube.com/@AWSStudyGroup
