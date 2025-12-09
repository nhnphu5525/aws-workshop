---
title : "Nhật ký tuần 1"
date :  2025-09-10 
weight : 1 
chapter : false
pre : " <b> 1.1 </b> "
---
### Mục tiêu tuần 1:
- **Thiết lập tài khoản AWS** và khám phá các dịch vụ cơ bản
- **Hoàn tất Module 01-02**: Leadership Principles, Global Infrastructure, Management Tools
- **Quản lý ngân sách AWS**: AWS Budgets, Cost Optimization, Support Plans
- **Nghiên cứu VPC & Networking**: VPC, Subnet, Security Groups, Load Balancers
- **Buổi thực hành**: Xây dựng VPC, EC2, NAT Gateway, VPC Peering
- **Học tập mở rộng**: Well Architecture Framework, Advanced Networking

### Lịch trình công việc trong tuần

| Thứ | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|---|---|---|---|---|
| 2 | - Gặp gỡ các thành viên FCJ<br>- Xem xét các quy định và hướng dẫn thực tập | 08/09/2025 | 08/09/2025 |  |
| 3 | - Đăng ký tài khoản AWS<br>- Nghiên cứu dịch vụ AWS:<br>&emsp; + Tìm hiểu MFA, nhóm IAM, người dùng IAM<br>&emsp; + Xem và cập nhật thông tin tài khoản<br>&emsp; + Tạo bí danh tài khoản cho người dùng IAM<br>- Thực hành vẽ sơ đồ kiến trúc trên [draw.io](https://draw.io)<br>- Khái niệm điện toán đám mây (định nghĩa, ưu điểm)<br>- Tìm hiểu Access Key<br>- Hoàn tất module 01-02<br>&emsp; + Leadership Principles<br>&emsp; + AZ - Khái niệm Availability Zone<br>&emsp; + Kiến thức cơ bản về Region<br>&emsp; + Tổng quan Edge location<br>&emsp; &emsp; * CloudFront (CDN)<br>&emsp; &emsp; * Web Application Firewall (WAF)<br>&emsp; &emsp; * Route 53 (DNS Service)<br>&emsp; + AWS Management Console (Service Search, Support Center, CLI)<br>&emsp; + Quản lý và tối ưu chi phí AWS<br>&emsp; + Sử dụng AWS Support<br>- Hoàn thành tất cả bài lab module 01<br>- Nghiên cứu mở rộng về Well-Architected Framework | 09/09/2025 | 09/09/2025 | [FCJ Study Web](https://cloudjourney.awsstudygroup.com)<br>[Youtube First Cloud Journey](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=1) |
| 4 | - Kiểm soát chi phí sử dụng AWS bằng AWS Budgets<br>&emsp; + Thiết lập ngân sách định kỳ<br>&emsp; + Cấu hình nhiều mức cảnh báo chi phí<br>&emsp; + Xây dựng Cost Budget<br>&emsp; + Hiểu các loại budget (Cost budget, Usage budget, Savings plans budget, RI Budget)<br>- Tìm hiểu sâu về AWS Support:<br>&emsp; + Các gói AWS Support hiện có (Định nghĩa, giá cả, khả năng)<br>&emsp; + Các loại yêu cầu hỗ trợ (Account and Billing Support, Service Limit Increase, Technical Support)<br>&emsp; + Quy trình chuyển đổi gói hỗ trợ<br>- Dịch vụ mạng AWS<br>&emsp; + Amazon Virtual Private Cloud (VPC)<br>&emsp; &emsp; * Tìm hiểu Subnet, Public Subnet, Private Subnet<br>&emsp; &emsp; * Khái niệm Route table, custom và default route table<br>&emsp; &emsp; * Kiến thức cơ bản ENI, EIP<br>&emsp; &emsp; * VPC Endpoint<br>&emsp; &emsp; * Internet Gateway<br>&emsp; + VPC Peering & Transit Gateway<br>&emsp; + VPN & Direct Connect<br>&emsp; + Elastic Load Balancing | 10/09/2025 | 10/09/2025 | [FCJ Study Web](https://cloudjourney.awsstudygroup.com)<br>[Youtube First Cloud Journey](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=1) |
| 5 | - Chủ đề VPC:<br>&emsp; + Kiến trúc và khái niệm NAT Gateway<br>&emsp; + Security Group<br>&emsp; + NACL<br>&emsp; + VPC Flow Logs<br>- VPC Peering & Transit Gateway:<br>&emsp; + VPC Peering (Định nghĩa, Thiết lập, Mẫu, Kịch bản, Kiến trúc)<br>&emsp; + Khái niệm Transit Gateway và Attachment<br>- VPN & Direct Connect:<br>&emsp; + Tổng quan môi trường hybrid<br>&emsp; + VPN Site to Site & VPN Client to Site<br>&emsp; + AWS Direct Connect<br>&emsp; + Elastic Load Balancing (Giao thức, Tính năng, Health check)<br>&emsp; &emsp; * Application, Network, Classic, Gateway Load Balancer (Khả năng, Thuộc tính)<br>&emsp; &emsp; * Sticky Session, ALB (Định nghĩa, Lớp hoạt động)<br>&emsp; &emsp; * Khả năng định tuyến dựa trên path của ALB<br>- Thực hành IAM nâng cao<br>&emsp; + Tìm hiểu sâu IAM (Shared Account Access, Granular Access Control, Secure Application Access)<br>&emsp; + IAM Policy, IAM Role | 11/09/2025 | 11/09/2025 | [FCJ Study Web](https://cloudjourney.awsstudygroup.com)<br>[Youtube First Cloud Journey](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=1) |
| 6 | - Tìm hiểu sâu về tường lửa VPC<br>&emsp; + Security Group<br>&emsp; + Network ACLs<br>&emsp; + VPC Resource Map<br>- Bài tập thực hành:<br>&emsp; + Xây dựng VPC<br>&emsp; + Xây dựng subnet<br>&emsp; + Xây dựng Internet Gateway<br>&emsp; + Xây dựng Route Table<br>&emsp; + Xây dựng Security Group<br>&emsp; + Kích hoạt VPC Flow Logs<br>&emsp; + Xây dựng EC2 Server<br>&emsp; + Xây dựng NAT Gateway<br>&emsp; + Áp dụng Reachability Analyzer | 12/09/2025 | 12/09/2025 | [FCJ Study Web](https://cloudjourney.awsstudygroup.com)<br>[Youtube First Cloud Journey](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=1) |
| 7 | - Triển khai CloudWatch Monitoring and Alerting<br>- Nghiên cứu và triển khai Site-to-Site VPN | 13/09/2025 | 13/09/2025 | [FCJ Study Web](https://cloudjourney.awsstudygroup.com)<br>[Youtube First Cloud Journey](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=1) |
| CN | - Ôn tập và làm lại các bước cấu hình EC2,..<br>- Mục đích, ứng dụng, thực hành với project cá nhân:<br> + Auto scaling group + Load Balancer<br> + EC2 + S3 | 13/09/2025 | 13/09/2025 | [FCJ Study Web](https://cloudjourney.awsstudygroup.com)<br>[Youtube First Cloud Journey](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=1) |

<!-- End of table -->

### Kết quả tuần 1:

#### **Kiến thức cốt lõi AWS & Hạ tầng toàn cầu**
- **AWS Leadership Principles**: Nắm vững 16 nguyên tắc lãnh đạo AWS, đặc biệt "Customer Obsession" và "13 năm liên tiếp dẫn đầu"
- **AWS Global Infrastructure**:
  - **Availability Zone (AZ)**: Chứa một hoặc nhiều data center, cung cấp cô lập lỗi, khuyến nghị deploy app trên 2 AZ
  - **Region**: Tối thiểu 3 AZ mỗi region
  - **Edge Location**: 
    - CloudFront (CDN)
    - Web Application Firewall (WAF) 
    - Route 53 (DNS Service)
- **AWS Management Tools**:
  - AWS Management Console (Service Search, Support Center, CLI)
  - AWS SDK (Xử lý credential, logic retry, data marshalling, serialization, deserialization)
- **Nghiên cứu mở rộng**: Well Architecture Framework

#### **Quản lý ngân sách & Hỗ trợ**
- **Phương pháp tối ưu chi phí**:
  - Chọn cấu hình phù hợp, tận dụng saving plans, reserved instances, spot instances
  - Thiết kế giải pháp tối ưu, cấu hình AWS Budget
  - Theo dõi chi phí theo phòng ban với cost allocation tags
- **AWS Budgets**:
  - Thiết lập budget định kỳ để giám sát liên tục
  - Cấu hình nhiều ngưỡng cảnh báo (50%, 80%, 90%, 100%)
  - Triển khai cảnh báo actual và forecasted
  - Lọc theo tags để theo dõi chi phí theo project/department
  - Xây dựng Cost Budget và Usage Budget (account phải active > 1 tháng)
- **Saving Plans**:
  - Budget chỉ giám sát tổng saving plan, không phải từng plan riêng lẻ
  - Best practice: Cost Explorer → Reports → SP Utilization/Coverage → filter
- **AWS Support Plans**:
  - **Basic**: Truy cập 24/7, best practices, hỗ trợ kiến trúc building block
  - **Business**: Hướng dẫn theo use-case, AWS Trusted Advisor, hỗ trợ phần mềm bên thứ 3
  - **Enterprise**: Hướng dẫn kiến trúc phần mềm, Infrastructure Event Management, TAM, hỗ trợ ưu tiên
- **Các loại yêu cầu hỗ trợ**: Account/Billing, Service Limit Increase, Technical Support

#### **Khái niệm cốt lõi VPC & Networking**
- **VPC (Virtual Private Cloud)**:
  - Nằm trong 1 region, yêu cầu khai báo CIDR IPv4 (bắt buộc)
  - Giới hạn: 5 VPC/region/account
  - Use case: Cô lập môi trường (Production/Dev/Test/Staging)
  - Mỗi subnet giữ lại 5 IP: Network, broadcast, router, DNS, tính năng tương lai
  - Mỗi subnet chỉ tồn tại trong 1 AZ
  - **Loại Subnet**: Public (giao tiếp bên ngoài), Private (giao tiếp nội bộ)
- **Network Components**:
  - **ENI Components**: EIP, MAC, Private IP Address
  - **VPC Endpoints**: Interface endpoint, Gateway endpoint
  - **Kết nối Internet**: Internet Gateway + Public IP + Route Table mapping
  - **NAT Gateway**: Cho phép private subnet giao tiếp ra ngoài, chặn truy cập inbound trực tiếp
- **Security & Monitoring**:
  - **Security Groups**: Stateful, chỉ allow rules, áp dụng lên ENI, mặc định chặn inbound, cho phép outbound
  - **NACL (Network Access Control List)**: Stateless, áp dụng lên subnets, rules đánh giá từ trên xuống
  - **VPC Flow Logs**: Theo dõi IP traffic, lưu trữ trên S3 hoặc CloudWatch Logs
- **Load Balancers**:
  - **ALB**: Layer 7, định tuyến dựa trên path, HTTP/HTTPS, định tuyến ngoài VPC
  - **NLB**: Layer 4, auto-scale, IP tĩnh, hiệu suất hàng đầu (hàng triệu requests/giây)
  - **Classic LB**: Layer 4&7, chi phí cao hơn, ít sử dụng
  - **Gateway LB**: Layer 3, chuyển tiếp đến virtual appliances

#### **Networking & Kết nối nâng cao**
- **VPC Peering & Transit Gateway**:
  - **VPC Peering**: Kết nối 1:1, không hỗ trợ transitive routing, yêu cầu thiết lập route table
  - **Transit Gateway**: Hub trung tâm liên kết nhiều VPC, tạo TGW, attachments, route tables
- **VPN & Direct Connect**:
  - **VPN Site-to-Site, VPN Client-to-Site**: Khuyến nghị dùng giải pháp bên thứ 3 từ AWS Marketplace
  - **AWS Direct Connect**: Kết nối ổn định, Hosted Connection cho phép thiết lập băng thông tùy chỉnh
- **Hybrid DNS**: Outbound/inbound endpoints, S3 resolver rules

#### **Bài Lab & Buổi thực hành**
- **VPC Setup & Configuration**:
  - Xây dựng VPC, Subnet, Internet Gateway, Route Table
  - Thiết lập Security Groups, NACL
  - Kích hoạt VPC Flow Logs
  - Xây dựng EC2 Server, NAT Gateway
  - Áp dụng Reachability Analyzer
- **Session Manager**: Thiết lập kết nối EC2, quản lý session logs, Port Forwarding
- **Auto Scaling Group + ALB**: Thực hành chi tiết
- **Key-pair Management**: Để lấy password administrator và SSH vào EC2

#### **Nghiên cứu mở rộng**
- **Advanced Networking - Specialty Study Guide**: Chuẩn bị cho AWS Advanced Networking - Specialty exam
- **Well Architecture Framework**: Best practices cho kiến trúc AWS
- **Quản lý ngân sách**: AWS Budgets, Cost Explorer, phương pháp tối ưu chi phí

#### **Năng lực thực hành đạt được**
- Xây dựng và cấu hình VPC hoàn chỉnh
- Triển khai networking components (IGW, NAT, Route Tables)
- Thiết lập bảo mật (Security Groups, NACL)
- Thực hành VPC Peering và Transit Gateway
- Vận hành AWS Management Console và CLI
- Kiểm soát chi phí với AWS Budgets
- Hiểu các loại Load Balancer và các kịch bản sử dụng
