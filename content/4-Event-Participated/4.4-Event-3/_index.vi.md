---
title: "Sự kiện 3"
date: 2025-11-17
weight: 4
chapter: false
pre: " <b> 4.4 </b> "
---

## AWS Cloud Mastery Series #2 - DevOps on AWS

### Thông tin sự kiện

| | |
|---|---|
| **Tên sự kiện** | AWS Cloud Mastery Series #2 - DevOps on AWS |
| **Ngày** | Thứ Hai, 17 tháng 11, 2025 |
| **Thời gian** | 8:30 SA – 5:00 CH |
| **Địa điểm** | AWS Event Center |
| **Chủ đề chính** | CI/CD pipelines, Infrastructure as Code, Container services, và Observability |
| **Vai trò** | Người tham dự |

---

### Tóm tắt sự kiện

Workshop cả ngày khám phá các thực hành và công cụ DevOps trên AWS. Phiên bao gồm toàn bộ vòng đời DevOps từ source control đến deployment và monitoring, với các trình diễn thực hành và case studies thực tế.

---

### Phiên buổi sáng: CI/CD & Infrastructure as Code

#### Các thành phần CI/CD Pipeline
Workshop bao gồm các dịch vụ CI/CD cốt lõi của AWS:
- **CodeCommit**: Hosting Git repository với tích hợp AWS
- **CodeBuild**: Dịch vụ build được quản lý với hỗ trợ container
- **CodeDeploy**: Deployment tự động với nhiều chiến lược
- **CodePipeline**: Điều phối toàn bộ workflow

#### Chiến lược Deployment
Ba phương pháp deployment được so sánh:
- **Blue/Green**: Chuyển đổi tức thì với khả năng rollback
- **Canary**: Chuyển traffic dần dần để giảm rủi ro
- **Rolling**: Cập nhật instance tuần tự

#### Infrastructure as Code
Các công cụ IaC được thảo luận:
- **CloudFormation**: Templates khai báo YAML/JSON
- **AWS CDK**: Ngôn ngữ lập trình (TypeScript, Python, Java)
- **Terraform**: Quản lý infrastructure đa cloud

---

### Phiên buổi chiều: Containers & Observability

#### Container Services
Các tùy chọn container của AWS:
- **ECS**: Điều phối native AWS cho hầu hết use cases
- **EKS**: Kubernetes cho yêu cầu đa cloud phức tạp
- **App Runner**: Deployment đơn giản hóa cho web apps

#### Monitoring & Observability
Stack observability được bao gồm:
- **CloudWatch**: Metrics, logs, alarms, và dashboards
- **X-Ray**: Distributed tracing cho microservices
- **Service Map**: Biểu diễn trực quan dependencies giữa các services

---

### Bài học rút ra

**Infrastructure & Deployment:**
- CDK cung cấp trải nghiệm developer tốt hơn so với CloudFormation thuần
- Blue/Green deployments cho zero-downtime releases
- Bắt đầu với ECS trừ khi có yêu cầu Kubernetes cụ thể

**Observability:**
- CloudWatch cho monitoring nền tảng
- X-Ray cần thiết cho troubleshooting microservices
- Xây dựng observability từ đầu

**Kết quả Case Study:**
- Startup đạt được cải thiện 3x về tần suất deployment
- Enterprise giảm 70% time-to-market
- Cả hai đều nhấn mạnh automation và thay đổi văn hóa

---

### Thư viện ảnh sự kiện

![Khai mạc Workshop DevOps](/images/Event-Participated/Event-3/pic1.jpg)
*Phiên khai mạc AWS Cloud Mastery Series #2*

![Demo CI/CD Pipeline](/images/Event-Participated/Event-3/pic2.jpg)
*Trình diễn trực tiếp thiết lập CI/CD pipeline*

![Workshop Container](/images/Event-Participated/Event-3/pic3.jpg)
*Phiên thực hành về container services*

---

*Workshop này củng cố rằng thành công DevOps đòi hỏi kết hợp các công cụ phù hợp với chuyển đổi văn hóa và quy trình cải tiến liên tục.*
