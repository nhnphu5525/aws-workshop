---
title: "Event 2"
date: 2025-11-15
weight: 3
chapter: false
pre: " <b> 4.3 </b> "
---

## AWS Cloud Mastery Series #1 - AI/ML/GenAI on AWS

### Event Information

| | |
|---|---|
| **Event Name** | AWS Cloud Mastery Series #1 - AI/ML/GenAI on AWS |
| **Date** | November 15, 2025 |
| **Speakers** | Danh Hoang Hieu Nghi (AI Engineer, Renova Cloud), Dinh Le Hoang Anh (Cloud Engineer Trainee), Lam Tuan Kiet (Senior DevOps Engineer FPT Software) |
| **Role** | Attendee |
| **Main Topic** | Building intelligent agents and generative AI applications with Amazon Bedrock |

---

### Event Summary

The first session of AWS Cloud Mastery Series focused on practical implementation of AI/ML solutions using Amazon Bedrock and AWS AI services. Expert speakers shared real-world experience building production-ready intelligent agents and RAG-based applications.

---

### Technical Sessions

#### Prompt Engineering Techniques
The session covered essential prompting methods for model interaction:
- **Zero-shot prompting**: Direct instruction without examples
- **Few-shot learning**: Using 2-3 examples to guide model behavior
- **Chain-of-thought**: Breaking complex problems into reasoning steps

#### RAG Architecture Implementation
The workshop demonstrated building knowledge-grounded applications:
1. Document ingestion and chunking strategies
2. Vector embeddings with Amazon OpenSearch
3. Semantic search and context injection
4. Response generation with source citations

#### Amazon Bedrock AgentCore
Key AgentCore components discussed:
- **Runtime**: Execution environment for agent operations
- **Memory**: State management across conversations
- **Identity**: Authentication and authorization
- **Code Interpreter**: Safe execution of generated code

#### Production Deployment Challenges
The speakers emphasized production readiness considerations:
- Performance optimization and latency targets
- Security controls and data protection
- Cost management for AI workloads
- Monitoring and observability setup

---

### Q&A Highlights

**Handling High-Volume Messages:**
- Use Kinesis for high-throughput scenarios over SQS
- DynamoDB Streams for ordering guarantees
- S3 + Lambda for large payload batch processing

**Rate Limiting AI Chatbots:**
- Implement request queuing with SQS
- Use response caching with DynamoDB or ElastiCache
- Consider async processing with webhooks for user notification

---

### Key Takeaways

The workshop provided practical insights for building AI applications:
1. **Start with clear use cases** - Define business problems before selecting foundation models
2. **Implement RAG** - Use retrieval-augmented generation for knowledge-grounded responses
3. **Design for production** - Consider security, monitoring, and cost from the beginning
4. **Choose appropriate frameworks** - Simple RAG vs multi-agent based on complexity

---

### Event Gallery

![AWS Cloud Mastery Series Opening](/images/Event-Participated/Event-2/pic1.jpg)
*Opening session of AWS Cloud Mastery Series #1*

![Technical Workshop](/images/Event-Participated/Event-2/pic2.jpg)
*Hands-on workshop on Amazon Bedrock*

![Q&A Session](/images/Event-Participated/Event-2/pic3.jpg)
*Interactive Q&A with expert speakers*

---

*The combination of expert presentations and hands-on demonstrations made this a valuable session for understanding GenAI implementation on AWS.*
