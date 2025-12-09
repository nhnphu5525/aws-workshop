---
title: "Week 5 Worklog"
date: 2025-10-06
weight: 5
chapter: false
pre: " <b> 1.5 </b> "
---

### Week 5 Goals:
- Study Module 06: AWS Database Services (RDS, Aurora, Redshift, ElastiCache)
- Practice Lab 10: Static Website Hosting with Amazon S3 and CloudFront
- Practice Lab 11: Amazon RDS - deploy application with database
- Practice Lab 12: Auto Scaling Group with Load Balancer
- Team project session: write proposal, define problem statement

### Weekly Task Schedule:

| Day | Task | Start Date | Completion Date | References |
|---|---|---|---|---|
| 2 | - Study Module 06: AWS Database Services<br>&emsp; + 06-01: Database Concepts review<br>&emsp; + 06-02: Amazon RDS & Amazon Aurora<br>&emsp; + 06-03: Redshift - ElastiCache | 06/10/2025 | 06/10/2025 | [FCJ Youtube](https://www.youtube.com/watch?v=OOD2RwWuLRw) |
| 3 | - Practice Lab 10: Static Website Hosting with Amazon S3<br>&emsp; + Build S3 bucket and upload data<br>&emsp; + Activate static website feature<br>&emsp; + Set up Block Public Access and public object<br>&emsp; + Speed up with CloudFront<br>&emsp; + Bucket versioning, move Objects<br>&emsp; + Copy S3 Objects to another region | 07/10/2025 | 07/10/2025 | [Lab 10](https://000057.awsstudygroup.com/vi/) |
| 4 | - Team project session: Start writing proposal<br>&emsp; + Define problem statement<br>&emsp; + Define main flows of web app | 08/10/2025 | 08/10/2025 | [Proposal Template](https://workshop-sample.fcjuni.com/2-proposal/) |
| 5 | - Practice Lab 11: Amazon RDS Fundamentals<br>&emsp; + Build VPC, EC2 Security Group, RDS Security Group<br>&emsp; + Build DB Subnet Group<br>&emsp; + Build EC2 instance and RDS database instance<br>&emsp; + Deploy application connecting to RDS<br>&emsp; + Backup and restore database | 09/10/2025 | 09/10/2025 | [Lab 11](https://000005.awsstudygroup.com/vi/) |
| 6 | - Practice Lab 12: Deploy FCJ Management app with Auto Scaling Group<br>&emsp; + Deploy network infrastructure, EC2, RDS<br>&emsp; + Load data for Database<br>&emsp; + Build Launch Template<br>&emsp; + Deploy Load Balancer (Target Group, ALB)<br>&emsp; + Build Auto Scaling Group<br>&emsp; + Test: manual scaling, scheduled scaling, dynamic scaling, predictive scaling | 10/10/2025 | 10/10/2025 | [Lab 12](https://000006.awsstudygroup.com/vi/) |

### Week 5 Results:

#### **Module 06: AWS Database Services**
- **Database Concepts**:
  - **OLTP** (Online Transaction Processing): Many small writes, low latency - use RDS/Aurora
  - **OLAP** (Online Analytical Processing): Complex queries, large data - use Redshift
  - **Rule of thumb**: OLTP for application database, OLAP for reporting/BI
- **Amazon RDS**:
  - Engines: MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, Aurora
  - **Multi-AZ**: Synchronous replication, automatic failover ~60s, for HA
  - **Read Replicas**: Asynchronous replication, scale read workload, cross-region for DR
  - **Backup**: Automated (retention 0-35 days), Manual snapshots (no expiration)
  - **Tip**: Enable Multi-AZ for production, Read Replica for heavy read workloads
- **Amazon Aurora**:
  - Storage auto-scales from 10GB to 128TB, 6 copies across 3 AZs
  - **Aurora Serverless v2**: Scale from 0.5 to 128 ACUs, pay per second
  - **Use case**: Variable workloads, dev/test environments, cost optimization
- **Amazon Redshift**: 
  - Columnar storage, MPP (Massively Parallel Processing)
  - **Redshift Spectrum**: Query S3 data without loading
  - Cost: ~$0.25/hour for dc2.large
- **ElastiCache**: Redis for complex data structures + persistence, Memcached for simple caching

#### **Lab 10: S3 Static Website with CloudFront**
- **S3 Static Website Hosting**:
  - Bucket name must be globally unique
  - Index document: `index.html`, Error document: `error.html`
  - **Gotcha**: Block Public Access must be disabled for public website, but use CloudFront OAI for security
- **CloudFront Integration**:
  - Edge locations: cache content near users, reduce latency from 200ms → 20ms
  - **OAI (Origin Access Identity)**: S3 bucket stays private, only CloudFront can access
  - Cache behaviors: TTL settings, query string forwarding
  - **Invalidation**: `/images/*` to clear cache when updating content, costs $0.005/path
- **S3 Versioning**:
  - Activate to track changes, recover deleted objects
  - **MFA Delete**: Require MFA to delete permanently - prevents accidental deletion
- **Cross-Region Replication**:
  - Async replication, needs versioning activated
  - **Use case**: Compliance (data in specific region), DR, latency reduction

#### **Lab 11: Amazon RDS Fundamentals**
- **Network Architecture for RDS**:
  - RDS in private subnet (no public IP)
  - EC2 Security Group → RDS Security Group (only allow port 3306/5432 from EC2 SG)
  - **DB Subnet Group**: Minimum 2 subnets in 2 AZs for Multi-AZ
- **RDS Instance Setup**:
  - Instance class: db.t3.micro (free tier), db.r5.large (production)
  - Storage: gp3 (general purpose), io1 (high IOPS)
  - **Parameter Group**: Custom settings (max_connections, slow_query_log)
- **Backup & Restore**:
  - Point-in-time recovery: Restore to any second within retention period
  - Snapshot restore: Build new instance from snapshot
  - **Tip**: Test restore process regularly, don't wait for disaster to test

#### **Lab 12: Auto Scaling Group with Load Balancer**
- **Launch Template**:
  - AMI + Instance type + Key pair + Security Groups + User Data
  - **Version control**: Each update creates new version, easy rollback
- **Application Load Balancer**:
  - **Target Group**: Health check path `/health`, interval 30s, threshold 2
  - **Listener**: Port 80 (HTTP), Port 443 (HTTPS with ACM certificate)
  - **Path-based routing**: `/api/*` → Backend TG, `/*` → Frontend TG
- **Auto Scaling Policies**:
  - **Target Tracking**: Maintain CPU at 70% - simplest, AWS auto-adjusts
  - **Step Scaling**: CPU > 80% add 2, CPU > 90% add 4 - more control
  - **Scheduled**: Scale up 9AM, scale down 6PM - predictable patterns
  - **Predictive**: ML forecast based on historical patterns - best for recurring patterns
- **Testing**: 
  - `stress --cpu 4 --timeout 300` to trigger scale out
  - Observe scale out ~3 mins, scale in ~15 mins (cooldown)

#### **Team Project Session**
- Started writing proposal for MapVibe project
- **Problem Statement**: Users struggle to find restaurants matching their preferences, lacking personalized recommendations
- **Main Flows**: Search by location/keyword → Filter (cuisine, price, rating) → View details → Read/Write reviews
- **Target Users**: Gen Z, millennials who enjoy exploring new places
