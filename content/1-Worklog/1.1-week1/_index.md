---
title : "Week 1 Worklog"
date :  2025-09-10 
weight : 1 
chapter : false
pre : " <b> 1.1 </b> "
---
### Week 1 Goals:
- **Set up AWS account** and explore fundamental services
- **Finish Module 01-02**: Leadership Principles, Global Infrastructure, Management Tools
- **AWS Budget Management**: AWS Budgets, Cost Optimization, Support Plans
- **Study VPC & Networking**: VPC, Subnet, Security Groups, Load Balancers
- **Practice sessions**: Build VPC, EC2, NAT Gateway, VPC Peering
- **Extended learning**: Well Architecture Framework, Advanced Networking

### Weekly Task Schedule

| Day | Task | Start date | Completion date | References |
|---|---|---|---|---|
| 2 | - Meet FCJ team members<br>- Review internship policies and guidelines | 08/09/2025 | 08/09/2025 |  |
| 3 | - Register AWS account<br>- Study AWS services:<br>&emsp; + Understanding MFA, IAM groups, IAM users<br>&emsp; + Account information viewing and updating<br>&emsp; + IAM user account alias creation<br>- Practice architecture diagrams on [draw.io](https://draw.io)<br>- Cloud computing concepts (definition, advantages)<br>- Understanding Access Keys<br>- Complete modules 01-02<br>&emsp; + Leadership Principles<br>&emsp; + AZ - Availability Zone concepts<br>&emsp; + Region fundamentals<br>&emsp; + Edge location overview<br>&emsp; &emsp; * CloudFront (CDN)<br>&emsp; &emsp; * Web Application Firewall (WAF)<br>&emsp; &emsp; * Route 53 (DNS Service)<br>&emsp; + AWS Management Console (Service Search, Support Center, CLI)<br>&emsp; + AWS cost management and optimization<br>&emsp; + AWS Support usage<br>- Finish all module 01 labs<br>- Extended research on Well-Architected Framework | 09/09/2025 | 09/09/2025 | [FCJ Study Web](https://cloudjourney.awsstudygroup.com)<br>[Youtube First Cloud Journey](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=1) |
| 4 | - Control AWS usage costs using AWS Budgets<br>&emsp; + Setting up recurring budgets<br>&emsp; + Configuring multiple cost alert levels<br>&emsp; + Building Cost Budgets<br>&emsp; + Understanding budget categories (Cost budget, Usage budget, Savings plans budget, RI Budget)<br>- Deep dive into AWS Support:<br>&emsp; + Available AWS Support tiers (Definition, pricing, capabilities)<br>&emsp; + Support request categories (Account and Billing Support, Service Limit Increase, Technical Support)<br>&emsp; + Support plan switching process<br>- AWS networking services<br>&emsp; + Amazon Virtual Private Cloud (VPC)<br>&emsp; &emsp; * Understanding Subnet, Public Subnet, Private Subnet<br>&emsp; &emsp; * Route table, custom and default route table concepts<br>&emsp; &emsp; * ENI, EIP fundamentals<br>&emsp; &emsp; * VPC Endpoint<br>&emsp; &emsp; * Internet Gateway<br>&emsp; + VPC Peering & Transit Gateway<br>&emsp; + VPN & Direct Connect<br>&emsp; + Elastic Load Balancing | 10/09/2025 | 10/09/2025 | [FCJ Study Web](https://cloudjourney.awsstudygroup.com)<br>[Youtube First Cloud Journey](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=1) |
| 5 | - VPC Topics:<br>&emsp; + NAT Gateway architecture and concepts<br>&emsp; + Security Group<br>&emsp; + NACL<br>&emsp; + VPC Flow Logs<br>- VPC Peering & Transit Gateway:<br>&emsp; + VPC Peering (Definition, Setup, Samples, Scenarios, Architecture)<br>&emsp; + Transit Gateway and Attachment concepts<br>- VPN & Direct Connect:<br>&emsp; + Hybrid environment overview<br>&emsp; + VPN Site to Site & VPN Client to Site<br>&emsp; + AWS Direct Connect<br>&emsp; + Elastic Load Balancing (Protocols, Features, Health check)<br>&emsp; &emsp; * Application, Network, Classic, Gateway Load Balancer (Capabilities, Attributes)<br>&emsp; &emsp; * Sticky Session, ALB (Definition, Operation layer)<br>&emsp; &emsp; * ALB path-based routing capability<br>- Advanced IAM practice<br>&emsp; + IAM deep dive (Shared Account Access, Granular Access Control, Secure Application Access)<br>&emsp; + IAM Policy, IAM Role | 11/09/2025 | 11/09/2025 | [FCJ Study Web](https://cloudjourney.awsstudygroup.com)<br>[Youtube First Cloud Journey](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=1) |
| 6 | - VPC firewall deep dive<br>&emsp; + Security Group<br>&emsp; + Network ACLs<br>&emsp; + VPC Resource Map<br>- Hands-on exercises:<br>&emsp; + Build VPC<br>&emsp; + Build subnet<br>&emsp; + Build Internet Gateway<br>&emsp; + Build Route Table<br>&emsp; + Build Security Group<br>&emsp; + Activate VPC Flow Logs<br>&emsp; + Build EC2 Server<br>&emsp; + Build NAT Gateway<br>&emsp; + Apply Reachability Analyzer | 12/09/2025 | 12/09/2025 | [FCJ Study Web](https://cloudjourney.awsstudygroup.com)<br>[Youtube First Cloud Journey](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=1) |
| 7 | - Deploy CloudWatch Monitoring and Alerting<br>- Study and deploy Site-to-Site VPN | 13/09/2025 | 13/09/2025 | [FCJ Study Web](https://cloudjourney.awsstudygroup.com)<br>[Youtube First Cloud Journey](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=1) |
| CN | - Recap and redo EC2 configuration steps,..<br>- Purpose, application, practice with personal project:<br> + Auto scaling group + Load Balancer<br> + EC2 + S3 | 13/09/2025 | 13/09/2025 | [FCJ Study Web](https://cloudjourney.awsstudygroup.com)<br>[Youtube First Cloud Journey](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=1) |

<!-- End of table -->

### Week 1 Results:

#### **AWS Core Knowledge & Global Infrastructure**
- **AWS Leadership Principles**: Grasped 16 AWS leadership principles, notably "Customer Obsession" and "13 consecutive years at the top"
- **AWS Global Infrastructure**:
  - **Availability Zone (AZ)**: Houses one or more data centers, provides fault isolation, recommended to deploy apps across 2 AZs
  - **Region**: Minimum 3 AZs per region
  - **Edge Location**: 
    - CloudFront (CDN)
    - Web Application Firewall (WAF) 
    - Route 53 (DNS Service)
- **AWS Management Tools**:
  - AWS Management Console (Service Search, Support Center, CLI)
  - AWS SDK (Credential handling, retry logic, data marshalling, serialization, deserialization)
- **Extended Research**: Well Architecture Framework

#### **Budget Management & Support**
- **Cost Optimization Approaches**:
  - Select appropriate configurations, utilize saving plans, reserved instances, spot instances
  - Architect optimized solutions, configure AWS Budget
  - Department-level cost tracking with cost allocation tags
- **AWS Budgets**:
  - Set up recurring budgets for continuous monitoring
  - Configure multiple alert thresholds (50%, 80%, 90%, 100%)
  - Implement actual and forecasted alerts
  - Filter by tags to monitor costs by project/department
  - Build Cost Budget and Usage Budget (account must be active > 1 month)
- **Saving Plans**:
  - Budget only monitors total saving plan, not individual plans
  - Best practice: Cost Explorer → Reports → SP Utilization/Coverage → filter
- **AWS Support Plans**:
  - **Basic**: 24/7 access, best practices, building block architecture support
  - **Business**: Use-case specific guidance, AWS Trusted Advisor, third-party software support
  - **Enterprise**: Software architecture guide, Infrastructure Event Management, TAM, prioritized support
- **Support Request Categories**: Account/Billing, Service Limit Increase, Technical Support

#### **VPC & Networking Core Concepts**
- **VPC (Virtual Private Cloud)**:
  - Resides in 1 region, requires CIDR IPv4 declaration (mandatory)
  - Limit: 5 VPCs/region/account
  - Use case: Environment isolation (Production/Dev/Test/Staging)
  - Each subnet reserves 5 IPs: Network, broadcast, router, DNS, future features
  - Each subnet exists in only 1 AZ
  - **Subnet Types**: Public (external communication), Private (internal communication)
- **Network Components**:
  - **ENI Components**: EIP, MAC, Private IP Address
  - **VPC Endpoints**: Interface endpoint, Gateway endpoint
  - **Internet Connectivity**: Internet Gateway + Public IP + Route Table mapping
  - **NAT Gateway**: Enables private subnet outbound communication only, blocks direct inbound access
- **Security & Monitoring**:
  - **Security Groups**: Stateful, allow rules only, applied to ENI, default blocks inbound, permits outbound
  - **NACL (Network Access Control List)**: Stateless, applied to subnets, rules evaluated top-to-bottom
  - **VPC Flow Logs**: Track IP traffic, store on S3 or CloudWatch Logs
- **Load Balancers**:
  - **ALB**: Layer 7, path-based routing, HTTP/HTTPS, routing outside VPC
  - **NLB**: Layer 4, auto-scale, static IP, top performance (millions of requests/second)
  - **Classic LB**: Layer 4&7, higher cost, rarely used
  - **Gateway LB**: Layer 3, forward to virtual appliances

#### **Advanced Networking & Connectivity**
- **VPC Peering & Transit Gateway**:
  - **VPC Peering**: 1:1 connection, no transitive routing support, requires route table setup
  - **Transit Gateway**: Central hub linking multiple VPCs, create TGW, attachments, route tables
- **VPN & Direct Connect**:
  - **VPN Site-to-Site, VPN Client-to-Site**: Recommended to use third-party solutions from AWS Marketplace
  - **AWS Direct Connect**: Stable connection, Hosted Connection allows customizable bandwidth setup
- **Hybrid DNS**: Outbound/inbound endpoints, S3 resolver rules

#### **Hands-on Labs & Practice Sessions**
- **VPC Setup & Configuration**:
  - Build VPC, Subnet, Internet Gateway, Route Table
  - Set up Security Groups, NACL
  - Activate VPC Flow Logs
  - Build EC2 Server, NAT Gateway
  - Apply Reachability Analyzer
- **Session Manager**: Establish EC2 connections, manage session logs, Port Forwarding
- **Auto Scaling Group + ALB**: Detailed practice
- **Key-pair Management**: For getting administrator password and SSH into EC2

#### **Extended Research**
- **Advanced Networking - Specialty Study Guide**: Preparation for AWS Advanced Networking - Specialty exam
- **Well Architecture Framework**: Best practices for AWS architecture
- **Budget Management**: AWS Budgets, Cost Explorer, cost optimization approaches

#### **Practical Competencies Gained**
- Build and configure complete VPC
- Deploy networking components (IGW, NAT, Route Tables)
- Set up security (Security Groups, NACL)
- Practice VPC Peering and Transit Gateway
- Operate AWS Management Console and CLI
- Control costs with AWS Budgets
- Understand different Load Balancer types and scenarios
