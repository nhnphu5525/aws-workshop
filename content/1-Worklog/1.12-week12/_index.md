---
title: "Week 12 Worklog"
date: 2025-11-24
weight: 12
chapter: false
pre: " <b> 1.12 </b> "
---

### Week 12 Goals:
- Migrate RAG System to AWS with Infrastructure as Code
- Practice Lab 30-33: IAM Governance, VPC Flow Log, Grafana, CloudWatch
- Complete and deploy RAG system for MapVibe

### Weekly Task Schedule:

| Day | Task | Start Date | Completion Date | References |
|---|---|---|---|---|
| 2 | - Team project session: Migrate RAG System to AWS<br>&emsp; + Research best practices for AWS services serving RAG<br>&emsp; + Start migrating RAG system to AWS<br>&emsp; + RDS PostgreSQL with pgvector<br>&emsp; + Amazon Bedrock for LLM | 24/11/2025 | 24/11/2025 | [AWS RDS PostgreSQL](https://aws.amazon.com/vi/rds/postgresql/)<br>[pgvector](https://github.com/pgvector/pgvector) |
| 3 | - Practice Lab 30: Cost and Resource Management with IAM<br>&emsp; + Build IAM Group and User<br>&emsp; + Limit by Region, EC2 family, instance size<br>&emsp; + Limit by EBS volume | 25/11/2025 | 25/11/2025 | [Lab 30](https://000064.awsstudygroup.com/vi/) |
| 4 | - Practice Lab 31: Monitor network infrastructure with VPC Flow Log<br>&emsp; + Activate VPC Flow Logs<br>&emsp; + Monitor network infrastructure<br>- Practice Lab 32: Getting started with Grafana on AWS<br>&emsp; + Build VPC, Security Group, EC2, IAM<br>&emsp; + Deploy and monitor with Grafana | 26/11/2025 | 26/11/2025 | [Lab 31](https://000074.awsstudygroup.com/vi/)<br>[Lab 32](https://000029.awsstudygroup.com/vi/) |
| 5 | - Team project session: Complete RAG System migration<br>&emsp; + Migrate RAG system to AWS with Infrastructure as Code<br>&emsp; + Use Terraform for deployment | 27/11/2025 | 27/11/2025 | [Terraform AWS](https://registry.terraform.io/providers/hashicorp/aws/latest/docs) |
| 6 | - Practice Lab 33: AWS CloudWatch Workshop<br>&emsp; + CloudWatch Metric: Viewing, Search, Math expressions<br>&emsp; + CloudWatch Logs and Logs Insights<br>&emsp; + CloudWatch Metric Filter<br>&emsp; + CloudWatch Alarms and Dashboards | 28/11/2025 | 28/11/2025 | [Lab 33](https://000036.awsstudygroup.com/vi/) |

### Week 12 Results:

#### **Team Project - RAG System Migration to AWS**
- **Migration Strategy**:
  - Local PostgreSQL → RDS PostgreSQL with pgvector
  - Local LLM calls → Amazon Bedrock
  - Local API → API Gateway + Lambda
  - **Why Terraform?**: Team more familiar with Terraform than CDK, easier to maintain long-term
- **RDS PostgreSQL Setup**:
  - Instance: db.t3.micro (free tier), Multi-AZ disabled (cost saving for dev)
  - **pgvector extension**: `CREATE EXTENSION vector;` - needs manual activation
  - Connection: Private subnet only, access via VPC
  - **RDS Proxy**: Connection pooling, reduces connection overhead for Lambda
  - **Tip**: Custom Parameter Group: `shared_preload_libraries = 'pg_stat_statements,pgvector'`
- **Amazon Bedrock Integration**:
  - Activate model access in console (Claude 3 Haiku, Sonnet)
  - IAM Role for Lambda: `bedrock:InvokeModel` permission
  - **Code snippet**:
    ```python
    bedrock = boto3.client('bedrock-runtime')
    response = bedrock.invoke_model(
        modelId='anthropic.claude-3-haiku-20240307-v1:0',
        body=json.dumps({"prompt": prompt, "max_tokens": 500})
    )
    ```
  - **Rate limiting**: Bedrock has quota per minute, implement retry with exponential backoff
- **Terraform Infrastructure**:
  - Modules structure:
    ```
    terraform/
    ├── modules/
    │   ├── vpc/
    │   ├── rds/
    │   ├── lambda/
    │   └── api-gateway/
    ├── environments/
    │   ├── dev/
    │   └── prod/
    └── main.tf
    ```
  - State management: S3 bucket + DynamoDB lock table
  - **Workflow**: `terraform plan` → Review → `terraform apply`
- **CI/CD for Infrastructure**:
  - GitLab CI: Terraform validate → Plan → Apply (manual approval for prod)
  - **Cost impact**: Each PR shows estimated cost change

#### **Lab 30: IAM Cost Governance**
- **Cost Control Policies**:
  - **Region restriction**: Only allow `ap-southeast-1` → Prevents accidental deploy in expensive regions
  - **Instance type restriction**: Dev account only gets t3.micro, t3.small
  - **Require tags**: Deny actions if missing `Environment`, `Project` tags
- **Practical IAM Policy**:
  ```json
  {
    "Condition": {
      "StringNotEquals": {
        "ec2:InstanceType": ["t3.micro", "t3.small"]
      }
    },
    "Effect": "Deny",
    "Action": "ec2:RunInstances",
    "Resource": "arn:aws:ec2:*:*:instance/*"
  }
  ```
- **Cost Allocation Tags**: Track cost per project, per environment, per team

#### **Lab 31 & 32: Network Monitoring**
- **VPC Flow Logs**:
  - Destination: CloudWatch Logs or S3 (cheaper for long-term)
  - Filter: ALL (accept + reject) for security analysis
  - **Query pattern**: Find rejected traffic → Identify missing Security Group rules
  - **Use case**: Debug "Lambda can't connect to RDS" → Check flow logs see reject → Fix SG
- **Grafana on AWS**:
  - EC2 t3.small, deploy Grafana OSS
  - Data source: CloudWatch metrics
  - **Dashboard for MapVibe**:
    - API latency (p50, p95, p99)
    - Error rate
    - Lambda concurrent executions
    - RDS connections, CPU, storage
  - **Alerting**: Slack notification when error rate > 5%

#### **Lab 33: CloudWatch Workshop**
- **Metrics Math**:
  - `m1/m2 * 100`: Error rate percentage
  - `RATE(m1)`: Requests per second
  - `ANOMALY_DETECTION_BAND(m1, 2)`: Auto anomaly detection
- **Logs Insights Advanced**:
  ```
  stats count(*) as requests, 
        avg(duration) as avg_latency,
        pct(duration, 95) as p95_latency
  by bin(5m)
  ```
- **Composite Alarms**:
  - Combine multiple conditions: High latency AND high error rate → Critical alert
  - Reduce alert noise: Single metric spike doesn't trigger, must have multiple signals
- **Dashboard Best Practices**:
  - Group by service: API metrics, Database metrics, Lambda metrics
  - Time range: Default 3h, drill down when investigating
  - **Annotation**: Mark deployments to correlate with metric changes
