---
title: "Sự kiện 2"
date: 2025-11-15
weight: 3
chapter: false
pre: " <b> 4.3 </b> "
---

## AWS Cloud Mastery Series #1 - AI/ML/GenAI on AWS

### Thông tin sự kiện

| | |
|---|---|
| **Tên sự kiện** | AWS Cloud Mastery Series #1 - AI/ML/GenAI on AWS |
| **Ngày** | 15 tháng 11, 2025 |
| **Diễn giả** | Danh Hoang Hieu Nghi (AI Engineer, Renova Cloud), Dinh Le Hoang Anh (Cloud Engineer Trainee), Lam Tuan Kiet (Senior DevOps Engineer FPT Software) |
| **Vai trò** | Người tham dự |
| **Chủ đề chính** | Xây dựng intelligent agents và ứng dụng generative AI với Amazon Bedrock |

---

### Tóm tắt sự kiện

Phiên đầu tiên của AWS Cloud Mastery Series tập trung vào triển khai thực tế các giải pháp AI/ML sử dụng Amazon Bedrock và các dịch vụ AWS AI. Các diễn giả chuyên gia chia sẻ kinh nghiệm thực tế xây dựng intelligent agents và ứng dụng RAG sẵn sàng cho production.

---

### Các phiên kỹ thuật

#### Kỹ thuật Prompt Engineering
Phiên bao gồm các phương pháp prompting cần thiết cho tương tác với model:
- **Zero-shot prompting**: Hướng dẫn trực tiếp không có ví dụ
- **Few-shot learning**: Sử dụng 2-3 ví dụ để hướng dẫn hành vi model
- **Chain-of-thought**: Chia nhỏ vấn đề phức tạp thành các bước suy luận

#### Triển khai kiến trúc RAG
Workshop trình diễn xây dựng ứng dụng dựa trên kiến thức:
1. Chiến lược nhập và chia nhỏ tài liệu
2. Vector embeddings với Amazon OpenSearch
3. Semantic search và context injection
4. Tạo response với trích dẫn nguồn

#### Amazon Bedrock AgentCore
Các thành phần AgentCore được thảo luận:
- **Runtime**: Môi trường thực thi cho các hoạt động agent
- **Memory**: Quản lý state qua các cuộc hội thoại
- **Identity**: Xác thực và ủy quyền
- **Code Interpreter**: Thực thi an toàn code được tạo

#### Thách thức triển khai Production
Các diễn giả nhấn mạnh các cân nhắc về production readiness:
- Tối ưu hiệu suất và mục tiêu latency
- Kiểm soát bảo mật và bảo vệ dữ liệu
- Quản lý chi phí cho AI workloads
- Thiết lập monitoring và observability

---

### Điểm nổi bật Q&A

**Xử lý tin nhắn khối lượng lớn:**
- Sử dụng Kinesis cho các kịch bản high-throughput thay vì SQS
- DynamoDB Streams để đảm bảo thứ tự
- S3 + Lambda cho xử lý batch payload lớn

**Rate Limiting AI Chatbots:**
- Triển khai request queuing với SQS
- Sử dụng response caching với DynamoDB hoặc ElastiCache
- Xem xét xử lý async với webhooks để thông báo người dùng

---

### Bài học rút ra

Workshop cung cấp insights thực tế để xây dựng ứng dụng AI:
1. **Bắt đầu với use cases rõ ràng** - Xác định vấn đề kinh doanh trước khi chọn foundation models
2. **Triển khai RAG** - Sử dụng retrieval-augmented generation cho responses dựa trên kiến thức
3. **Thiết kế cho production** - Xem xét bảo mật, monitoring và chi phí từ đầu
4. **Chọn frameworks phù hợp** - Simple RAG vs multi-agent dựa trên độ phức tạp

---

### Thư viện ảnh sự kiện

![Khai mạc AWS Cloud Mastery Series](https://nhnphu5525.github.io/aws-workshop/images/Event-Participated/Event-2/pic1.jpg)
*Phiên khai mạc AWS Cloud Mastery Series #1*

![Workshop kỹ thuật](https://nhnphu5525.github.io/aws-workshop/images/Event-Participated/Event-2/pic2.jpg)
*Workshop thực hành về Amazon Bedrock*

![Phiên Q&A](https://nhnphu5525.github.io/aws-workshop/images/Event-Participated/Event-2/pic3.jpg)
*Q&A tương tác với các diễn giả chuyên gia*

---

*Sự kết hợp giữa bài trình bày của chuyên gia và trình diễn thực hành làm cho đây trở thành một phiên có giá trị để hiểu về triển khai GenAI trên AWS.*
