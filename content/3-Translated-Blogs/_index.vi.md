---
title : "Translated Blogs"
date :  2025-10-03
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

## [Blog 1 - Truy cập các endpoint riêng tư của Amazon API Gateway thông qua phân phối Amazon CloudFront tùy chỉnh bằng cách sử dụng VPC Origins](./3.1-Blog-1/)
Bài viết này minh họa cách kết nối Amazon CloudFront với Private REST API trong Amazon API Gateway bằng cách sử dụng VPC Origins. Giải pháp này cho phép các tổ chức tăng cường bảo mật và hiệu năng bằng cách giữ các API ở trạng thái riêng tư trong khi vẫn truy cập được thông qua CloudFront, với các lớp bảo mật bổ sung như AWS Shield Advanced, geoblocking, và hỗ trợ TLSv1.3. Kiến trúc sử dụng Application Load Balancer nội bộ tích hợp với VPC Origins để định tuyến lưu lượng đến Private REST API thông qua VPC endpoint của execute-api.

## [Blog 2 - Tính nhất quán dữ liệu với AWS DMS Data Resync](./3.2-Blog-2/)
Bài viết này đi sâu vào AWS DMS Data Resync — một tính năng được giới thiệu trong phiên bản DMS 3.6.1 để tự động phát hiện và khắc phục sự không nhất quán dữ liệu trong quá trình migration. Data Resync hoạt động bằng cách đọc các sai lệch được xác định bởi DMS data validation, truy xuất giá trị hiện tại từ source và áp dụng lên target. Bài viết thảo luận về các bước cấu hình và trình bày các trường hợp sử dụng bao gồm khôi phục các bản ghi bị xóa nhầm và tiếp tục task CDC sau khi xảy ra lỗi trên bảng.

## [Blog 3 - Tăng tốc quá trình phát triển serverless cục bộ với console đến IDE và remote debugging cho AWS Lambda](./3.3-Blog-3/)
Bài viết này đề cập đến các cải tiến gần đây nhằm nâng cao trải nghiệm phát triển cục bộ cho AWS Lambda. Hai tính năng mới của Lambda — console to IDE và remote debugging — giúp thu hẹp khoảng cách giữa phát triển trên đám mây và phát triển cục bộ. Console to IDE cho phép chuyển đổi liền mạch từ chu trình code/test trên cloud sang môi trường cục bộ chỉ với một cú nhấp chuột, trong khi remote debugging cho phép các developer gỡ lỗi các function đang chạy trên cloud trực tiếp từ VS Code IDE cục bộ bằng AWS Toolkit.
