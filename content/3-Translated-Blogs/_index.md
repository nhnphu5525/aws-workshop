---
title : "Translated Blogs"
date :  2025-10-03
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

## [Blog 1 - Accessing private Amazon API Gateway endpoints through custom Amazon CloudFront distribution using VPC Origins](./3.1-Blog-1/)
This article demonstrates how to connect Amazon CloudFront to a Private REST API in Amazon API Gateway using VPC Origins. The solution enables organizations to enhance security and performance by keeping APIs private while accessing them through CloudFront, with additional security layers like AWS Shield Advanced, geoblocking, and TLSv1.3 support. The architecture uses an internal Application Load Balancer integrated with VPC Origins to route traffic to the Private REST API through the execute-api VPC endpoint.

## [Blog 2 - Data consistency with AWS DMS Data Resync](./3.2-Blog-2/)
This post dives into AWS DMS Data Resync — a feature introduced in DMS version 3.6.1 to detect and resolve data inconsistencies during database migration automatically. Data Resync works by reading discrepancies identified by DMS data validation, retrieving current values from the source, and applying them to the target. The article discusses configuration steps and demonstrates use cases including recovering accidentally deleted records and resuming CDC tasks after table errors.

## [Blog 3 - Accelerating local serverless development with console to IDE and remote debugging for AWS Lambda](./3.3-Blog-3/)
This article covers recent improvements to enhance the local development experience for AWS Lambda. Two new Lambda features — console to IDE and remote debugging — help bridge the gap between cloud and local development. Console to IDE enables seamless transition from cloud code/test cycles to local environments with one click, while remote debugging allows developers to debug functions running in the cloud directly from their local VS Code IDE using AWS Toolkit.
