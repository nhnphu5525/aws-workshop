---
title: "Sự kiện 4"
date: 2025-11-29
weight: 5
chapter: false
pre: " <b> 4.5 </b> "
---

## AWS Cloud Mastery Series #3 - Well-Architected Security Pillar

### Thông tin sự kiện

| | |
|---|---|
| **Tên sự kiện** | AWS Well-Architected Security Pillar |
| **Ngày** | Thứ Bảy, 29 tháng 11, 2025 |
| **Thời gian** | 8:30 SA – 12:00 CH |
| **Địa điểm** | Văn phòng AWS Việt Nam |
| **Chủ đề chính** | Security Pillar - IAM, Detection, Infrastructure Protection, Data Protection, Incident Response |
| **Vai trò** | Người tham dự |

---

### Tóm tắt sự kiện

Workshop nửa ngày về Security Pillar của AWS Well-Architected Framework. Các diễn giả kết nối các nguyên tắc lý thuyết với các tình huống thực tế tại doanh nghiệp Việt Nam, bao gồm năm trụ cột cốt lõi với các trình diễn thực tế.

---

### Nền tảng bảo mật

Các nguyên tắc cốt lõi được thảo luận:
- **Least Privilege**: Quyền tối thiểu cho mỗi tác vụ
- **Zero Trust**: Luôn xác minh bất kể vị trí mạng
- **Defense in Depth**: Nhiều lớp bảo mật

---

### Năm trụ cột bảo mật

#### Trụ cột 1: Identity & Access Management
Các thực hành chính được nhấn mạnh:
- Tránh credentials dài hạn - sử dụng IAM roles
- Bật MFA cho tất cả người dùng
- Sử dụng IAM Identity Center cho môi trường multi-account
- Triển khai SCPs và Permission Boundaries

#### Trụ cột 2: Detection
Các thành phần phát hiện:
- **CloudTrail**: Logging API toàn organization
- **GuardDuty**: Phát hiện mối đe dọa thông minh
- **Security Hub**: Tổng hợp security findings
- **EventBridge**: Triggers phản hồi tự động

#### Trụ cột 3: Infrastructure Protection
Kiến trúc bảo mật mạng:
- Phân đoạn VPC theo độ nhạy cảm
- Security Groups là tuyến phòng thủ chính
- AWS WAF để bảo vệ web application
- AWS Shield để bảo vệ DDoS

#### Trụ cột 4: Data Protection
Thực hành bảo mật dữ liệu:
- KMS để quản lý key với rotation tự động
- Mã hóa at rest và in transit cho tất cả services
- Secrets Manager để rotation credentials
- Phân loại dữ liệu với enforcement qua SCPs

#### Trụ cột 5: Incident Response
Framework phản hồi:
1. Chuẩn bị: Runbooks và game days
2. Phát hiện: GuardDuty và CloudTrail alerts
3. Ngăn chặn: Cô lập và bảo toàn bằng chứng
4. Loại bỏ: Xóa mối đe dọa
5. Khôi phục: Restore từ backups sạch
6. Sau sự cố: Tài liệu hóa bài học

---

### Bài học rút ra

1. **IAM là nền tảng** - Tất cả các kiểm soát khác có thể bị bypass nếu không có identity management đúng
2. **Detection cho phép response** - Logging toàn diện phải được bật và review
3. **Automation là thiết yếu** - Quy trình bảo mật thủ công không scale được
4. **Defense in depth hiệu quả** - Xếp chồng nhiều kiểm soát để dự phòng
5. **Mã hóa nên là mặc định** - Overhead của KMS là tối thiểu

**Các mục hành động từ workshop:**
- Audit IAM policies với Access Analyzer
- Bật CloudTrail cấp organization
- Triển khai phản hồi GuardDuty tự động
- Review mã hóa trên tất cả data stores
- Tạo và test incident response playbooks

---

### Thư viện ảnh sự kiện

![Khai mạc Workshop Security](https://nhnphu5525.github.io/aws-workshop/images/Event-Participated/Event-4/pic1.jpg)
*Phiên khai mạc về AWS Well-Architected Security Pillar*

![Thực hành IAM tốt nhất](https://nhnphu5525.github.io/aws-workshop/images/Event-Participated/Event-4/pic2.jpg)
*Tìm hiểu sâu về Identity and Access Management*

![Thảo luận nhóm](https://nhnphu5525.github.io/aws-workshop/images/Event-Participated/Event-4/pic3.jpg)
*Thảo luận tương tác về các thực hành bảo mật tốt nhất*

---

*Bảo mật phải là trách nhiệm chung giữa các team phát triển, vận hành và bảo mật. Well-Architected framework cung cấp ngôn ngữ chung cho các cuộc thảo luận này.*
