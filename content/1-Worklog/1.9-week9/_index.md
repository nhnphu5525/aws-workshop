---
title: "Week 9 Worklog"
date: 2025-11-03
weight: 9
chapter: false
pre: " <b> 1.9 </b> "
---

### Week 9 Goals:
- Team project session: complete database, collect data, UI feedback
- Practice Lab 19, 20: CDK basics
- Practice Lab 21: Infrastructure as Code - Three-Tier Architecture

### Weekly Task Schedule:

| Day | Task | Start Date | Completion Date | References |
|---|---|---|---|---|
| 2 | - Team project session: Complete database design, continue data collection | 03/11/2025 | 03/11/2025 | |
| 3 | - Practice Lab 19: CDK basics<br>&emsp; + Build IAM Role<br>&emsp; + CDK basics: Build workspace, set up Cloud9<br>&emsp; + Build CDK Template<br>&emsp; + Update CDK Template | 04/11/2025 | 04/11/2025 | [Lab 19 CDK](https://000038.awsstudygroup.com/vi/) |
| 4 | - Practice Lab 20: CDK Basics - 2<br>&emsp; + Build IAM Role, run EC2, set up VSCode<br>&emsp; + ECS, ALB and API Gateway<br>&emsp; + Lambda and S3<br>&emsp; + Nested stack: Build nested stacks with CDK | 05/11/2025 | 05/11/2025 | [Lab 20](https://000076.awsstudygroup.com/vi/) |
| 5 | - Team project session: Complete data collection, feedback to improve UI design on Figma | 06/11/2025 | 06/11/2025 | |
| 6 | - Practice Lab 21: Introduction to Infrastructure as Code<br>&emsp; + Build Lambda function<br>&emsp; + Build VPC and EC2<br>&emsp; + Deploy Three-Tier Architecture<br>&emsp; &emsp; * Web Tier, Application Tier, Database Tier | 07/11/2025 | 07/11/2025 | [Lab 21](https://000102.awsstudygroup.com/vi/) |

### Week 9 Results:

#### **Team Project - Database Design & Data Collection**
- **Database Design completed (Quan + Dat responsible)**:
  - **DB to Vector**: Convert text data to vector embeddings for semantic search
  - Cost tracking: **$16.58** for embedding API calls + **$0.000028** for additional operations
  - Use OpenAI text-embedding-3-small (cheaper, good enough for use case)
- **PostgreSQL Schema Design**:
  - `places` table: id, name, address, lat, lng, description, embedding (vector)
  - `reviews` table: id, place_id, user_id, content, rating, created_at
  - **PostGIS extension**: `geometry(Point, 4326)` for location queries
  - Index strategy: B-tree for id/foreign keys, GiST for geometry, IVFFlat for vectors
- **Data Collection** (entire team participates):
  - Crawl restaurant information from various sources
  - Fill data into shared Google Sheet, standard format
  - **Lesson learned**: Data quality more important than quantity - must validate before import
- **Daily Session (2/11)**: 8AM morning
- **UI Feedback**: Review Figma designs, contribute feedback on UX flow

#### **Lab 19: AWS CDK Basics**
- **CDK vs CloudFormation**:
  - CDK: Write code (TypeScript/Python), generate CloudFormation
  - Benefit: IDE support, reusable constructs, loops/conditions easier than YAML
  - **Trade-off**: Extra abstraction layer, harder to debug when issues occur
- **CDK Concepts**:
  - **App**: Entry point, contains multiple Stacks
  - **Stack**: Unit of deployment, maps 1:1 with CFN stack
  - **Construct**: Building blocks, has 3 levels (L1 = CFN, L2 = curated, L3 = patterns)
- **Workflow**:
  ```bash
  cdk init app --language typescript  # Init project
  cdk synth                           # Generate CFN template
  cdk diff                            # Preview changes
  cdk deploy                          # Deploy stack
  cdk destroy                         # Cleanup
  ```
- **Best Practices**:
  - Use L2 constructs when possible (sensible defaults)
  - Environment separation with cdk.json contexts
  - Stack naming convention: `{project}-{env}-{service}`

#### **Lab 20: CDK Advanced Patterns**
- **ECS with CDK**:
  - `ApplicationLoadBalancedFargateService` L3 construct - builds ALB + ECS + Target Group in 10 lines
  - Compared to raw CloudFormation: ~200 lines → 10 lines, huge productivity gain
- **Serverless with CDK**:
  - `NodejsFunction` construct: Auto bundle with esbuild, TypeScript support
  - Event sources: `S3EventSource`, `SqsEventSource`, `ApiGatewayEventSource`
  - **Tip**: `bundling.minify = true` for production, reduce cold start
- **Nested Stacks Pattern**:
  - Main stack imports child stacks
  - Cross-stack references with `CfnOutput` and `Fn.importValue`
  - **When to use**: >500 resources, separate team ownership, independent deployment

#### **Lab 21: Three-Tier Architecture IaC**
- **Complete Stack**:
  - Web tier: ALB + ASG with Launch Template
  - App tier: Lambda functions with API Gateway
  - Data tier: RDS PostgreSQL Multi-AZ
- **Security**:
  - Security Groups chained: ALB → App → DB
  - Each tier only accepts traffic from previous tier
  - DB in private subnet, no public access
- **Practical Implementation**:
  - Test end-to-end: User → ALB → Lambda → RDS → Response
  - Verify failover: Stop primary DB, confirm auto-failover to standby
  - **Cost estimate**: ~$50/month for small setup (t3.micro + db.t3.micro)
