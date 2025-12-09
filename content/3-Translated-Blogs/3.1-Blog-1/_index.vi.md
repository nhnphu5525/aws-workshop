---
title : "Blog 1"
date :  2025-09-10 
weight : 1
chapter : false
pre : " <b> 3.1 </b> "
---

[**AWS Compute Blog**](https://aws.amazon.com/blogs/compute/)

## **Truy cập các endpoint riêng tư của Amazon API Gateway thông qua phân phối Amazon CloudFront tùy chỉnh bằng cách sử dụng VPC Origins**

by Napoleone Capasso and Usama Ali Khan |   on 09 SEP 2025 |   in [Advanced (300)](https://aws.amazon.com/blogs/compute/category/learning-levels/advanced-300/), [Amazon API Gateway](https://aws.amazon.com/blogs/compute/category/application-services/amazon-api-gateway-application-services/), [Amazon CloudFront](https://aws.amazon.com/blogs/compute/category/networking-content-delivery/amazon-cloudfront/), [AWS Serverless Application Model](https://aws.amazon.com/blogs/compute/category/compute/aws-serverless-application-model/), [Serverless](https://aws.amazon.com/blogs/compute/category/serverless/), [Technical How-to](https://aws.amazon.com/blogs/compute/category/post-types/technical-how-to/) |   [Permalink](https://aws.amazon.com/blogs/compute/accessing-private-amazon-api-gateway-endpoints-through-custom-amazon-cloudfront-distribution-using-vpc-origins/) |   [Share](https://aws.amazon.com/vi/blogs/compute/accessing-private-amazon-api-gateway-endpoints-through-custom-amazon-cloudfront-distribution-using-vpc-origins/#)

Các tổ chức có thể sử dụng **Amazon CloudFront Virtual Private Cloud (VPC) Origins** để phân phối nội dung từ các ứng dụng được lưu trữ trong các subnet riêng tư bên trong **Amazon VPC**. Lưu lượng mạng sẽ được truyền giữa **Amazon CloudFront** và **Application Load Balancers (ALB)**, **Network Load Balancers (NLB)** hoặc **Amazon Elastic Compute Cloud (Amazon EC2)** được triển khai trong các subnet riêng tư. Điều này có nghĩa là Amazon CloudFront có thể truy cập liền mạch cả tài nguyên công khai và tài nguyên riêng tư của Amazon Web Services (AWS).

Bài viết này minh họa cách bạn có thể kết nối CloudFront với **Private REST API trong Amazon API Gateway** bằng cách sử dụng VPC origin.

### **Tổng quan**

Các tổ chức mong muốn tăng cường bảo mật và hiệu năng cho ứng dụng của mình có thể tìm thấy nhiều lợi ích quan trọng trong kiến trúc này. Bạn có thể sử dụng nó để giữ cho các API của mình ở trạng thái riêng tư và truy cập chúng thông qua CloudFront, đồng thời triển khai thêm nhiều lớp bảo mật bổ sung như **AWS Shield Advanced**, geoblocking, và **hỗ trợ TLSv1.3** cùng với bộ mã hóa (cipher suite) tùy chỉnh. Cách tiếp cận này cho phép bạn tận dụng mạng phân phối nội dung toàn cầu của CloudFront, trong khi vẫn duy trì quyền kiểm soát chặt chẽ hơn đối với việc phân phối nội dung.

Hơn nữa, bạn có thể tăng cường kiểm soát bảo mật thông qua các tính năng tích hợp sẵn của CloudFront, chẳng hạn như tích hợp với **AWS WAF**, chứng chỉ SSL tùy chỉnh, và mã hóa ở cấp trường dữ liệu (field-level encryption). Tính năng VPC Origins loại bỏ nhu cầu phải mở tài nguyên nội bộ ra Internet công cộng, từ đó giảm thiểu bề mặt tấn công tiềm năng của ứng dụng.

Các doanh nghiệp cần duy trì các yêu cầu tuân thủ nghiêm ngặt trong khi vẫn phải phân phối nội dung trên phạm vi toàn cầu sẽ thấy giải pháp này đặc biệt hữu ích. Việc giữ toàn bộ lưu lượng trong mạng riêng tư của AWS giúp bạn đáp ứng tốt hơn các mục tiêu bảo mật và tuân thủ, đồng thời vẫn đảm bảo khả năng truy cập nhanh chóng và đáng tin cậy cho các ứng dụng của mình.

### **Tổng quan về giải pháp**

Bạn có thể thiết lập CloudFront như cổng truy cập (front door) cho ứng dụng của mình và sử dụng VPC Origins được tích hợp với một Application Load Balancer (ALB) nội bộ để định tuyến lưu lượng đến **Private REST API** thông qua **VPC endpoint** của execute-api. Toàn bộ lưu lượng giữa CloudFront và Private REST API đều được giữ hoàn toàn trong mạng riêng tư của AWS.

Hình minh họa sau đây cung cấp tổng quan về giải pháp này.

![Solution Overview](https://nhnphu5525.github.io/aws-workshop/images/translated-blogs/blog1/pic1.png)

Sơ đồ này mô tả ba dịch vụ đang chạy trong một tài khoản AWS. Phân phối CloudFront đóng vai trò là điểm truy cập chính của ứng dụng. Phân phối này kết nối với một Application Load Balancer (ALB) nội bộ bằng cách sử dụng VPC Origins. VPC endpoint dạng interface có tên execute-api được đặt làm đích (target) cho ALB nội bộ, nhằm định tuyến các yêu cầu đến Private **Amazon API Gateway**.

### **Triển khai giải pháp**

Để triển khai giải pháp này, hãy làm theo hướng dẫn trong kho **lưu trữ GitHub** và nhân bản (clone) kho lưu trữ đó.

Giải pháp này có thể được triển khai ở bất kỳ AWS Region nào. Hãy đảm bảo rằng bạn có chứng chỉ SSL hợp lệ trong **AWS Certificate Manager (ACM)** tại khu vực us-east-1, vì đây là yêu cầu cho phân phối CloudFront. Tất cả các tài nguyên khác phải nằm trong cùng một Region.

### **Điều kiện tiên quyết**

Trong hướng dẫn triển khai này, bạn sẽ cần các tài nguyên sau:

* Một Amazon VPC có ít nhất 2 Private Subnet.
* Một Public Hosted Zone trong **Amazon Route 53**.
* Một chứng chỉ SSL công khai hợp lệ trong ACM tại Region us-east-1 cho CloudFront, và một chứng chỉ khác trong cùng Region với ALB.
* Một tên miền tùy chỉnh (custom domain name) được bao phủ bởi chứng chỉ ACM dùng cho CloudFront distribution.

Đây là các tham số đầu vào (input parameters) cần thiết cho quá trình triển khai giải pháp.

### **Hướng dẫn triển khai từng bước**

Mẫu **AWS Serverless Application Model (AWS SAM)** từ kho GitHub mẫu sẽ tạo ra một kiến trúc mạng riêng tư và an toàn, cho phép kiểm soát quyền truy cập vào API Gateway thông qua CloudFront. Mẫu này khởi tạo (provision) các thành phần gồm: Private API Gateway với VPC endpoint, ALB nội bộ, và CloudFront distribution. Nó thiết lập các kênh liên lạc an toàn bằng cách triển khai các thành phần mạng riêng tư, cấu hình chứng chỉ SSL, và thiết lập định tuyến DNS của Route53. Bên cạnh đó, mẫu còn sử dụng các tài nguyên **AWS Lambda** tùy chỉnh để quản lý linh hoạt các giao diện mạng (network interface) và cấu hình nhóm bảo mật (security group) một cách tự động, từ đó cung cấp một hạ tầng mạnh mẽ và linh hoạt cho việc truy cập Private API, như được minh họa trong hình dưới đây.

![Architecture](https://nhnphu5525.github.io/aws-workshop/images/translated-blogs/blog1/pic2.png)

#### **Bước 1: Tạo CloudFront distribution và VPC Origins**

Giải pháp này tạo ra một CloudFront distribution hỗ trợ nhiều loại HTTP client khác nhau nhờ khả năng tương thích với HTTP/2 và HTTP/3, đồng thời tăng cường bảo mật cho hệ thống bằng cách bắt buộc toàn bộ lưu lượng phải sử dụng HTTPS. Ngoài ra, CloudFront distribution còn sử dụng tên miền tùy chỉnh (custom domain) cùng với chứng chỉ SSL do người dùng cung cấp. Application Load Balancer (ALB) nội bộ được cấu hình làm origin cho CloudFront distribution, và nó được tạo ra bằng cách sử dụng tính năng VPC Origins.

```yaml
########### Cloudfront Distribution ###############
  CloudFrontDistribution:
    Type: AWS::CloudFront::Distribution
    Properties:
      DistributionConfig:
        HttpVersion: http2and3
        Comment: CloudFront Distribution with VPC Origin Integration
        Aliases: 
        - !Ref CloudFrontDomainName
        ViewerCertificate:
          AcmCertificateArn: !Ref CloudFrontCertificateARN
          MinimumProtocolVersion: TLSv1.2_2021
          SslSupportMethod: sni-only
        Origins:
        - Id: AlbOrigin
          DomainName: !GetAtt ApplicationLoadBalancer.DNSName
          VpcOriginConfig:
            OriginKeepaliveTimeout: 60
            OriginReadTimeout: 60
            VpcOriginId: !GetAtt CloudFrontVpcOrigin.Id
        Enabled: true
        DefaultCacheBehavior:
          TargetOriginId: AlbOrigin
          CachePolicyId: 83da9c7e-98b4-4e11-a168-04f0df8e2c65
          OriginRequestPolicyId: 216adef6-5c7f-47e4-b989-5492eafa07d3
          ViewerProtocolPolicy: https-only
```

VPC Origins tham chiếu đến Application Load Balancer (ALB) nội bộ và chỉ hỗ trợ giao thức HTTPS.

```yaml
########### Cloudfront VPC Origin ###############
  CloudFrontVpcOrigin:
    Type: AWS::CloudFront::VpcOrigin
    Properties:
      VpcOriginEndpointConfig:
          Arn: !Ref ApplicationLoadBalancer
          Name: !Sub vpc-origin-${AWS::StackName}
          OriginProtocolPolicy: https-only
          OriginSSLProtocols: 
          - TLSv1.2
```

Khi VPC Origins được khởi tạo, hàm Lambda của tài nguyên tùy chỉnh (custom resource Lambda function) sẽ thêm một quy tắc inbound vào nhóm bảo mật (security group) của CloudFront VPC Origin, nhằm chỉ cho phép lưu lượng truy cập đến từ CloudFront prefix list trong Region được chọn.

```python
ec2_client.authorize_security_group_ingress(
            GroupId=cloudfront_sg_id,
            IpPermissions=[
                {
                    'IpProtocol': 'tcp',  
                    'FromPort': 443,      
                    'ToPort': 443,        
                    'PrefixListIds': [{'PrefixListId': cloudfront_prefix_id}]
                }
            ]
        )
```

#### **Bước 2: Tạo Application Load Balancer (ALB)**

Application Load Balancer (ALB) nội bộ được cấu hình với một HTTPS listener sử dụng chứng chỉ SSL do người dùng cung cấp. Cấu hình này giúp duy trì mã hóa lưu lượng truy cập giữa CloudFront và ALB, đảm bảo tính bảo mật của dữ liệu trong quá trình truyền tải.

```yaml
########### ALB Listener ###########  
  ALBListener:
    Type: AWS::ElasticLoadBalancingV2::Listener
    Properties:
      DefaultActions:
        - Type: forward
          TargetGroupArn: !Ref ALBTargetGroup
      LoadBalancerArn: !Ref ApplicationLoadBalancer
      Port: '443'
      Protocol: HTTPS
      SslPolicy: ELBSecurityPolicy-TLS-1-2-2017-01
      Certificates:
        - CertificateArn: !Ref ALBCertificateARN
```

Nhóm target (target group) của Application Load Balancer (ALB) được trỏ đến các địa chỉ IP của VPC endpoint của execute-api. Các địa chỉ IP này được lấy tự động thông qua một hàm Lambda của tài nguyên tùy chỉnh (custom resource Lambda function).

```yaml
########### ALB Target Group ###########
  ALBTargetGroup:
    Type: AWS::ElasticLoadBalancingV2::TargetGroup
    Properties:
      Port: 443
      Name: !Sub TargetGroup-${AWS::StackName}
      Protocol: HTTPS
      VpcId: !Ref VPCId
      Targets:
        - Id: !GetAtt GetPrivateIPs.IP0
          Port: 443
        - Id: !GetAtt GetPrivateIPs.IP1
          Port: 443
      TargetType: ip
      Matcher:
        HttpCode: '200,403'
```

Hàm Lambda của tài nguyên tùy chỉnh (custom resource Lambda function) sẽ lấy các địa chỉ IP riêng tư (private IPs) dựa trên các ID của network interface được chỉ định, bằng cách sử dụng EC2 client. Sau đó, hàm này trả về một từ điển (dictionary) với các khóa (key) là IP0 và IP1, tương ứng với các giá trị là các địa chỉ IP riêng tư đó.

```python
def fetch_interface_ips(network_interface_ids):
    """
    Fetch private IPs for given network interface IDs using ec2 client
    Returns a dictionary with keys IP0, IP1, etc. and values as the private IPs
    """
    responseData = {}
    
    # Use describe_network_interfaces instead of the resource approach
    response = ec2_client.describe_network_interfaces(
        NetworkInterfaceIds=network_interface_ids
    )
    
    for index, interface in enumerate(response['NetworkInterfaces']):
        responseData[f'IP{index}'] = interface['PrivateIpAddress']
    
    return responseData
```

Bên cạnh đó, hàm Lambda sẽ thêm một quy tắc inbound vào nhóm bảo mật (security group) của ALB nội bộ, cho phép lưu lượng truy cập từ nhóm bảo mật của VPC Origin.

```python
ec2_client.authorize_security_group_ingress(  
            GroupId=security_group_id,  
            IpPermissions=[  
                {  
                    'IpProtocol': 'tcp',    
                    'FromPort': 443,       
                    'ToPort': 443,    
                    'UserIdGroupPairs': [{'GroupId': cloudfront_sg_id}]  
                }  
            ]  
        )
```

#### **Bước 3: Tạo VPC endpoint cho Private API Gateway**

VPC Endpoint của execute-api được cấu hình để định tuyến lưu lượng từ ALB nội bộ đến Private API Gateway. Chỉ có VPC Endpoint mới có khả năng phân giải các endpoint riêng tư (private endpoints) và định tuyến lưu lượng một cách an toàn.

```yaml
########### execute-api VPC Endpoint ###########  
  ExecuteApiVpcEndpoint:  
    Type: AWS::EC2::VPCEndpoint  
    Properties:  
      ServiceName: !Sub "com.amazonaws.${AWS::Region}.execute-api"  
      VpcId: !Ref VPCId  
      SubnetIds: !Ref PrivateSubnets  
      VpcEndpointType: Interface  
      PrivateDnsEnabled: true  
      SecurityGroupIds:  
        - !Ref VpcEndpointSG 
```

#### **Bước 4: Tạo Resource Policy cho Private API Gateway**

Resource Policy được thiết lập trên Private API Gateway chỉ cho phép lưu lượng truy cập đến từ VPC endpoint nằm bên trong VPC do người dùng định nghĩa.

```yaml
x-amazon-apigateway-policy:  
          Version: "2012-10-17"  
          Statement:  
          - Effect: "Allow"  
            Principal: "*"  
            Action: "execute-api:Invoke"  
            Resource: "execute-api:/*"  
            Condition:  
              StringEquals:  
                aws:sourceVpce:   
                - !Ref ExecuteApiVpcEndpoint
```

### **Kiểm thử**

Hãy lấy URL của CloudFront từ mục Outputs trong stack đã được triển khai, sau đó kiểm tra hoạt động của nó bằng cách sử dụng lệnh curl hoặc trình duyệt web của bạn.

```bash
curl https://{your custom domain name}   
{"message": "Hello from API GW"}
```

### **Kết luận**

Bài viết này minh họa cách bạn có thể thiết lập một kiến trúc bảo mật để truy cập vào Private REST API Gateway thông qua Private ALB, với Amazon CloudFront đóng vai trò là điểm truy cập (entry point) cho ứng dụng của bạn. Giải pháp này sử dụng tính năng CloudFront VPC Origins — một khả năng mạnh mẽ cho phép bạn tích hợp trực tiếp CloudFront với các tài nguyên được lưu trữ trong Amazon VPC của mình. Bạn có thể triển khai kiến trúc này để tăng cường đáng kể mức độ bảo mật của ứng dụng, bằng cách giới hạn quyền truy cập vào các dịch vụ backend và giảm thiểu bề mặt tấn công tiềm năng. Cách tiếp cận này cung cấp cho bạn một phương pháp mạnh mẽ và đáng tin cậy để bảo vệ ứng dụng khỏi truy cập trái phép, đồng thời vẫn duy trì hiệu năng cao và khả năng sẵn sàng toàn cầu thông qua mạng phân phối nội dung CloudFront.
