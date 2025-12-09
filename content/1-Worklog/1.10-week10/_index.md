---
title: "Week 10 Worklog"
date: 2025-11-10
weight: 10
chapter: false
pre: " <b> 1.10 </b> "
---

### Week 10 Goals:
- Develop backend - Hybrid Search Engine (Text search + semantic search)
- Practice Lab 22-25: Serverless, API Gateway, CI/CD, CloudWatch, X-Ray
- Research and implement hybrid search for MapVibe

### Weekly Task Schedule:

| Day | Task | Start Date | Completion Date | References |
|---|---|---|---|---|
| 2 | - Team project session: Develop backend - Hybrid Search Engine<br>&emsp; + Research best practices, papers on hybrid search engine<br>&emsp; + Design preliminary architecture for hybrid search engine | 10/11/2025 | 10/11/2025 | [Hybrid Search Paper](https://arxiv.org/pdf/2408.09236) |
| 3 | - Practice Lab 22: Serverless - Lambda interaction with S3 and DynamoDB<br>&emsp; + Process and Optimize Image Size on AWS<br>&emsp; + Build Lambda Function for Image Processing, S3 Bucket<br>&emsp; + Write data to Amazon DynamoDB | 11/11/2025 | 11/11/2025 | [Lab 22](https://000078.awsstudygroup.com/vi/) |
| 4 | - Practice Lab 23: Serverless - Guide to writing Front-end calling API Gateway<br>&emsp; + Deploy Lambda function (write, read, delete data)<br>&emsp; + Deploy API Gateway, build methods<br>&emsp; + Deploy and activate CORS<br>&emsp; + Test API with Postman and front-end | 12/11/2025 | 12/11/2025 | [Lab 23](https://000079.awsstudygroup.com/vi/) |
| 5 | - Team project session: Develop backend - Hybrid Search Engine<br>&emsp; + Run and test hybrid search engine with collected data<br>&emsp; + Complete hybrid search engine architecture | 13/11/2025 | 13/11/2025 | [Supabase Hybrid Search](https://supabase.com/docs/guides/ai/hybrid-search) |
| 6 | - Practice Lab 24: Serverless - CI/CD with CodePipeline<br>&emsp; + Build Git repo, SAM pipeline<br>&emsp; + Build pipeline for front-end<br>- Practice Lab 25: Serverless - Monitor with CloudWatch and X-Ray<br>&emsp; + Debug with CloudWatch Logs<br>&emsp; + Build custom metrics, CloudWatch Alarm<br>&emsp; + Trace with X-ray | 14/11/2025 | 14/11/2025 | [Lab 24](https://000084.awsstudygroup.com/vi/)<br>[Lab 25](https://000085.awsstudygroup.com/vi/) |

### Week 10 Results:

#### **Team Project - Hybrid Search Engine Development**
- **Daily Session (4/11)**: Plan processing query feature
  - Goal: Query must handle geographic location (District 1, near me) + semantic meaning
  - Concern: Accuracy of query results
- **Research Phase**:
  - Read paper on hybrid search: [Hybrid Search](https://arxiv.org/pdf/2408.09236)
  - Reference Supabase hybrid search implementation
  - **Key insight**: Pure vector search misses keyword matches, pure text search misses semantic similarity
- **Architecture Design**:
  ```
  Query → [Text Search (BM25)] → Score A
        → [Vector Search]      → Score B
        → RRF Fusion           → Final Ranking
  ```
- **Implementation with PostgreSQL**:
  - Full-text search: `to_tsvector('vietnamese', description) @@ plainto_tsquery('vietnamese', query)`
  - Vector search: `embedding <-> query_embedding` with pgvector
  - **RRF (Reciprocal Rank Fusion)**: `1/(k + rank_a) + 1/(k + rank_b)` with k=60
  - Geospatial filter: `ST_DWithin(location, user_location, radius_meters)`
- **Testing Results**:
  - Query "quiet cafe district 1" → Top 5 results relevant
  - Query "good breakfast place nearby" → Results sorted by distance + rating
  - **Performance**: <100ms for 10k records with proper indexing

#### **Lab 22: Serverless - Lambda + S3 + DynamoDB**
- **Image Processing Pipeline**:
  - S3 triggers Lambda when image uploaded
  - Lambda resize image (thumbnail, medium, large)
  - Store metadata in DynamoDB
  - **Tip**: Set Lambda memory 1024MB+ for image processing, CPU scales with memory
- **DynamoDB Patterns**:
  - Single-table design: PK = `PLACE#123`, SK = `REVIEW#456`
  - GSI for query by different access patterns
  - **Gotcha**: DynamoDB scan = expensive, always use query with key conditions

#### **Lab 23: API Gateway + Lambda**
- **REST API Setup**:
  - Lambda Proxy Integration: API Gateway passes entire request to Lambda
  - Method: GET /places, POST /places, GET /places/{id}
  - **CORS config**: Allow-Origin, Allow-Methods, Allow-Headers - crucial for frontend!
- **Testing Workflow**:
  - Postman collection with environment variables
  - Test each endpoint before integrating frontend
  - **Tip**: Enable CloudWatch Logs for API Gateway to debug integration issues

#### **Lab 24 & 25: CI/CD + Monitoring**
- **SAM Pipeline**:
  - `sam init` → `sam build` → `sam deploy`
  - Pipeline stages: Source → Build → Test → Deploy (Dev) → Approve → Deploy (Prod)
  - **Benefit**: Infrastructure and application code in same repo, deploy together
- **CloudWatch Deep Dive**:
  - **Logs Insights query**:
    ```
    fields @timestamp, @message
    | filter @message like /ERROR/
    | sort @timestamp desc
    | limit 20
    ```
  - **Custom Metrics**: `put-metric-data` for business metrics (orders/minute, search latency)
  - **Alarms**: Lambda errors > 5 in 5 minutes → SNS notification
- **X-Ray Tracing**:
  - Visualize request flow: API Gateway → Lambda → DynamoDB
  - Identify bottlenecks: See DynamoDB query slow → Add GSI
  - **Service Map**: Overview of entire architecture, dependencies
