---
title: "Week 8 Worklog"
date: 2025-10-27
weight: 8
chapter: false
pre: " <b> 1.8 </b> "
---

### Week 8 Goals:
- Team project session: plan UI/UX design, database, data collection
- Continue Lab 17: VPC Endpoints, Peering, Network Manager
- Practice Lab 18: Deploy Wordpress on AWS Cloud
- Practice Lab 19: AWS CloudFormation

### Weekly Task Schedule:

| Day | Task | Start Date | Completion Date | References |
|---|---|---|---|---|
| 2 | - Team project session: Plan UI/UX design, preliminary database design, data collection plan | 27/10/2025 | 27/10/2025 | |
| 3 | - Continue Practice Lab 17:<br>&emsp; + VPC Endpoints for AWS Services<br>&emsp; &emsp; * Deploy and test VPC Endpoint<br>&emsp; + VPC Endpoint Services<br>&emsp; + VPC Peering<br>&emsp; &emsp; * VPC Peering Request, Routing Configuration<br>&emsp; + Transit Gateway Network Manager<br>&emsp; &emsp; * Deploy Network Manager, Set up Site<br>&emsp; &emsp; * Network Insights | 28/10/2025 | 28/10/2025 | [Lab 17](https://000092.awsstudygroup.com/vi/) |
| 4 | - Practice Lab 18: Deploy Wordpress on AWS Cloud<br>&emsp; + Prepare VPC, Subnet, Security Groups<br>&emsp; + Launch EC2 Instance and Database Instance<br>&emsp; + Deploy Wordpress on EC2<br>&emsp; + Build Autoscaling for Wordpress<br>&emsp; &emsp; * Build AMI, Launch Template, Target Group<br>&emsp; &emsp; * Build Load Balancer, Auto Scaling Group<br>&emsp; + Backup and restore database<br>&emsp; + Build CloudFront for Web Server | 29/10/2025 | 29/10/2025 | [Lab 18](https://000101.awsstudygroup.com/vi/) |
| 5 | - Team project session: Start data collection based on preliminary database design | 30/10/2025 | 30/10/2025 | |
| 6 | - Practice Lab 19: AWS CloudFormation<br>&emsp; + Build IAM User and IAM Role<br>&emsp; + CloudFormation basics<br>&emsp; &emsp; * Build Workspace, CloudFormation Template<br>&emsp; + Advanced CloudFormation<br>&emsp; &emsp; * Custom resources (Lambda Function, Stack)<br>&emsp; &emsp; * Mappings and Stacksets<br>&emsp; &emsp; * Drift Detection | 31/10/2025 | 31/10/2025 | [Lab 19](https://000037.awsstudygroup.com/vi/) |

### Week 8 Results:

#### **Team Project - UI/UX & Database Planning**
- **Daily Session (20/10)**: Skip since waiting for architecture feedback from mentor
- **UX/UI Design on Figma** (Phu responsible):
  - User flow: Search → Browse results → View detail → Save/Review
  - Search UI: Map-based search with filters (distance, rating, cuisine type)
  - Responsive design for mobile-first approach
- **Daily Session (23/10)**: Skip since entire team focusing on UI =)))
- **Team photo**: Pending, couldn't arrange schedule

#### **Lab 17 (continued): VPC Advanced Networking**
- **VPC Endpoints** - Private access to AWS services:
  - **Gateway Endpoint**: S3 and DynamoDB only, free, add route to route table
  - **Interface Endpoint**: Most other services, creates ENI in subnet, has cost ($0.01/hour + data)
  - **Practical use case**: Lambda in private subnet accesses S3 without NAT Gateway → saves data transfer cost
- **VPC Peering**:
  - Non-transitive: VPC A ↔ VPC B and VPC B ↔ VPC C, but A cannot reach C through B
  - Need to update route tables on both sides
  - CIDR must not overlap - plan IP ranges from the start!
- **Transit Gateway Network Manager**:
  - Global view of network topology
  - Route Analyzer: Check which path traffic takes
  - **Practical insight**: Use for multi-region, multi-account architectures

#### **Lab 18: Wordpress High Availability**
- **Architecture Pattern - Classic 3-tier**:
  - Web tier: EC2 behind ALB, Auto Scaling Group (min 2, max 4)
  - App tier: Wordpress on EC2, shared storage with EFS
  - DB tier: RDS MySQL Multi-AZ
- **AMI Golden Image Strategy**:
  - Deploy Wordpress + plugins → Build AMI → Use in Launch Template
  - User Data only for mounting EFS and starting services
  - **Benefit**: Faster scaling, consistent deployments
- **CloudFront Integration**:
  - Cache static assets (images, CSS, JS)
  - Origin: ALB (dynamic) + S3 (uploads)
  - Cache behavior: `/wp-content/uploads/*` → S3, `*` → ALB
- **Backup Strategy**:
  - RDS automated backups: retention 7 days
  - Manual snapshot before major changes
  - **Restore test**: Important! Tried restoring from snapshot to verify

#### **Lab 19: AWS CloudFormation**
- **Template Structure**:
  ```yaml
  AWSTemplateFormatVersion, Description, Parameters, Mappings, Resources, Outputs
  ```
  - Parameters: Input values when creating stack (instance type, environment name)
  - Mappings: Lookup tables (AMI ID per region)
  - Outputs: Export values for cross-stack references
- **Custom Resources with Lambda**:
  - When CloudFormation doesn't support resource type
  - Lambda receives event from CFN, processes, sends response back to CFN
  - **Use case**: Build resources in third-party services, run custom logic
- **StackSets - Multi-account deployment**:
  - Deploy same template to multiple accounts/regions
  - Needs setup: Admin account + Target accounts trust
  - **Guard rails**: Deploy security baselines across organization
- **Drift Detection**:
  - Detect manual changes outside CloudFormation
  - `IN_SYNC` vs `MODIFIED` vs `DELETED`
  - **Best practice**: Run drift detection weekly, fix drift or import changes into template
