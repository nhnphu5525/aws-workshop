---
title : "Nhật ký tuần 2"
date :  2025-09-15
lastmod : 2025-01-17
weight : 2
chapter : false
pre : " <b> 1.2 </b> "
---
### Mục tiêu tuần 2:
- **Thực hành Advanced Networking**: VPC Peering, Cross-Peer DNS, Transit Gateway
- **Học Module 03 - Compute Services**: AMI, EC2, EBS, Instance Store, Auto Scaling
- **Khám phá Storage Services**: EFS, FSx, Lightsail, AWS Backup
- **Thực hành CloudFormation**: Security Groups, RDGW, Stack management
- **Tham dự sự kiện**: Vietnam Cloud Day 2025, khám phá GenAI
- **Thực hành AWS Migration**: MGN (Application Migration Service)


### Lịch trình công việc trong tuần:

| Thứ | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|---|---|---|---|---|
| 2 | - Tìm hiểu sâu về Auto Scaling Group + Application Load Balancer <br>&emsp; + Nghiên cứu và xây dựng: target group, load balancer, auto scaling group, attach EC2 to ASG<br>- Tìm hiểu sâu cách sử dụng EC2 + S3: <br>&emsp; + Áp dụng kiến thức để lấy data, upload data lên S3 không cần accesskey<br>- Nghiên cứu Hybrid DNS và Route 53 Resolver<br>- Thực hành Module2-Lab10-01 => 02.2:<br>&emsp; + Nghiên cứu về Key Pair<br>&emsp; + Triển khai Cloudformation | 15/09/2025 | 15/09/2025 | [FCJ Study Web](https://cloudjourney.awsstudygroup.com)<br>[Youtube First Cloud Journey](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=1) |
| 3 | - Thực hành Module2-Lab10-02.03 => Lab19-07:<br>&emsp; + Thiết lập Security Group cho Cloudformation <br>&emsp; + Kết nối RDGW<br>&emsp; + Tìm hiểu Stack trong CloudFormation<br>&emsp; + Peering DNS<br>&emsp; + Cross-peer DNS<br>- Học về Transit Gateway:<br>&emsp; + Chuẩn bị trước khi xây dựng TGW<br>&emsp; + Xây dựng TGW | 16/09/2025 | 16/09/2025 | [FCJ Study Web](https://cloudjourney.awsstudygroup.com)<br>[Youtube First Cloud Journey](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=1) |
| 4 | - Xây dựng TGW Attachment<br>- Xây dựng TGW Route Table<br>- Thêm TGW Routes vào VPC Route Tables<br>- Module 03:<br>&emsp; + Học về Compute VM trên AWS<br>&emsp; + Tìm hiểu AMI, thành phần và quyền sử dụng?<br>&emsp; + EC2 Instance được backup ở đâu?<br>&emsp; + Tìm hiểu EBS, thành phần và đặc tính?<br>&emsp; + Hypervisor Nitro là gì?<br>&emsp; + Tìm hiểu Instance store và khi nào sử dụng?<br>&emsp; + Ưu, nhược điểm của Instance Store<br>&emsp; + EC2 User Data là gì?<br>&emsp; + EC2 Metadata là gì?<br>&emsp; + EC2 Auto Scaling là gì?<br>&emsp; + Có mấy tùy chọn về giá tiền khi sử dụng EC2?<br>&emsp; + Amazon Lightsail là gì? Các đặc tính, tính năng, giá cả,...?<br>&emsp; + Amazon EFS là gì? Các đặc tính, tính năng, giá cả, so sánh với EBS,...?<br>&emsp; + Amazon FSx là gì? Định nghĩa, mục đích sử dụng, tính năng,...?<br>&emsp; + MGN là gì? Mục đích sử dụng,...? | 17/09/2025 | 17/09/2025 | [FCJ Study Web](https://cloudjourney.awsstudygroup.com)<br>[Youtube First Cloud Journey](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=1) |
| 5 | - Tham dự sự kiện Viet Nam Cloud Day 2025: Ho Chi Minh City Connect Edition for Builders<br>- Khám phá GenAI: Amazon Nova, Bedrock AgentCore, ADDL,... | 18/09/2025 | 18/09/2025 | [FCJ FB Group](https://www.facebook.com/pages/Th%C3%A0nh-ph%E1%BB%91-H%E1%BB%93-Ch%C3%AD-Minh/108458769184495) |
| 6 | - Học về AWS Backup:<br>&emsp; + Thực hành xây dựng cloudformation, watchcloud, s3 bucket, sns, backup plan,...<br>&emsp; + Dọn dẹp resource<br>&emsp; + Hoàn thành full Module3-lab13 | 19/09/2025 | 19/09/2025 | [FCJ Study Web](https://cloudjourney.awsstudygroup.com)<br>[Youtube First Cloud Journey](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=1) |
| 7 | - Thực hành Module 03 - Lab 24: Sử dụng AWS Storage Gateway | 20/09/2025 | 20/09/2025 | [FCJ Study Web](https://cloudjourney.awsstudygroup.com)<br>[Youtube First Cloud Journey](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=1) |
| CN | - Ôn lại kiến thức cũ và ghi chú những phần quan trọng | 21/09/2025 | 21/09/2025 | [FCJ Study Web](https://cloudjourney.awsstudygroup.com)<br>[Youtube First Cloud Journey](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=1) |

### Kết quả tuần 2:

#### **Advanced Networking & Connectivity**
- **VPC Peering**: Thực hành xây dựng và thiết lập VPC Peering connections
- **Cross-Peer DNS**: Thiết lập DNS resolution giữa các VPC
- **Transit Gateway (TGW)**:
  - Chuẩn bị và xây dựng Transit Gateway
  - Xây dựng TGW Attachments
  - Xây dựng TGW Route Tables
  - Thiết lập routes từ TGW tới VPC Route Tables

#### **Module 03 - Compute Services**
- **AMI (Amazon Machine Image)**:
  - Hiểu AMI có thể provision 1 hoặc nhiều EC2 Instances cùng lúc
  - AMI bao gồm: Root OS volume, EBS volume mapping, quyền sử dụng AMI
- **Keypair**: Mã hóa thông tin đăng nhập cho EC2 Instance
- **EC2 Backup & EBS**:
  - EC2 backup sử dụng snapshot vào S3 (snapshot đầu tiên full, các snapshot tiếp theo incremental)
  - **Amazon EBS (Elastic Block Store)**: Block storage gắn trực tiếp vào EC2
  - EBS hoạt động độc lập với EC2, kết nối với mạng riêng của EBS
  - 2 nhóm đĩa chính: HDD & SSD, 99,9% availability qua replication giữa 3 Storage Nodes trong 1 AZ
  - EC2 luôn đi liền với EBS, thiếu EBS thì EC2 không thể hoạt động
  - EBS Multi attach: 1 EBS có thể gắn vào nhiều EC2 Instance (với Hypervisor Nitro)
- **Instance Store**:
  - Vùng đĩa NVME gắn trực tiếp lên hardware node
  - Tốc độ cao nhưng không được backup (không khuyến khích lưu trữ)
  - Dừng máy chủ sẽ xóa hết dữ liệu, restart giữ nguyên dữ liệu
  - Sử dụng cho: log, swap, paging, buffer/cache
- **EC2 Features**:
  - **EC2 User Data**: Câu lệnh chạy lần đầu khi khởi tạo EC2 từ AMI
  - **EC2 Metadata**: Thông tin về EC2 Instance (IP Private/Public, Hostname, Security Group)
  - **EC2 Auto Scaling**: Tăng giảm số lượng instance dựa theo điều kiện cụ thể
- **EC2 Pricing Options**:
  - **On-demand**: Tính theo giờ, đắt nhất, sử dụng dưới 6 tiếng
  - **Reserved Instance**: Trên 6 tiếng, discount thay đổi theo instance type
  - **Saving Plans**: Không bị giới hạn bởi instance type
  - **Spot Instance**: Tận dụng tài nguyên dư, giá rẻ nhưng có thể terminate trong 2 phút
  - **Best practice**: Kết hợp nhiều pricing options trong EC2 Auto Scaling Group

#### **Storage Services**
- **Amazon Lightsail**:
  - Dịch vụ tính toán chi phí thấp
  - Mỗi Instance Lightsail có data transfer đi kèm (giá rẻ hơn EC2)
  - Có khả năng backup
  - Chạy trong VPC đặc biệt, kết nối với VPC thông thường = 1 click peering
- **Amazon EFS**:
  - Xây dựng NFSv4 Network volume gắn vào nhiều EC2 Instance cùng lúc
  - Quy mô tới petabyte
  - EFS chỉ support Linux
  - Tính phí theo dung lượng sử dụng (EBS tính theo dung lượng cấp phát)
  - Có thể mount vào môi trường on-premise bằng DX hoặc VPN
- **Amazon FSx**:
  - Xây dựng NTFS volume gắn nhiều EC2 cùng lúc sử dụng giao thức SMB
  - Tính phí theo dung lượng sử dụng
  - Hỗ trợ tính năng deduplication
  - **FSx support cả Windows và Linux**

#### **Migration & Backup Services**
- **AWS Application Migration Service (MGN)**:
  - Migrate và replicate để xây dựng Disaster Recovery Site
  - Sử dụng máy staging có quy mô nhỏ hơn máy chính
  - Cut-over: MGN xây dựng và chạy trên EC2 (chuyển hẳn sang AWS)
- **AWS Backup**:
  - Thực hành xây dựng CloudFormation, CloudWatch, S3 bucket, SNS
  - Xây dựng backup plan và dọn dẹp resources
  - Hoàn thành Module3-lab13

#### **CloudFormation & Infrastructure as Code**
- **CloudFormation Stack Management**:
  - Thiết lập Security Groups cho CloudFormation
  - Kết nối RDGW (Remote Desktop Gateway)
  - Hiểu Stack là gì trong CloudFormation
- **Module2-Lab10-01 đến Lab19-07**: Hoàn thành các lab thực hành

#### **Sự kiện & Nghiên cứu**
- **Vietnam Cloud Day 2025**: Tham dự sự kiện Hồ Chí Minh City Connect Edition for Builders
- **GenAI Research**: Khám phá Amazon Nova, Bedrock AgentCore, ADDL
- **AWS Storage Gateway**: Thực hành Module 03 - Lab 24

#### **Năng lực thực hành đạt được**
- Thiết lập VPC Peering và Cross-Peer DNS
- Xây dựng và quản lý Transit Gateway
- Hiểu sâu về EC2, EBS, Instance Store và các pricing options
- Thực hành với EFS, FSx, Lightsail
- Sử dụng AWS Backup và Migration services
- Làm việc với CloudFormation và Infrastructure as Code
- Tham dự sự kiện công nghệ và nghiên cứu GenAI
