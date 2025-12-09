---
title: "Week 7 Worklog"
date: 2025-10-20
weight: 7
chapter: false
pre: " <b> 1.7 </b> "
---

### Week 7 Goals:
- Receive feedback on architecture solution from FCJ mentors
- Practice Lab 16: Amazon ElastiCache - Redis
- Practice Lab 17: AWS Networking and Content Delivery
- Complete and submit proposal

### Weekly Task Schedule:

| Day | Task | Start Date | Completion Date | References |
|---|---|---|---|---|
| 2 | - Receive feedback on project architecture solution from FCJ mentors<br>- Listen and adjust architecture based on feedback | 20/10/2025 | 20/10/2025 | |
| 3-4 | - Practice Lab 16: Amazon ElastiCache - Redis<br>&emsp; + Build AWS Access Key, deploy and set up AWS CLI<br>&emsp; + Build ElastiCache cluster<br>&emsp; &emsp; * Build subnet group (Console & CLI)<br>&emsp; &emsp; * Build cluster (mode disabled & enabled)<br>&emsp; &emsp; * Grant access to cluster<br>&emsp; &emsp; * Connect to cluster nodes<br>&emsp; + Use AWS SDK to write and read data<br>&emsp; &emsp; * Set and Get strings, hash<br>&emsp; &emsp; * Publish/subscribe<br>&emsp; &emsp; * Write and read from stream | 21/10/2025 | 22/10/2025 | [Lab 16](https://000061.awsstudygroup.com/vi/) |
| 5 | - Complete entire proposal, deploy to GitHub and submit proposal | 23/10/2025 | 23/10/2025 | |
| 6 | - Practice Lab 17: AWS Networking and Content Delivery<br>&emsp; + Deploy VPC, Cisco CSR Agreement<br>&emsp; + VPC Components Deep Dive<br>&emsp; + Transit Gateway and Site-to-Site VPNs<br>&emsp; &emsp; * Access Cisco CSR Router with Cloud9<br>&emsp; &emsp; * Deploy Site-to-site VPN<br>&emsp; &emsp; * Add ECMP Path<br>&emsp; &emsp; * Transit Gateway Routing<br>&emsp; + Route53 DNS Endpoints and Internal Hosted Zones | 24/10/2025 | 24/10/2025 | [Lab 17](https://000092.awsstudygroup.com/vi/) |

### Week 7 Results:

#### **Team Project - Research & Architecture Phase**
- **Daily Session (13/10)**: Kick-off session, distribute research tasks
- **Research Tech Stack (completed 16/10)**:
  - Frontend: React + Vite + TailwindCSS - chosen for large ecosystem, good performance
  - Backend: Node.js + Express or Bun + Hono - considering Bun for faster runtime
  - Database: PostgreSQL + PostGIS for geospatial data (restaurants need location)
  - CI/CD: GitHub Actions or GitLab CI - team more familiar with GitLab
- **Draw Demo Architecture**: Sketched initial architecture diagram on draw.io, including:
  - 3-tier architecture: Frontend (S3 + CloudFront) → API Gateway → Lambda/ECS → RDS
  - Separate search service for vector search (hybrid search)
- **Complete SRS (19/10)**: 
  - Wrote SRS document with sections: Business Requirements, Functional Requirements, Non-functional Requirements
  - Task assignment: Thong writes main SRS, Dat + Minh write Business Processes, Quan + Phu document architecture in detail

#### **Lab 16: Amazon ElastiCache - Redis**
- **Cluster Mode Disabled vs Enabled**:
  - Disabled: Simple, 1 primary + replicas, max 5 replicas, auto-failover
  - Enabled: Sharding data across multiple nodes, horizontal scaling, higher throughput
  - **Which mode to choose?**: Disabled for simple caching, Enabled when data > 100GB or need > 1 million requests/sec
- **Redis Operations practiced**:
  - `SET/GET`: Basic key-value, use for session storage
  - `HSET/HGETALL`: Hash for user profiles, multiple fields per key
  - `PUBLISH/SUBSCRIBE`: Real-time notifications - subscribe channel, publish message
  - `XADD/XREAD`: Streams for event sourcing, message queue alternative
- **Connection Management**:
  - Security Group must allow port 6379 from application
  - Use connection pooling (ioredis) to avoid creating connection per request
  - **TTL strategy**: Set expiration for cached data, avoid stale data

#### **Lab 17: AWS Networking Deep Dive**
- **Transit Gateway Architecture**:
  - Hub-and-spoke model: TGW is central hub, each VPC attaches as spoke
  - Route propagation: Automatically learns routes from attached VPCs
  - **ECMP**: Multiple VPN tunnels, load balance traffic - increase throughput to 2.5Gbps per tunnel × number of tunnels
- **Site-to-Site VPN with Cisco CSR**:
  - Cisco CSR 1000v on EC2 as Customer Gateway
  - IPSec tunnel with BGP routing
  - **Lesson learned**: BGP convergence takes 30-60s when failover, plan for downtime
- **Route53 DNS Integration**:
  - Inbound Endpoint: On-prem resolve AWS private DNS
  - Outbound Endpoint: AWS resolve on-prem DNS
  - Private Hosted Zone: Internal DNS not exposed to internet

#### **Submit Proposal**
- Completed proposal document with architecture diagram
- Deploy to GitHub Pages for mentor review
- **Feedback pending**: Waiting for mentor to review architecture before continuing implementation
