---
title: "Week 11 Worklog"
date: 2025-11-17
weight: 11
chapter: false
pre: " <b> 1.11 </b> "
---

### Week 11 Goals:
- Develop backend - RAG System (combining hybrid search engine and LLM)
- Practice Lab 26-29: Serverless, SAM, SageMaker, AWS Toolkit
- Research and implement RAG for MapVibe chatbot

### Weekly Task Schedule:

| Day | Task | Start Date | Completion Date | References |
|---|---|---|---|---|
| 2 | - Team project session: Develop backend - RAG System<br>&emsp; + Improve accuracy of hybrid search engine with LLM<br>&emsp; + Add chat feature for users to search<br>&emsp; + Research best practices for RAG systems | 17/11/2025 | 17/11/2025 | [RAG Paper](https://arxiv.org/pdf/2005.11401) |
| 3 | - Practice Lab 26: Serverless - Front-end calling API Gateway<br>&emsp; + Deploy Front-end, deploy API Gateway<br>&emsp; + Test API with Postman and Front-end<br>- Practice Lab 27: Serverless with Lambda, API Gateway and SAM<br>&emsp; + Deploy Frontend and Backend<br>&emsp; + Deploy ride times system<br>&emsp; + Image processing (Chroma Key, Photo-Compositing) | 18/11/2025 | 18/11/2025 | [Lab 26](https://000135.awsstudygroup.com/vi/)<br>[Lab 27](https://000066.awsstudygroup.com/vi/) |
| 4 | - Practice Lab 28: SageMaker Immersion Day Workshop<br>&emsp; + Build SageMaker Studio, clone GitHub repo<br>&emsp; + Feature Engineering: Data Wrangler, analyze Dataset<br>&emsp; + Train/Tune/Deploy XGBoost model<br>&emsp; + Evaluate performance and auto-tune model | 19/11/2025 | 19/11/2025 | [Lab 28](https://000200.awsstudygroup.com/vi/) |
| 5 | - Team project session: Develop backend - RAG System<br>&emsp; + Run and test RAG system with collected data<br>&emsp; + Complete RAG system | 20/11/2025 | 20/11/2025 | [AWS RAG](https://aws.amazon.com/vi/what-is/retrieval-augmented-generation/) |
| 6 | - Practice Lab 29: AWS Toolkit for VS Code - Amazon Q & CodeWhisperer<br>&emsp; + Deploy AWS Toolkit for VS Code<br>&emsp; + Connect AWS account, change Region<br>&emsp; + Authentication: IAM Identity Center, IAM credentials, Builder ID<br>&emsp; + Interact with services: AWS Explorer, Amazon Q, CodeWhisperer | 21/11/2025 | 21/11/2025 | [Lab 29](https://000087.awsstudygroup.com/vi/) |

### Week 11 Results:

#### **Team Project - RAG System Development**
- **Daily Session (14/11)**: Review hybrid search, plan RAG integration
  - Hybrid search already works, now need to wrap with LLM to answer natural language
  - Phu + Quan responsible for RAG implementation
- **RAG Architecture Design**:
  ```
  User Query → Query Understanding → Hybrid Search (Top-K) → Context Building → LLM Generation → Response
  ```
  - **Naive RAG problem**: Stuff all context into prompt → exceed token limit, expensive
  - **Solution**: Retrieve top-5 results, summarize context, generate focused response
- **Implementation Details**:
  - Query understanding: Extract location, cuisine type, preferences from natural language
  - Context template:
    ```
    Based on the following restaurant information:
    {retrieved_places}
    
    Answer the question: {user_query}
    ```
  - LLM: Claude 3 Haiku (fast, cheap) for chat, Sonnet for complex queries
- **Chat Features**:
  - Conversation history: Store in session, pass to LLM for context
  - Multi-turn: "Any closer options?" → LLM understands context from previous turns
  - **Fallback**: When no results found → "Sorry, I couldn't find a suitable restaurant..."
- **Testing**:
  - "Find cafe with wifi in district 3" → Return relevant cafes with wifi mention
  - "Does that place have parking?" → LLM checks context of previously mentioned restaurant
  - **Latency**: ~2s end-to-end (search 100ms + LLM 1.5s + overhead)

#### **Lab 26 & 27: Serverless Applications**
- **Frontend Deployment**:
  - S3 bucket with Static Website Hosting activated
  - CloudFront distribution for caching + HTTPS
  - **Tip**: Invalidate cache after each deploy: `aws cloudfront create-invalidation --distribution-id XXX --paths "/*"`
- **SAM Deep Dive**:
  - `template.yaml`: Define Lambda, API Gateway, DynamoDB in 1 file
  - `samconfig.toml`: Store deployment parameters (stack name, region, S3 bucket)
  - **Local testing**: `sam local start-api` → Test API locally before deploy
- **Image Processing (Chroma Key)**:
  - Remove background from uploaded image
  - Composite with new background
  - **Use case**: Product photos, profile pictures
  - Lambda Layer for sharp/jimp libraries

#### **Lab 28: SageMaker ML Workshop**
- **SageMaker Studio**:
  - JupyterLab environment managed by AWS
  - Kernel: Python 3 (Data Science), has pre-installed ML libraries
  - **Gotcha**: Studio domain must be in same VPC as data sources
- **Data Wrangler**:
  - Visual data transformation: Join, filter, encode, scale
  - Export to: Processing Job, Pipeline, Feature Store
  - **Benefit**: Non-ML engineers can prepare data, democratize ML
- **XGBoost Training**:
  - Built-in algorithm, no need to write training code
  - Hyperparameters: `max_depth`, `eta`, `num_round`, `objective`
  - **Automatic Model Tuning**: Define ranges, SageMaker finds best params
  - Training job: ml.m5.xlarge, ~15 min for small dataset
- **Model Deployment**:
  - Real-time endpoint: Always-on, ~$0.05/hour for ml.t3.medium
  - Serverless inference: Pay per request, cold start ~5s
  - **Choice**: Serverless for MapVibe (low traffic, cost-sensitive)

#### **Lab 29: AWS Toolkit & Amazon Q**
- **AWS Toolkit in VS Code**:
  - Explorer: Browse S3, Lambda, CloudWatch directly from IDE
  - Deploy Lambda: Right-click → Deploy to AWS
  - **Time saver**: No need to switch between IDE and Console
- **Amazon Q Developer**:
  - Inline suggestions when typing code
  - `/explain`: Explain code block
  - `/fix`: Suggest fixes for errors
  - `/optimize`: Performance improvements
  - **Security scanning**: Flag potential vulnerabilities in code
- **Authentication Methods**:
  - **IAM Identity Center** (recommended): SSO, centralized management
  - **IAM credentials**: Access key + secret, store in `~/.aws/credentials`
  - **Builder ID**: Free tier, limited features, good for personal projects
