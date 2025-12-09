---
title : "Blog 3"
date :  2025-09-10 
weight : 3
chapter : false
pre : " <b> 3.3 </b> "
---

[**AWS Compute Blog**](https://aws.amazon.com/blogs/compute/)

## **Tăng tốc quá trình phát triển serverless cục bộ với console đến IDE và remote debugging cho AWS Lambda**

by Brian Krygsman and Shridhar Pandey |  on 09 SEP 2025 |   in [AWS Lambda](https://aws.amazon.com/blogs/compute/category/compute/aws-lambda/), [Best Practices](https://aws.amazon.com/blogs/compute/category/post-types/best-practices/), [Developer Tools](https://aws.amazon.com/blogs/compute/category/developer-tools/), [Intermediate (200)](https://aws.amazon.com/blogs/compute/category/learning-levels/intermediate-200/) |  [Permalink](https://aws.amazon.com/blogs/compute/accelerating-local-serverless-development-with-console-to-ide-and-remote-debugging-for-aws-lambda/) |   [Share](https://aws.amazon.com/vi/blogs/compute/accelerating-local-serverless-development-with-console-to-ide-and-remote-debugging-for-aws-lambda/#)

Trải nghiệm phát triển thuận tiện là một yếu tố quan trọng trong việc xây dựng các ứng dụng serverless một cách hiệu quả, dù bạn đang tạo một automation script hay phát triển một ứng dụng doanh nghiệp phức tạp. Mặc dù **AWS Lambda** đã làm thay đổi cách thức phát triển ứng dụng hiện đại trên nền tảng đám mây thông qua mô hình serverless computing, các developer vẫn dành phần lớn thời gian làm việc trong môi trường cục bộ của họ. Họ phụ thuộc vào các IDE, công cụ debugging, testing framework quen thuộc, và quy trình làm việc đã được thiết lập trong tổ chức để xây dựng các ứng dụng sẵn sàng triển khai vào môi trường production.

Bài viết này đề cập đến một số cải tiến gần đây nhằm nâng cao trải nghiệm phát triển cục bộ. Hai tính năng mới của Lambda — đó là **console to IDE và remote debugging** — giúp thu hẹp hơn nữa khoảng cách giữa phát triển trên đám mây và phát triển cục bộ, cho phép bạn tận dụng toàn bộ sức mạnh của các công cụ cục bộ trong khi vẫn làm việc với các Lambda function trên đám mây.

### **Tổng quan**

Phát triển serverless với Lambda bao gồm cả môi trường cloud và local, mỗi môi trường đều có những ưu điểm riêng. Trong khi Lambda console cung cấp khả năng triển khai và tạo nguyên mẫu nhanh chóng, thì phát triển cục bộ mang lại chiều sâu và tính linh hoạt cần thiết cho quy trình phát triển ứng dụng phức tạp — bao gồm integration testing, triển khai lên các môi trường dùng chung, CI/CD pipeline, và khả năng cộng tác với các thành viên khác trong nhóm. Trải nghiệm phát triển cục bộ bao gồm các tool, workflow, và practice mà các developer sử dụng trên thiết bị của họ để xây dựng và duy trì ứng dụng. Một trải nghiệm phát triển cục bộ trực quan giúp nhóm phát triển ứng dụng đạt được năng suất cao, đảm bảo chất lượng mã nguồn và tự tin triển khai các thay đổi lên môi trường production.

### **Những cải tiến gần đây trong trải nghiệm phát triển serverless cục bộ**

Các workflow phát triển cục bộ có thể được xem như hai vòng lặp riêng biệt nhưng có mối liên kết chặt chẽ: vòng lặp bên trong bao gồm việc viết, kiểm thử và debug mã cục bộ; và vòng lặp bên ngoài mở rộng đến quá trình triển khai lên cloud, integration testing, release pipeline, và monitoring, như được minh họa trong hình dưới đây. Đối với các ứng dụng serverless, các developer mong muốn nhận được phản hồi ngay lập tức trong vòng lặp bên trong, khi họ lặp lại quá trình chỉnh sửa mã function và kiểm thử khả năng tích hợp với các AWS service. AWS đã không ngừng cải thiện trải nghiệm phát triển cục bộ cho các developer xây dựng trên Lambda, tập trung vào việc tăng tốc vòng lặp bên trong — nơi các developer dành phần lớn thời gian làm việc.

![Inner and Outer Loop](/images/translated-blogs/blog3/pic1.png)

Theo **2024 Stack Overflow Developer Survey**, **Visual Studio Code** (VS Code) là IDE phổ biến nhất trong giới developer. **Trải nghiệm IDE cục bộ** được cải tiến giúp các developer có thể code, test, debug, và deploy các ứng dụng serverless dựa trên Lambda một cách hiệu quả hơn ngay trong VS Code. Tính năng này giới thiệu Application Builder interface, giúp hợp lý hóa toàn bộ workflow phát triển — từ khâu thiết lập đến triển khai — với các tính năng như guided walkthrough cho việc cài đặt môi trường, các sample application được cấu hình sẵn, build setting management, và khả năng local debugging được cải thiện. Nhờ đó, các developer không còn cần phải chuyển đổi qua lại giữa nhiều giao diện khác nhau. Trải nghiệm này cũng được tích hợp với **AWS Infrastructure Composer**, cho phép xây dựng ứng dụng trực quan trực tiếp trong VS Code, đồng thời cung cấp các quick-action button cho các tác vụ phổ biến như build, deploy, và invoke function — cả ở môi trường cục bộ lẫn trên cloud.

![Guided Walkthrough in VS Code IDE](/images/translated-blogs/blog3/pic2.png)

Với **thư viện pattern sẵn sàng sử dụng phong phú của Serverless Land có thể truy cập trực tiếp trong VS Code**, bạn giờ đây có thể duyệt, tìm kiếm và áp dụng một bộ sưu tập các serverless pattern được chọn lọc và xây dựng sẵn mà không cần rời khỏi IDE. Sự tích hợp này giúp việc áp dụng các architecture đã được kiểm chứng và AWS best practice trở nên dễ dàng hơn trong quá trình xây dựng ứng dụng serverless. Tính năng hỗ trợ **Amazon CloudWatch Logs Live Tail cho Lambda function trong VS Code** mang đến khả năng log streaming và analytics theo thời gian thực trực tiếp trong IDE, cho phép bạn theo dõi và xử lý sự cố cho các Lambda function mà không cần chuyển đổi ngữ cảnh làm việc. Dù bạn đang testing một tính năng mới hay debugging một vấn đề, giờ đây bạn có thể thấy ngay tác động tức thì của các thay đổi trong mã nguồn mà không cần rời khỏi IDE.

### **Từ Console đến IDE**

Trong suốt thập kỷ qua, **Lambda console** đã giúp các developer nhanh chóng bắt đầu với việc viết Lambda function, cho phép họ lặp lại nhanh chóng quá trình thay đổi mã, kiểm thử và triển khai các function của mình. Trải nghiệm console IDE đã có một đợt cải tiến lớn về khả năng sử dụng vào năm 2024, bao gồm cả việc giới thiệu **Amazon Q Developer trong Lambda console**.

Khi các ứng dụng ngày càng trở nên phức tạp, các developer thường cần refactor mã, thêm logic phức tạp, bao gồm các utility library làm dependency, hoặc xử lý các edge case trong Lambda function của họ. Ví dụ bao gồm việc sử dụng các external library cho các phép tính thời gian phức tạp hoặc thêm các module để thực hiện caller-specific validation. Điều này có thể khiến các function trở nên quá cồng kềnh để quản lý trực tiếp trong console.

Các developer cũng có thể muốn đưa function của họ vào software development lifecycle (SDLC) bao gồm test framework, công cụ security scanning, **infrastructure as code** (IaC) template, hoặc CI/CD pipeline. Điều này có thể yêu cầu họ sử dụng version control để cộng tác trong nhóm, hoặc phát triển cùng AI agent được **điều khiển bởi các quy tắc tùy chỉnh**.

Trước đây, việc thiết lập như vậy đòi hỏi phải cấu hình thủ công môi trường phát triển cục bộ, bao gồm IDE, language runtime, và build/package toolchain. Sau đó, bạn cần tải xuống function code, configuration, và integration setting, rồi sao chép chúng vào IDE. Tiếp theo, bạn còn phải tạo IaC template cần thiết bằng **AWS Serverless Application Model (AWS SAM)**. Chỉ sau đó, bạn mới có thể deploy lên cloud để xác thực tính chính xác của mã và cấu hình, rồi tiếp tục workflow phát triển.

Tính năng **Lambda console to IDE** mới cho phép chuyển đổi liền mạch từ chu trình code/test trên cloud sang môi trường cục bộ, cho phép bạn tải xuống function code và configuration vào VS Code IDE cục bộ chỉ với một cú nhấp chuột. Từ đó, bạn có thể dễ dàng thêm dependency và commit code vào source control. Hơn nữa, bạn có thể sync ngược trở lại cloud để deploy, hoặc xuất toàn bộ AWS SAM template với tính năng "Convert to SAM", và tiếp tục quản lý function của mình như thể bạn đã bắt đầu phát triển cục bộ từ đầu. Console to IDE cũng hướng dẫn bạn trong quá trình thiết lập IDE trên thiết bị cục bộ (nếu bạn chưa có), cùng với các cấu hình cần thiết khác. Các hình minh họa dưới đây cho thấy một function được mở trong Lambda console và sau đó trong VS Code IDE cục bộ.

![Lambda Function in Console](/images/translated-blogs/blog3/pic3.png)

![Lambda Function in Local IDE](/images/translated-blogs/blog3/pic4.png)

Bằng cách giúp việc chuyển đổi giữa vòng lặp phát triển bên trong (inner loop) trên cloud và môi trường phát triển cục bộ trở nên dễ dàng, tính năng console to IDE cho phép bạn nhanh chóng mở rộng một ý tưởng từ proof-of-concept thành một serverless application hoàn chỉnh. Hãy truy cập **Lambda documentation** để tìm hiểu thêm chi tiết.

### **Gỡ lỗi từ xa**

Các developer xây dựng serverless applications với Lambda thường cần kiểm thử và gỡ lỗi cho các tích hợp xuyên dịch vụ (cross-service integrations). Mặc dù các local debugging tools cung cấp những khả năng hữu ích, chúng không thể hoàn toàn tái tạo Lambda runtime environment và các tương tác của nó với những AWS services khác, nhất là khi liên quan đến Amazon Virtual Private Cloud (VPC) resources và **AWS Identity and Access Management** (IAM) permissions. Do đó, các developer thường phải dựa vào print statements và verbose logging, và trong những kịch bản phức tạp họ phải deploy function nhiều lần để chẩn đoán và khắc phục sự cố. Quy trình này làm kéo dài chu kỳ phát triển, đặc biệt khi xử lý các vấn đề chỉ xuất hiện trong production environment. Các developer mong muốn có thể sử dụng các công cụ phát triển cục bộ nâng cao như debuggers để điều tra các vấn đề với mã đang chạy trong Lambda functions được deployed trên cloud.

**Tính năng remote debugging mới của Lambda** giờ cho phép bạn debug các function đang chạy trên cloud trực tiếp từ VS Code IDE cục bộ bằng cách dùng extension **AWS Toolkit**. Bạn có thể gỡ lỗi **môi trường thực thi** của function chạy trên cloud trong security context của IAM execution role với quyền truy cập tới các VPC resources đã cấu hình, và theo dõi lần lượt luồng thực thi qua toàn bộ service flows trên cloud.

Để bắt đầu gỡ lỗi, bật **Remote debugging** khi **invoking function** thông qua AWS Toolkit. Cấu hình đường dẫn mã cục bộ (local code path) và payload, sau đó chọn **Remote Invoke**. AWS Toolkit sẽ tự động thêm một AWS-managed debugging **Lambda layer** vào function của bạn, mở rộng timeout, publish một temporary **version**, rồi hoàn nguyên thay đổi cấu hình. AWS Toolkit sau đó sẽ invoke phiên bản debug đã được publish. Khi đó bạn có thể bắt đầu gỡ lỗi. Tính năng này thiết lập một kết nối bảo mật giữa trình gỡ lỗi cục bộ và function đang chạy trên cloud bằng **AWS IoT Secure Tunneling**. Khi debug session kết thúc, Lambda sẽ tự động xóa temporary function version. Bạn có thể **kết thúc debug session một cách tường minh**; nếu không, phiên làm việc sẽ kết thúc tự động sau 60 seconds of inactivity hoặc khi đạt Lambda function timeout.

Hình minh họa sau cho thấy việc đặt một breakpoint trong VS Code IDE trong một phiên remote debugging sẽ tạm dừng việc thực thi, cho phép bạn kiểm tra dữ liệu mà function trên cloud được gọi với (cùng các biến của function). Bạn có thể tiếp tục bước theo từng dòng (step forward line-by-line) từ điểm này để theo dõi tiến trình thực thi của function.

![Remote Debugging in VS Code](/images/translated-blogs/blog3/pic5.png)

Tất cả những điều này có nghĩa là bạn không còn cần phải thiết lập các local emulator để mô phỏng hành vi của cloud, quản lý các test framework phức tạp, hay liên tục thu thập các log tốn kém ở mức TRACE-level chỉ để hiểu cách mã của bạn được thực thi. Debugger của bạn có thể hiển thị chính xác các invocation parameter (chẳng hạn như event và **context**) khi chúng đến function handler. Bạn có thể step through để quan sát cách function hoạt động với các đầu vào khác nhau và kiểm tra giá trị của các biến trong suốt quá trình thực thi. Vì mã của bạn đang chạy trên cloud, bạn thậm chí có thể xem cách IAM execution role của function ảnh hưởng đến hành vi của nó. Trong khi step through, bạn có thể thấy ngay khi một AWS SDK service call thất bại do thiếu quyền truy cập (permissions).

Hơn nữa, bạn có thể kết hợp tính năng này với console to IDE đã được mô tả trước đó trong bài viết. Khi bạn đã download function và scaffold local environment của mình thông qua console to IDE, bạn có thể debug function khi nó chạy trên cloud bằng remote debugging. Điều này mang lại khả năng quan sát sâu hơn vào Lambda developer experience, giúp bạn dễ dàng phát hiện sự cố, nhanh chóng sửa lỗi và triển khai các tính năng mới một cách hiệu quả. Hãy làm theo các bước trong **documentation** để bắt đầu sử dụng.

### **Best practices**

Mặc dù trải nghiệm phát triển được cải thiện giúp bạn tăng tốc trong việc xây dựng serverless application bằng Lambda, bạn vẫn nên tích hợp các **best practice do AWS khuyến nghị** vào application development workflow của mình.

Đối với các function lớn hoặc phức tạp, hãy refactor code theo chuẩn ngôn ngữ lập trình để cả developer và AI agent có thể dễ dàng hiểu và bảo trì hơn. Ví dụ: di chuyển các business logic phức tạp (chẳng hạn như inventory calculation) ra khỏi function handler và đặt vào một module riêng biệt. Console to IDE cho phép bạn sử dụng các refactoring tool cục bộ để tái cấu trúc mã của function.

Để tách biệt chi phí và giới hạn bảo mật giữa môi trường development và production, bạn nên sử dụng các **AWS environment riêng** cho từng giai đoạn của quy trình phát triển. Bạn có thể dùng console to IDE để tạo AWS SAM template cho ứng dụng của mình với đầy đủ property của function và các AWS resource liên quan, giúp chuẩn hóa quá trình deployment giữa nhiều môi trường khác nhau. Sau đó, bạn có thể tự động hóa việc triển khai template và function code thông qua **CI/CD pipeline**.

Trong giai đoạn phát triển, bạn nên **test function trực tiếp trên cloud** bất cứ khi nào có thể. Remote debugging giúp quá trình kiểm thử này dễ dàng hơn từ môi trường cục bộ, cho phép bạn step through code để xác thực logic và **least-privilege execution permission** của function. Để tối ưu chi phí, hãy tập trung logging vừa đủ để tái tạo các kịch bản gặp lỗi, bao gồm những thông tin ngữ cảnh cần thiết về quá trình thực thi của function, thay vì ghi lại toàn bộ mọi thứ. Điều này cũng giúp giảm lượng log cần phân tích.

Bạn nên tái tạo kịch bản lỗi trong một môi trường mà bạn có thể kiểm soát luồng input và sử dụng remote debugging. Nếu có thể, hãy dùng development environment nơi không có nguồn invoke nào khác. Có một khoảng thời gian ngắn khi remote debugging áp dụng thay đổi cấu hình tạm thời, trong đó các traffic khác đến **$LATEST** có thể gây ra kết quả không mong muốn, chẳng hạn như **cold start** chậm hơn. Theo mặc định, debugger sẽ không khởi tạo khi chạy trên $LATEST. Bạn cũng nên sử dụng **Alias** và **Version** để cố định rõ ràng các môi trường vào đúng phiên bản của function tương ứng, tránh được vấn đề này và mang lại hành vi nhất quán hơn, đồng thời cho phép thực hiện **canary deployment**.

### **Kết luận**

Các cải tiến trong trải nghiệm phát triển cục bộ — bao gồm quy trình gỡ lỗi (debugging workflows) và tích hợp IDE — giúp giảm thiểu việc cấu hình và thiết lập cần thiết để các nhà phát triển có thể xây dựng ứng dụng serverless cục bộ bằng Lambda. Điều này cho phép họ tập trung vào việc phát triển logic nghiệp vụ (business logic). Những cải tiến này cũng cung cấp vòng phản hồi nhanh (rapid feedback loop) cần thiết, đồng thời đảm bảo môi trường cục bộ phản ánh chính xác hành vi trên đám mây.

AWS tiếp tục tối ưu hóa trải nghiệm của nhà phát triển đối với ứng dụng serverless trong các lĩnh vực như kiểm thử cục bộ các tích hợp dịch vụ (local testing of service integrations), quy trình IaC (Infrastructure as Code), khả năng khắc phục sự cố (troubleshooting capabilities), và ứng dụng AI sâu hơn trong quy trình phát triển cục bộ. Tất cả những điều này giúp các nhà phát triển xây dựng ứng dụng serverless hiệu quả hơn và an toàn hơn.

Để bắt đầu với các tính năng mới này, hãy truy cập Lambda Developer Guide để xem hướng dẫn chi tiết và các thực tiễn tốt nhất (best practices). Bạn cũng có thể chia sẻ trải nghiệm và đề xuất của mình thông qua trang GitHub Issues của Lambda để cùng định hình tương lai của trải nghiệm phát triển serverless.

Để tìm hiểu thêm về serverless, hãy ghé thăm **Serverless Land**. Ngoài ra, bạn cũng có thể xem video từ một **AWS Community Builder giới thiệu các tính năng mới nhất**.
