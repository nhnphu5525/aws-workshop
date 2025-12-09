---
title: "Event 4"
date: 2025-11-29
weight: 5
chapter: false
pre: " <b> 4.5 </b> "
---

## AWS Cloud Mastery Series #3 - Well-Architected Security Pillar

### Event Information

| | |
|---|---|
| **Event Name** | AWS Well-Architected Security Pillar |
| **Date** | Saturday, November 29, 2025 |
| **Time** | 8:30 AM – 12:00 PM |
| **Location** | AWS Vietnam Office |
| **Main Topic** | Security Pillar - IAM, Detection, Infrastructure Protection, Data Protection, Incident Response |
| **Role** | Attendee |

---

### Event Summary

A half-day workshop on the Security Pillar of AWS Well-Architected Framework. The speakers connected theoretical principles to real-world scenarios in Vietnamese enterprises, covering five core pillars with practical demonstrations.

---

### Security Foundation

Core principles discussed:
- **Least Privilege**: Minimum permissions for each task
- **Zero Trust**: Always verify regardless of network location
- **Defense in Depth**: Multiple security layers

---

### Five Security Pillars

#### Pillar 1: Identity & Access Management
Key practices emphasized:
- Avoid long-term credentials - use IAM roles
- Enable MFA for all human users
- Use IAM Identity Center for multi-account environments
- Implement SCPs and Permission Boundaries

#### Pillar 2: Detection
Detection components:
- **CloudTrail**: Organization-wide API logging
- **GuardDuty**: Intelligent threat detection
- **Security Hub**: Aggregated security findings
- **EventBridge**: Automated response triggers

#### Pillar 3: Infrastructure Protection
Network security architecture:
- VPC segmentation by sensitivity
- Security Groups as primary defense
- AWS WAF for web application protection
- AWS Shield for DDoS protection

#### Pillar 4: Data Protection
Data security practices:
- KMS for key management with automatic rotation
- Encryption at rest and in transit for all services
- Secrets Manager for credential rotation
- Data classification with enforcement via SCPs

#### Pillar 5: Incident Response
Response framework:
1. Preparation: Runbooks and game days
2. Detection: GuardDuty and CloudTrail alerts
3. Containment: Isolate and preserve evidence
4. Eradication: Remove threats
5. Recovery: Restore from clean backups
6. Post-incident: Document lessons learned

---

### Key Takeaways

1. **IAM is foundational** - All other controls can be bypassed without proper identity management
2. **Detection enables response** - Comprehensive logging must be enabled and reviewed
3. **Automation is essential** - Manual security processes do not scale
4. **Defense in depth works** - Layer multiple controls for redundancy
5. **Encryption should be default** - KMS overhead is minimal

**Actionable items from this workshop:**
- Audit IAM policies with Access Analyzer
- Enable organization-level CloudTrail
- Implement automated GuardDuty response
- Review encryption across all data stores
- Create and test incident response playbooks

---

### Event Gallery

![Security Workshop Opening](/images/Event-Participated/Event-4/pic1.jpg)
*Opening session on AWS Well-Architected Security Pillar*

![IAM Best Practices](/images/Event-Participated/Event-4/pic2.jpg)
*Deep dive into Identity and Access Management*

![Group Discussion](/images/Event-Participated/Event-4/pic3.jpg)
*Interactive discussion on security best practices*

---

*Security must be a shared responsibility across development, operations, and security teams. The Well-Architected framework provides a common language for these conversations.*
