---
title: "Week 6 Worklog"
date: 2025-10-13
weight: 6
chapter: false
pre: " <b> 1.6 </b> "
---

### Week 6 Goals:
- Practice Lab 13: Optimize EC2 costs with Lambda
- Practice Lab 14: Serverless - Lambda with S3 and DynamoDB
- Practice Lab 15: Getting started with AWS CLI
- Participate in workshop: Data Science on AWS
- Team project session: define solution architecture, budget estimation

### Weekly Task Schedule:

| Day | Task | Start Date | Completion Date | References |
|---|---|---|---|---|
| 2 | - Team project session: Define and research solution architecture for web app | 13/10/2025 | 13/10/2025 | [Proposal Template](https://workshop-sample.fcjuni.com/2-proposal/) |
| 3 | - Practice Lab 13: Optimize EC2 costs with Lambda<br>&emsp; + Build VPC, Security Group, EC2 instance<br>&emsp; + Set up Incoming Web-hooks Slack<br>&emsp; + Build Tag for Instance<br>&emsp; + Build Role for Lambda<br>&emsp; + Build Lambda Function: stop instance, start instance<br>&emsp; + Test results | 14/10/2025 | 14/10/2025 | [Lab 13](https://000022.awsstudygroup.com/vi/) |
| 4 | - Practice Lab 14: Serverless - Lambda interaction with S3 and DynamoDB<br>&emsp; + Process and Optimize Image Size on AWS<br>&emsp; &emsp; * Build Lambda Function for Image Processing<br>&emsp; &emsp; * Build S3 Bucket, IAM Policy for Lambda<br>&emsp; + Write data to Amazon DynamoDB<br>&emsp; &emsp; * Build and Manage Tables in DynamoDB<br>&emsp; &emsp; * Build Lambda Function to Write data | 15/10/2025 | 15/10/2025 | [Lab 14](https://000078.awsstudygroup.com/vi/) |
| 5 | - Participate in workshop: Data Science on AWS - Unlock data power with cloud computing<br>- Team project session: Complete solution architecture, budget estimation for web app | 16/10/2025 | 16/10/2025 | [AWS Calculator](https://calculator.aws/#/) |
| 6 | - Practice Lab 15: Getting started with AWS CLI<br>&emsp; + Deploy AWS CLI<br>&emsp; + Check resources via CLI<br>&emsp; + AWS CLI with Amazon S3<br>&emsp; + AWS CLI with Amazon SNS<br>&emsp; + AWS CLI with IAM<br>&emsp; + AWS CLI with VPC and Internet Gateway<br>&emsp; + Build EC2 using AWS CLI<br>&emsp; + Troubleshooting | 17/10/2025 | 17/10/2025 | [Lab 15](https://000011.awsstudygroup.com/vi/) |

### Week 6 Results:

#### **Lab 13: Optimize EC2 Costs with Lambda**
- **Cost Optimization Strategy**:
  - Dev/Test instances don't need to run 24/7
  - Schedule: Start 8AM, Stop 6PM weekdays → Save 65% cost
  - **ROI calculation**: t3.medium $0.0416/hour × 14 hours/day saved × 22 days = ~$12.8/month/instance
- **Lambda Implementation**:
  - **Start Function**: `ec2.start_instances(InstanceIds=[...])`, trigger by EventBridge 8AM
  - **Stop Function**: `ec2.stop_instances(InstanceIds=[...])`, trigger by EventBridge 6PM
  - **Tag-based filtering**: `Environment: dev` to only affect dev instances
- **Slack Integration**:
  - Incoming Webhook URL from Slack App
  - Lambda post message when start/stop succeeds
  - **Benefit**: Team awareness, easier troubleshooting
- **IAM Role for Lambda**:
  - `ec2:StartInstances`, `ec2:StopInstances`, `ec2:DescribeInstances`
  - **Least privilege**: Only allow necessary actions, resource-level permissions

#### **Lab 14: Serverless with Lambda, S3, DynamoDB**
- **Image Processing Pipeline**:
  - S3 trigger: `s3:ObjectCreated:*` on bucket `uploads/`
  - Lambda resize image → Save to `thumbnails/` bucket
  - **Sharp library**: Lambda Layer because of native bindings
  - **Memory setting**: 1024MB for image processing (CPU scales with memory)
- **DynamoDB Design**:
  - **Partition Key**: Unique identifier, high cardinality (user_id, place_id)
  - **Sort Key**: Range queries (timestamp, rating)
  - **Single-table design**: `PK: PLACE#123, SK: META` for place info, `SK: REVIEW#456` for reviews
  - **GSI**: `GSI1PK: CITY#HCM, GSI1SK: RATING#4.5` for query places by city sorted by rating
- **Lambda Best Practices**:
  - **Cold start**: Initialize DB connections outside handler
  - **Timeout**: Set reasonable timeout (default 3s, max 15 mins)
  - **Error handling**: Try-catch, DLQ for failed events

#### **Lab 15: AWS CLI Mastery**
- **Setup**: `aws configure` with Access Key, Secret Key, Region, Output format
- **S3 Commands**:
  ```bash
  aws s3 mb s3://my-bucket                    # Build bucket
  aws s3 cp file.txt s3://my-bucket/          # Upload
  aws s3 sync ./local s3://my-bucket/folder   # Sync directory
  aws s3 ls s3://my-bucket --recursive        # List all objects
  ```
- **EC2 Commands**:
  ```bash
  aws ec2 describe-instances --query 'Reservations[].Instances[].InstanceId'
  aws ec2 run-instances --image-id ami-xxx --instance-type t3.micro
  aws ec2 terminate-instances --instance-ids i-xxx
  ```
- **Troubleshooting**:
  - `--debug` flag to view full request/response
  - `aws sts get-caller-identity` to verify credentials
  - **Common errors**: ExpiredToken, AccessDenied (check IAM permissions)

#### **Workshop: Data Science on AWS**
- Hands-on with SageMaker: Build notebook, train model, deploy endpoint
- Data processing with Glue: ETL jobs, Data Catalog
- Analytics with Athena: Query S3 data with SQL
- **Key insight**: AWS has full ML pipeline, no need to manage infrastructure

#### **Team Project Session - Architecture & Budget**
- **Solution Architecture**:
  - Frontend: React (S3 + CloudFront) 
  - Backend: Lambda + API Gateway (serverless, pay per request)
  - Database: RDS PostgreSQL with PostGIS (geospatial queries)
  - Search: pgvector extension for vector search
  - Auth: Cognito User Pools
- **Budget Estimation (AWS Calculator)**:
  - RDS db.t3.micro: ~$15/month
  - Lambda: ~$0 (free tier 1M requests)
  - S3 + CloudFront: ~$5/month
  - **Total dev environment**: ~$20-30/month
- **Architecture Decision**: Serverless-first to minimize ops and cost
