---
title: "Week 4 Worklog"
date: 2025-09-29
weight: 4
chapter: false
pre: " <b> 1.4 </b> "
---

### Week 4 Goals:
- Deep practice with Amazon EC2: build instances, connect, backup, AMI, IAM governance
- Study Module 04: AWS Storage Services (S3, Glacier, Snow Family, Storage Gateway)
- Study Module 05: AWS Security Services (IAM, Cognito, KMS, Security Hub)
- Participate in event: AI-Driven Development Life Cycle

### Weekly Task Schedule:

| Day | Task | Start Date | Completion Date | References |
|---|---|---|---|---|
| 2-3 | - Practice Lab 9: Amazon Elastic Compute Cloud (EC2)<br>&emsp; + Build VPC for Linux and Windows<br>&emsp; + Build Security Groups for Linux and Windows<br>&emsp; + Launch and connect Windows instance<br>&emsp; + Launch and connect Linux instance<br>&emsp; + EC2 basics: Change configuration, build snapshot, build Custom AMI<br>&emsp; + Access when losing Key Pair (SSM, User Data)<br>&emsp; + Set up Desktop for EC2-Ubuntu 22.04<br>&emsp; + Amazon EBS Snapshots Archive, Share AMI | 29/09/2025 | 30/09/2025 | [Lab 9](https://000004.awsstudygroup.com/vi/) |
| 3 | - Continue Lab 9:<br>&emsp; + Deploy Node.js application on Amazon Linux<br>&emsp; &emsp; * Deploy LAMP web server, set up database, phpMyAdmin<br>&emsp; &emsp; * Deploy Node.js on Linux<br>&emsp; + Node.js application on Amazon EC2 Windows<br>&emsp; &emsp; * Deploy XAMPP, Nodejs on Windows<br>&emsp; + Limit resource usage with IAM<br>&emsp; &emsp; * Limit by Region, Instance Family, Instance type<br>&emsp; &emsp; * Limit EBS volume storage type<br>&emsp; &emsp; * Limit delete permissions by IP, time | 30/09/2025 | 30/09/2025 | [Lab 9](https://000004.awsstudygroup.com/vi/) |
| 4 | - Study Module 04: AWS Storage Services<br>&emsp; + 04-01: Amazon S3 - Access Point - Storage Class<br>&emsp; + 04-02: S3 Static Website & CORS - Control Access - Object Key & Performance - Glacier<br>&emsp; + 04-03: Snow Family - Storage Gateway - Backup | 01/10/2025 | 01/10/2025 | [FCJ Youtube](https://www.youtube.com/watch?v=_yunukwcAwc) |
| 5 | - Participate in event: AI-Driven Development Life Cycle: Reimagining Software Engineering | 02/10/2025 | 02/10/2025 | |
| 6 | - Study Module 05: AWS Security Services<br>&emsp; + 05-01: Shared Responsibility Model<br>&emsp; + 05-02: Amazon Identity and Access Management<br>&emsp; + 05-03: Amazon Cognito<br>&emsp; + 05-04: AWS Organization<br>&emsp; + 05-05: AWS Identity Center<br>&emsp; + 05-06: Amazon Key Management Service<br>&emsp; + 05-07: AWS Security Hub | 03/10/2025 | 03/10/2025 | [FCJ Youtube](https://www.youtube.com/watch?v=tsobAlSg19g) |

### Week 4 Results:

#### **Lab 9: Amazon EC2 - Deployment and management**
- **Instance Management**:
  - Built separate VPC for Linux and Windows with corresponding Security Groups - crucial to isolate environments
  - Windows uses RDP (port 3389), Linux uses SSH (port 22) - Security Group must open correct port
  - **Practical tip**: Changing instance type requires stopping instance first, EBS volume can resize online but only increase not decrease
- **EBS Snapshots & AMI**:
  - Snapshot is incremental backup - only saves changed blocks, saves storage cost
  - Building AMI from running instance works but recommend stopping to ensure data consistency
  - **EBS Snapshots Archive**: 75% cheaper than standard, but restore takes 24-72h - only use for long-term backup
  - Share AMI cross-account: Modify permissions, add account ID - useful for multi-account strategy
- **Recover Access when losing Key Pair**:
  - **SSM Session Manager**: No need to open port 22/3389, more secure, needs IAM Role with `AmazonSSMManagedInstanceCore`
  - **User Data method**: Mount root volume to another instance, add public key to `~/.ssh/authorized_keys`
  - **Lesson learned**: Always enable SSM from the start, backup key pair in secure location (Secrets Manager)
- **Deploy Applications**:
  - LAMP stack: Apache + MySQL + PHP, config in `/var/www/html/`
  - Node.js on Linux: Use nvm to manage versions, pm2 for process management
  - Windows XAMPP: Easier to setup but not recommended for production

#### **IAM Governance - Cost & Security Control**
- **Resource Limitation Policies**:
  - **Limit by Region**: `"Condition": {"StringEquals": {"aws:RequestedRegion": "ap-southeast-1"}}` - blocks resource creation in other regions
  - **Limit EC2 Family**: Only allow t3, t3a (burstable) for dev environment, block c5, r5 (expensive)
  - **Limit Instance Type**: `ec2:InstanceType` condition key, dev only gets t3.micro/small
  - **EBS Volume Type**: Block io1, io2 (expensive IOPS), only allow gp3
- **Advanced Conditions**:
  - **IP-based restriction**: `aws:SourceIp` condition, only allow from company IP range
  - **Time-based restriction**: `aws:CurrentTime` condition, block delete actions outside business hours
  - **Practical insight**: Combine multiple conditions with AND logic to build granular control

#### **Module 04: AWS Storage Services**
- **S3 Storage Classes** - Choosing right class saves 60-95% cost:
  - **Standard**: Frequently accessed, ≥3 AZ, 99.999999999% durability
  - **Intelligent-Tiering**: Unknown access pattern, auto-move objects, no retrieval fee - best choice when unsure of pattern
  - **Standard-IA**: Infrequent access (>30 days), minimum 128KB charge, 30-day minimum storage
  - **Glacier Instant**: Archive but needs millisecond access, 68% cheaper than Standard
  - **Glacier Deep Archive**: $1/TB/month, 12-48h retrieval, compliance data 7-10 years
- **S3 Performance Optimization**:
  - 3,500 PUT/POST/DELETE and 5,500 GET/HEAD per prefix per second
  - **Prefix strategy**: `bucket/user1/photos/` vs `bucket/user2/photos/` - each prefix has separate throughput
  - Multipart upload: Required >5GB, recommend >100MB, parallel upload faster
- **Snow Family** - Offline data transfer:
  - Snowball Edge: 80TB, has compute capability for edge processing
  - Snowmobile: 100PB, literally a truck - use when >10PB data
  - **Rule of thumb**: >1 week to transfer over network → use Snow Family
- **Storage Gateway** - Hybrid cloud storage:
  - File Gateway: NFS/SMB interface to S3, cache frequently accessed data locally
  - Volume Gateway: iSCSI block storage, Stored mode (full local) vs Cached mode (only cache local)

#### **Module 05: AWS Security Services**
- **Shared Responsibility Model**:
  - AWS: Security OF the cloud (hardware, software, networking, facilities)
  - Customer: Security IN the cloud (data, IAM, encryption, network config)
  - **Key insight**: EC2 → customer manages OS patches; RDS → AWS manages OS, customer manages DB config
- **IAM Advanced Concepts**:
  - **Policy Evaluation Logic**: Explicit Deny → Explicit Allow → Implicit Deny
  - **Permission Boundary**: Sets maximum permissions for IAM users/roles - prevents privilege escalation
  - **Resource-based Policy**: Attach to resource (S3 bucket policy), supports cross-account access directly
- **Cognito** - User management:
  - **User Pools**: Authentication, sign-up/sign-in, MFA, password policies - returns JWT tokens
  - **Identity Pools**: Authorization, exchanges tokens for temporary AWS credentials
  - **Use case**: Mobile/web app needs user login + access AWS resources (S3, DynamoDB)
- **AWS Organizations & SCPs**:
  - SCP (Service Control Policies): Restricts actions across entire OU/account
  - SCP doesn't grant permissions, only restricts - still needs IAM policies
  - **Example**: Block root user from doing anything except specific actions
- **KMS Encryption**:
  - AWS Managed Keys: Free, auto-rotate yearly, cannot control
  - Customer Managed Keys (CMK): $1/month + API calls, custom rotation, audit via CloudTrail
  - **Envelope encryption**: Data key encrypts data, CMK encrypts data key - efficient for large data

#### **Event: AI-Driven Development Life Cycle**
- Hands-on with Amazon CodeWhisperer (now Amazon Q Developer): Generate code from comments, supports Python, JS, Java, C#
- AI-assisted development workflow: Write comment → generate code → review → refine
- **Practical takeaway**: AI tools boost productivity 25-30% for routine tasks, but still needs human review especially for security-sensitive code
- Networking with other developers, discussion about AI integration in real projects
