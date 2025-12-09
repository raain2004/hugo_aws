---
title: "Từ lý thuyết đến thực tiễn với việc sử dụng Amazon Q Developer CLI để tạo ra các dự án AWS được tùy chỉnh"
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

 **Từ lý thuyết đến thực tiễn với việc sử dụng Amazon Q Developer CLI để tạo ra các dự án AWS được tùy chỉnh**

 Bởi Ifeanyi Otuonye và Favour Ezeugwa | vào ngày 26 tháng 8 năm 2025 | trong [Amazon Q Developer](https://aws.amazon.com/blogs/training-and-certification/category/amazon-q/amazon-q-developer/), [AWS CLI](https://aws.amazon.com/blogs/training-and-certification/category/programing-language/aws-cli/), [AWS Training and Certification](https://aws.amazon.com/blogs/training-and-certification/category/aws-training-and-certification/) | [Permalink](https://aws.amazon.com/blogs/training-and-certification/from-theory-to-practice-using-amazon-q-developer-cli-to-generate-tailored-aws-projects/) | [Share](https://aws.amazon.com/vi/blogs/training-and-certification/from-theory-to-practice-using-amazon-q-developer-cli-to-generate-tailored-aws-projects/ ).

  Bạn có kiến thức lý thuyết chuyên sâu về [AWS](https://aws.amazon.com/), có thể thông qua việc chuẩn bị cho các kỳ thi [AWS Certification](https://aws.amazon.com/certification/?ams%23interactive-card-vertical%23pattern-data.filter=%257B%2522filters%2522%253A%255B%255D%257D), nhưng lại thấy khó khăn khi chuyển hóa kiến thức đó thành các dự án thực tiễn trong quá trình học? Bạn không đơn độc. Nhiều cloud practitioners gặp phải thách thức chung là làm thế nào để bước từ sự hiểu biết lý thuyết sang những ý tưởng triển khai thực tế. Sẽ ra sao nếu bạn có một AI-powered advisor không chỉ gợi ý các dự án phù hợp với kỹ năng và sở thích của bạn, mà còn cung cấp hướng dẫn triển khai từng bước, giúp thu hẹp khoảng cách giữa kiến thức hiện có và kinh nghiệm thực tiễn?

  Trong bài viết này, chúng tôi sẽ hướng dẫn bạn cách tạo và triển khai các dự án thực tế trên [Amazon Web Services (AWS)](https://aws.amazon.com/) bằng cách sử dụng [Amazon Q Developer command line interface (CLI)](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/command-line.html). Bằng cách kết hợp sức mạnh của AI và CLI, bạn có thể xây dựng một project generator cá nhân hóa, hiểu rõ trình độ kỹ năng của bạn và giúp bạn phát triển các giải pháp AWS thực tiễn để bổ sung vào portfolio cá nhân.

  Chúng tôi thiết kế hướng dẫn này dành cho những người đã có chứng chỉ AWS hoặc những ai có kiến thức cơ bản về AWS và muốn tích lũy kinh nghiệm thực hành bằng cách xây dựng portfolio dự án của riêng mình. Điều này bao gồm những người đã được chứng nhận AWS hoặc những người muốn củng cố kỹ năng thực hành. Thông qua các prompt có chiến lược và hướng dẫn triển khai, bạn sẽ khám phá cách Amazon Q Developer CLI có thể đóng vai trò vừa là AWS project advisor vừa là trợ lý triển khai.

  **Hiểu về khả năng tạo dự án của Amazon Q Developer CLI**

  Khác với việc tìm kiếm trong tài liệu truyền thống hoặc các kho template, Amazon Q Developer CLI hiểu ngữ cảnh và có thể tạo ra các gợi ý dự án tùy chỉnh dựa trên trình độ kỹ năng và mục tiêu của bạn. Khả năng này không chỉ dừng lại ở các gợi ý lệnh ngắn gọn mà còn giúp bạn xây dựng một lộ trình học tập thực tiễn, phát triển cùng với chuyên môn của bạn.

  Khi tương tác với Amazon Q Developer CLI, bạn đang sử dụng một công cụ hiểu rõ các best practices của AWS, các yếu tố bảo mật và các mô hình triển khai phổ biến. Sức mạnh thực sự của nó nằm ở khả năng cung cấp hướng dẫn theo ngữ cảnh, giải thích không chỉ những gì cần làm mà còn lý do tại sao các phương pháp nhất định được khuyến nghị.

  **Các điều kiện tiên quyết**

  Trước khi bắt đầu, bạn cần có các điều kiện tiên quyết sau:

1.   Một tài khoản AWS với các quyền phù hợp trong [AWS Identity and Access Management (IAM)](https://aws.amazon.com/iam/), bao gồm AmazonS3FullAccess, quyền IAM role và quyền Amazon Q Developer CLI (bedrock:InvokeModel và bedrock:InvokeModelWithResponseStream).

2.   Môi trường cục bộ của bạn nên được cài đặt cả [AWS Command Line Interface (AWS CLI)](https://aws.amazon.com/cli/) và Amazon Q Developer CLI, đồng thời được cấu hình để xác thực với tài khoản AWS của bạn. Để biết thông tin về cách cài đặt, hãy tham khảo [Installing or updating to the latest version of the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) và [Installing Amazon Q for command line](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/command-line-installing.html). Để làm quen với các công cụ này, hãy theo dõi hướng dẫn [AWS CLI Getting Started](https://skillbuilder.aws/learn/HNQT94X934/aws-command-line-interface-aws-cli-getting-started/QHT6C7ZHDA) và [Amazon Q Developer CLI](https://skillbuilder.aws/learn/DH893V2JQ2/amazon-q-developer-command-line-interface-cli/MTYYEVP78D) trong [AWS Skill Builder](https://skillbuilder.aws/). Việc sử dụng [Amazon Q Developer](https://aws.amazon.com/q/developer/) tuân theo mô hình trả phí theo mức sử dụng (pay-as-you-go), vì vậy hãy theo dõi mức sử dụng của bạn qua [AWS Management Console](https://aws.amazon.com/console/) để quản lý chi phí hiệu quả. Đồng thời, tham khảo tài liệu [Amazon Q Developer pricing](https://aws.amazon.com/q/developer/pricing/) để biết chi tiết chi phí cụ thể.

  Sau khi thiết lập thành công, bạn sẽ thấy giao diện chat của Amazon Q Developer CLI.

![][image1]

  **Tạo các prompt dự án hiệu quả**

  Chất lượng các gợi ý dự án phụ thuộc đáng kể vào cách bạn giao tiếp với Amazon Q Developer CLI. Thông qua việc tạo prompt cẩn thận, bạn có thể khai thác các ý tưởng dự án cụ thể, phù hợp với khả năng hiện tại và mục tiêu học tập của mình. Ví dụ, nếu bạn là một [AWS Certified Cloud Practitioner](https://aws.amazon.com/certification/certified-cloud-practitioner/), Amazon Q Developer CLI có thể gợi ý các dự án xây dựng dựa trên các khái niệm của chứng chỉ này đồng thời mang đến kinh nghiệm triển khai thực hành.

  Dưới đây là một ví dụ prompt thực tiễn cho giao diện chat của Amazon Q Developer CLI:

You are my AWS project advisor with expertise in helping beginners 

implement practical AWS solutions. I am an AWS Certified Cloud Practitioner looking to build my first hands-on projects. Please suggest three beginner-friendly projects using Amazon S3 that: 

1\. Build upon Cloud Practitioner knowledge 

2\. Follow AWS best practices and Well-Architected Framework 

3\. Are free-tier friendly 

4\. Have clear learning outcomes 

5\. Can be completed within a few hours

For each project suggestion, please include:

 

\- The main AWS services involved 

\- Key learning objectives 

\- Estimated time to complete 

\- Potential real-world applications

Khi bạn gửi prompt tới Amazon Q Developer CLI, phản hồi sẽ cung cấp các gợi ý được cấu trúc cẩn thận, phù hợp với cả kiến thức chứng chỉ của bạn lẫn nhu cầu học tập thực hành. Từ những gợi ý này, chúng ta sẽ tập trung vào dự án được đề xuất là triển khai một static website hosting, một điểm khởi đầu lý tưởng kết hợp các khái niệm AWS cơ bản với kết quả thực tế.

Sau khi gửi prompt ví dụ tới Amazon Q Developer CLI, nó sẽ cung cấp các gợi ý được cấu trúc cẩn thận, phù hợp với cả kiến thức chứng chỉ của bạn và nhu cầu học tập thực hành. Từ những gợi ý này, chúng ta sẽ tập trung vào ý tưởng dự án là triển khai một static website với Amazon CloudFront distribution. Dự án thân thiện với người mới này kết hợp ba dịch vụ AWS chính: [Amazon Simple Storage Service (Amazon S3)](https://aws.amazon.com/s3/) để hosting, [Amazon CloudFront](https://aws.amazon.com/cloudfront/) để phân phối nội dung toàn cầu, và tùy chọn [Amazon Route 53](https://aws.amazon.com/route53/) để quản lý domain. Với thời gian hoàn thành ước tính 2–3 giờ, đây là điểm khởi đầu lý tưởng kết hợp các khái niệm cơ bản của AWS với kết quả thực tế.

  ![][image2]**Từ ý tưởng dự án đến các bước triển khai**

  Việc chuyển từ ý tưởng sang triển khai đòi hỏi các định nghĩa hạ tầng rõ ràng. Amazon Q Developer CLI nổi bật trong việc tạo ra các lệnh triển khai chính xác đồng thời vẫn thân thiện với người mới. Hãy yêu cầu Amazon Q Developer CLI cung cấp các bước triển khai bằng prompt sau:

As my AWS project advisor, help me implement a simple version of the static website hosting solution using Amazon S3 from project 1\. 

For each step:

1\. Provide the exact AWS CLI commands needed

2\. Explain the purpose and importance of each command

3\. Include necessary security considerations

4\. Highlight best practices

5\. Mention potential gotchas or common mistakes to avoid

Phản hồi được tạo ra, bao gồm các bước và lệnh CLI, thể hiện cách Amazon Q Developer CLI có thể trở thành công cụ học tập, minh họa cách cấu hình S3 bucket đúng, thiết lập website hosting và các quyền cần thiết. Nó hướng dẫn bạn từng lệnh, giải thích cách các thành phần phối hợp với nhau để tạo ra một giải pháp static website hosting vừa bảo mật vừa hoạt động hiệu quả.![][image3]

**Triển khai và thực hành trực tiếp**

Mặc dù Amazon Q Developer CLI có thể tự động thực thi các lệnh và quản lý quy trình triển khai, việc học thực sự đến từ việc bạn tự thực hiện các bước. Hãy triển khai bước đầu tiên từ phản hồi được tạo ra bằng cách tạo một S3 bucket sử dụng AWS CLI, như minh họa trong hình trước.

Để tạo S3 bucket của bạn, mở một cửa sổ terminal mới. Nhập lệnh sau từ bước được tạo bởi Amazon Q Developer CLI để tạo S3 bucket, thay thế ***my-name*** trong tên bucket bằng tên của bạn để đảm bảo tính duy nhất:

aws s3 mb s3://my-portfilio-site-2025-my-name \--region us-east-1

Sau khi tạo S3 bucket, tiếp tục thực hiện từng bước triển khai còn lại, từ việc bật static website hosting đến bước cuối cùng là lấy URL endpoint của website tĩnh. Hãy đảm bảo bạn hiểu mục đích của từng lệnh. Khi gặp khó khăn, Amazon Q Developer CLI sẽ hỗ trợ bạn; nếu gặp vấn đề hoặc cần làm rõ, hãy yêu cầu Amazon Q Developer CLI trợ giúp. Nó sẽ cung cấp hướng dẫn khắc phục, giải thích nguyên nhân tiềm ẩn và các giải pháp. Quá trình gặp và giải quyết vấn đề này sẽ là một phần quan trọng trong hành trình học tập của bạn. Sau khi hoàn thành tất cả các bước còn lại để triển khai static website và lấy URL endpoint, hãy sao chép và dán vào trình duyệt để xem website trực tiếp của bạn. Nếu mọi việc diễn ra suôn sẻ, xin chúc mừng bạn đã triển khai thành công dự án AWS đầu tiên với Amazon Q Developer CLI\!

  Hạ tầng dưới dạng mã với Amazon Q Developer CLI

  Bây giờ, sau khi bạn đã triển khai thủ công static website, bạn có thể khám phá các tính năng mạnh mẽ khác của Amazon Q Developer CLI, chẳng hạn như tạo hạ tầng dưới dạng mã (Infrastructure as Code – IaC).

  Hãy yêu cầu Amazon Q Developer CLI tạo một [AWS Cloud Development Kit (AWS CDK)](https://aws.amazon.com/cdk/) stack đại diện cho việc triển khai của bạn và cung cấp giải thích về các thành phần của nó:

Create a CDK TypeScript stack for the S3 static website we just built manually.

After generating the code, please explain:

\- The main components of the CDK stack

\- How each component relates to our manual implementation steps

\- Any best practices or optimizations included in the generated code

\- How this CDK implementation enhances our project's maintainability and scalability

  Amazon Q Developer CLI sẽ tạo ra một triển khai CDK hoàn chỉnh và cung cấp giải thích chi tiết, biến các bước thủ công của bạn thành hạ tầng dưới dạng mã với bối cảnh bổ sung. Bạn có thể sử dụng cách tiếp cận này để quản lý phiên bản hạ tầng, đảm bảo triển khai nhất quán giữa các môi trường và củng cố hiểu biết về các dịch vụ AWS cũng như các nguyên tắc IaC.

  **Building on your success**

  Sau khi triển khai thành công static website trên Amazon S3, bạn có thể cân nhắc cải thiện hiệu suất và bảo mật của nó. Một cải tiến tự nhiên là thêm Amazon CloudFront, một content delivery network (CDN) giúp phân phối nội dung website nhanh hơn tới người dùng trên toàn cầu đồng thời tăng cường bảo mật. Để tìm hiểu cách bắt đầu với CloudFront, hãy truy cập [Amazon CloudFront Getting Started](https://skillbuilder.aws/learn/5ER4A2FQNV/amazon-cloudfront-getting-started/ZA4XJ48BP1) trong AWS Skill Builder.

  Amazon Q Developer CLI có thể hướng dẫn bạn trong quá trình cải tiến này. Sử dụng ngôn ngữ tự nhiên để yêu cầu nó giải thích cách thêm CloudFront vào static website Amazon S3 hiện có của bạn, và nó sẽ cung cấp các bước và lệnh cần thiết. Cải tiến này sẽ nâng cao hiệu suất website của bạn và giới thiệu các khái niệm quan trọng như CDNs, edge locations và cache behaviors.

  **Dọn dẹp tài nguyên của bạn**

  Sau khi hoàn thành dự án static website, việc xóa những tài nguyên không còn cần thiết là rất quan trọng. Thực hành này giúp bạn tránh phát sinh chi phí không cần thiết và củng cố nguyên tắc cost optimization trong Well-Architected Framework. Để xóa các tài nguyên được tạo trong hướng dẫn này, bạn có thể yêu cầu Amazon Q Developer CLI hướng dẫn quá trình dọn dẹp bằng prompt sau:

Provide the commands in the correct order to help me clean up all the AWS resources we created for the static website project, including the S3 bucket, its contents etc.

Amazon Q Developer CLI sẽ cung cấp cho bạn các lệnh AWS CLI phù hợp để xóa tài nguyên một cách an toàn. Thông thường, việc này bao gồm xóa tất cả các object trong S3 bucket trước, sau đó xóa chính bucket. Nếu bạn đã nâng cấp dự án với CloudFront, bạn cũng cần vô hiệu hóa và xóa distribution. Thói quen này sẽ rất hữu ích khi bạn tiến tới các dự án phức tạp hơn với nhiều dịch vụ AWS và chi phí tiềm năng cao hơn.

**Tích hợp với các tài nguyên đào tạo AWS**

Mặc dù Amazon Q Developer CLI cung cấp hướng dẫn dự án mạnh mẽ, nó hoạt động hiệu quả nhất khi kết hợp với các tài nguyên học tập toàn diện mà AWS cung cấp. Kinh nghiệm thực hành từ dự án này bổ trợ cho các khóa đào tạo có sẵn trên [AWS Skill Builder.](https://skillbuilder.aws/) Ví dụ, khóa [Introduction to Amazon S3](https://skillbuilder.aws/learn/R54NZHEX5K/introduction-to-amazon-simple-storage-service-s3/SKTY8SPYDX) cung cấp bối cảnh sâu hơn về khả năng static website hosting, trong khi khóa “AWS Command Line Interface Basics” giúp bạn hiểu rõ các lệnh CLI hơn.

Hãy xây dựng một nhịp học kết hợp giữa công việc dự án với Amazon Q Developer CLI và các khóa đào tạo AWS có cấu trúc. Bắt đầu với các khái niệm cơ bản trên AWS Skill Builder, triển khai chúng bằng hướng dẫn của Amazon Q Developer CLI, sau đó phản ánh lại những gì bạn đã xây dựng. Cách tiếp cận này giúp củng cố kiến thức đồng thời tạo ra các sản phẩm thực tế cho portfolio của bạn.

**Kết luận**

Hành trình từ kiến thức AWS Certification đến triển khai thực tế không nhất thiết phải khó khăn. Bằng cách sử dụng Amazon Q Developer CLI như một cố vấn dự án và hướng dẫn triển khai, bạn đã khám phá ra cách tiếp cận đơn giản để xây dựng các giải pháp AWS dựa trên dự án. Phương pháp này sẽ giúp bạn tạo các dự án xứng đáng đưa vào portfolio và đào sâu hiểu biết về các dịch vụ AWS thông qua kinh nghiệm thực hành. Hãy nhớ rằng, mọi chuyên gia AWS đều bắt đầu với những dự án đơn giản như static website mà bạn vừa triển khai theo hướng dẫn trong bài viết này. Khi bạn tự tin hơn, hãy sử dụng Amazon Q Developer CLI để khám phá các kiến trúc và triển khai phức tạp hơn. Kinh nghiệm thực tiễn từ các dự án này, kết hợp với các tài nguyên đào tạo AWS, sẽ tạo nền tảng vững chắc cho hành trình học tập của bạn.

**Tài nguyên bổ sung**

Để tiếp tục hành trình học tập, hãy khám phá các tài nguyên AWS sau:

* [AWS Command Line Interface Basics](https://skillbuilder.aws/learn/VZ6UJAWE63/aws-command-line-interface-cli-basics/BBJTE8CY94)

* [Amazon Q Developer CLI User Guide](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/command-line.html)

* [Amazon S3 Getting Started](https://skillbuilder.aws/learn/H99Y6PR2F7/amazon-s3-getting-started/TCVDGQFEJR)

* [Amazon CloudFront Getting Started](https://skillbuilder.aws/learn/5ER4A2FQNV/amazon-cloudfront-getting-started/ZA4XJ48BP1)

Chúng tôi khuyến khích bạn bắt đầu với dự án static website được trình bày trong bài viết này. Khi đã quen, hãy nâng cấp dự án với CloudFront để tìm hiểu về CDNs. Chia sẻ các triển khai của bạn, đặt câu hỏi trong các diễn đàn cộng đồng AWS và tiếp tục xây dựng. Dự án AWS tiếp theo của bạn chỉ cách một prompt.

**Về các tác giả**

**Ifeanyi Otuonye**  
Ifeanyi Otuonye là Technical Account Manager và là chuyên gia AWS Certified 10 lần. Với vai trò cố vấn chiến lược, ông giúp khách hàng đạt được mục tiêu kinh doanh với các dịch vụ AWS Cloud. Là một người đam mê giáo dục và truyền cảm hứng, ông phát triển các nội dung và tài nguyên giúp việc học cloud trở nên dễ tiếp cận, trao quyền cho các chuyên gia phát triển kiến thức, ảnh hưởng và tác động. Bạn có thể kết nối với ông trên [LinkedIn](https://www.linkedin.com/in/ifeanyi-otuonye/).

**Favour Ezeugwa**  
Favour Ezeugwa là Solutions Architect tại Amazon Web Services (AWS), nơi cô giúp khách hàng thiết kế các kiến trúc cloud có khả năng mở rộng, bảo mật và tối ưu chi phí. Với nền

tảng hệ thống thông tin máy tính và đam mê về generative AI và bảo mật cloud, Favour đã dẫn dắt các dự án quan trọng bao gồm phát triển trợ lý AI và ứng dụng serverless. Cô là người ủng hộ học tập thực hành, mentorship và sử dụng công nghệ để tạo ra thay đổi ý nghĩa.

**Nguồn:[https://aws.amazon.com/vi/blogs/training-and-certification/from-theory-to-practice-using-amazon-q-developer-cli-to-generate-tailored-aws-projects/](https://aws.amazon.com/vi/blogs/training-and-certification/from-theory-to-practice-using-amazon-q-developer-cli-to-generate-tailored-aws-projects/)**

  

  

  


