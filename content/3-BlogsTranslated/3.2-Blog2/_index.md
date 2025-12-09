---
title: "From Theory to Practice Using Amazon Q Developer CLI to Create Customized AWS Projects"
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

**From Theory to Practice Using Amazon Q Developer CLI to Create Customized AWS Projects**

By Ifeanyi Otuonye and Favour Ezeugwa | on August 26, 2025 | in [Amazon Q Developer](https://aws.amazon.com/blogs/training-and-certification/category/amazon-q/amazon-q-developer/), [AWS CLI](https://aws.amazon.com/blogs/training-and-certification/category/programing-language/aws-cli/), [AWS Training and Certification](https://aws.amazon.com/blogs/training-and-certification/category/aws-training-and-certification/) | [Permalink](https://aws.amazon.com/blogs/training-and-certification/from-theory-to-practice-using-amazon-q-developer-cli-to-generate-tailored-aws-projects/) | [Share](https://aws.amazon.com/vi/blogs/training-and-certification/from-theory-to-practice-using-amazon-q-developer-cli-to-generate-tailored-aws-projects/ ). 

Do you have in-depth theoretical knowledge of [AWS](https://aws.amazon.com/), perhaps through preparing for [AWS Certification](https://aws.amazon.com/certification/?ams%23interactive-card-vertical%23pattern-data.filter=%257B%2522filters%2522%253A%255B%255D%257D) exams, but find it difficult to translate that knowledge into practical projects during your studies? You are not alone. Many cloud practitioners face a common challenge of how to move from theoretical understanding to practical implementation ideas. What if you had an AI-powered advisor that could not only suggest projects that match your skills and interests, but also provide step-by-step implementation guidance, helping to bridge the gap between existing knowledge and practical experience?

In this article, we will guide you through creating and deploying real-world projects on [Amazon Web Services (AWS)](https://aws.amazon.com/) using [Amazon Q Developer command line interface (CLI)](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/command-line.html). By combining the power of AI and CLI, you can build a personalized project generator that understands your skill level and helps you develop practical AWS solutions to add to your personal portfolio.

We designed this guide for people who are already AWS certified or who have a basic understanding of AWS and want to gain hands-on experience by building their own project portfolio. This includes people who are already AWS certified or who want to strengthen their practical skills. Through strategic prompts and deployment guidance, you will discover how Amazon Q Developer CLI can serve as both an AWS project advisor and a deployment assistant.

**Understanding Amazon Q Developer CLI's Project Creation Capabilities**

Unlike searching through traditional documentation or template repositories, Amazon Q Developer CLI understands context and can generate customized project suggestions based on your skill level and goals. This capability goes beyond concise command suggestions and helps you build a practical learning path that grows with your expertise.

When you interact with Amazon Q Developer CLI, you are using a tool that understands AWS best practices, security considerations, and common deployment patterns. Its real power lies in its ability to provide contextual guidance, explaining not only what to do but also why certain approaches are recommended.

**Prerequisites**

Before you begin, you need the following prerequisites:

1. An AWS account with appropriate permissions in [AWS Identity and Access Management (IAM)](https://aws.amazon.com/iam/), including AmazonS3FullAccess, IAM role permissions, and Amazon Q Developer CLI permissions (bedrock:InvokeModel and bedrock:InvokeModelWithResponseStream).

2. Your local environment should have both [AWS Command Line Interface (AWS CLI)](https://aws.amazon.com/cli/) and Amazon Q Developer CLI installed and configured to authenticate with your AWS account. For installation information, refer to [Installing or updating to the latest version of the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) and [Installing Amazon Q for command line](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/command-line-installing.html). To get familiar with these tools, follow the [AWS CLI Getting Started](https://skillbuilder.aws/learn/HNQT94X934/aws-command-line-interface-aws-cli-getting-started/QHT6C7ZHDA) and [Amazon Q Developer CLI](https://skillbuilder.aws/learn/DH893V2JQ2/amazon-q-developer-command-line-interface-cli/MTYYEVP78D) tutorials in [AWS Skill Builder](https://skillbuilder.aws/). Using [Amazon Q Developer](https://aws.amazon.com/q/developer/) follows a pay-as-you-go model, so monitor your usage through the [AWS Management Console](https://aws.amazon.com/console/) to effectively manage costs. Also, refer to the [Amazon Q Developer pricing](https://aws.amazon.com/q/developer/pricing/) for specific pricing details.

Once setup is complete, you will see the Amazon Q Developer CLI chat interface.

![][image1]

**Creating Effective Project Prompts**

The quality of your project suggestions depends significantly on how you communicate with the Amazon Q Developer CLI. By carefully crafting your prompts, you can tap into specific project ideas that align with your current capabilities and learning goals. For example, if you are an [AWS Certified Cloud Practitioner](https://aws.amazon.com/certification/certified-cloud-practitioner/), Amazon Q Developer CLI can suggest projects that build on the concepts of this certification while also providing hands-on implementation experience.

Here is a practical prompt example for the Amazon Q Developer CLI chat interface:

You are my AWS project advisor with expertise in helping beginners

implement practical AWS solutions. I am an AWS Certified Cloud Practitioner looking to build my first hands-on projects. Please suggest three beginner-friendly projects using Amazon S3 that:

1\. Build upon Cloud Practitioner knowledge

2\. Follow AWS best practices and the Well-Architected Framework

3\. Are free-tier friendly

4\. Have clear learning outcomes

5\. Can be completed within a few hours

For each project suggestion, please include:

\- The main AWS services involved

\- Key learning objectives

\- Estimated time to complete

\- Potential real-world applications

When you send a prompt to the Amazon Q Developer CLI, the response will provide carefully structured suggestions that align with both your certification knowledge and your practical learning needs. From these suggestions, we will focus on the suggested project of deploying a static website hosting, an ideal starting point that combines basic AWS concepts with real-world results.

After submitting the example prompt to the Amazon Q Developer CLI, it provides carefully structured suggestions that are relevant to both your certification knowledge and your practical learning needs. From these suggestions, we will focus on the project idea of ​​deploying a static website with Amazon CloudFront distribution. This beginner-friendly project combines three key AWS services: [Amazon Simple Storage Service (Amazon S3)](https://aws.amazon.com/s3/) for hosting, [Amazon CloudFront](https://aws.amazon.com/cloudfront/) for global content delivery, and the optional [Amazon Route 53](https://aws.amazon.com/route53/) for domain management. With an estimated completion time of 2–3 hours, this is an ideal starting point for combining basic AWS concepts with practical results.

![][image2]**From Project Idea to Implementation Steps**

Moving from idea to implementation requires clear infrastructure definitions. Amazon Q Developer CLI excels at generating precise deployment commands while remaining beginner-friendly. Ask Amazon Q Developer CLI to provide deployment steps using the following prompt:

As my AWS project advisor, help me implement a simple version of the static website hosting solution using Amazon S3 from project 1\.

For each step:

1\. Provide the exact AWS CLI commands needed

2\. Explain the purpose and importance of each command

3\. Include necessary security considerations

4\. Highlight best practices

5\. Mention potential gotchas or common mistakes to avoid

The generated response, including CLI steps and commands, demonstrates how Amazon Q Developer CLI can be a learning tool, illustrating how to properly configure an S3 bucket, set up website hosting, and the necessary permissions. It guides you through each command, explaining how the components work together to create a secure and efficient static website hosting solution.![][image3]

**Deploy and practice live**

While the Amazon Q Developer CLI can automate the execution of commands and manage the deployment process, the real learning comes from performing the steps yourself. Let's deploy the first step from the generated response by creating an S3 bucket using the AWS CLI, as shown in the previous image.

To create your S3 bucket, open a new terminal window. Enter the following command from the Amazon Q Developer CLI-generated step to create an S3 bucket, replacing ***my-name*** with your own to ensure uniqueness:

aws s3 mb s3://my-portfilio-site-2025-my-name \--region us-east-1

After creating the S3 bucket, continue through each remaining deployment step, from enabling static website hosting to the final step of getting the static website endpoint URL. Make sure you understand the purpose of each command. If you get stuck, the Amazon Q Developer CLI will assist you; if you run into problems or need clarification, ask the Amazon Q Developer CLI for help. It will provide troubleshooting guidance, explaining potential causes and solutions. This process of encountering and resolving issues will be an important part of your learning journey. After completing all the remaining steps to deploy the static website and getting the endpoint URL, copy and paste it into your browser to view your live website. If everything goes well,Well done, congratulations on successfully deploying your first AWS project with Amazon Q Developer CLI!

Infrastructure as Code with Amazon Q Developer CLI

Now that you have manually deployed your static website, you can explore other powerful features of Amazon Q Developer CLI, such as creating Infrastructure as Code (IaC).

Ask Amazon Q Developer CLI to generate an [AWS Cloud Development Kit (AWS CDK)](https://aws.amazon.com/cdk/) stack that represents your deployment and provides an explanation of its components:

Create a CDK TypeScript stack for the S3 static website we just built manually.

After generating the code, please explain:

\- The main components of the CDK stack

\- How each component relates to our manual implementation steps

\- Any best practices or optimizations included in the generated code

\- How this CDK implementation enhances our project's maintainability and scalability

The Amazon Q Developer CLI will generate a complete CDK implementation and provide detailed explanations, turning your manual steps into infrastructure as code with additional context. You can use this approach to manage infrastructure versions, ensure consistent deployments across environments, and solidify your understanding of AWS services and IaC principles.

**Building on your success**

After successfully deploying a static website to Amazon S3, you can consider improving its performance and security. A natural enhancement is to add Amazon CloudFront, a content delivery network (CDN) that delivers website content faster to users globally while enhancing security. To learn how to get started with CloudFront, visit [Amazon CloudFront Getting Started](https://skillbuilder.aws/learn/5ER4A2FQNV/amazon-cloudfront-getting-started/ZA4XJ48BP1) in AWS Skill Builder.

The Amazon Q Developer CLI can guide you through this improvement. Use natural language to ask it to explain how to add CloudFront to your existing Amazon S3 static website, and it will provide the necessary steps and commands. This improvement will improve your website performance and introduce important concepts such as CDNs, edge locations, and cache behaviors.

**Clean up your resources**

After completing your static website project, it is important to remove resources that are no longer needed. This practice helps you avoid unnecessary costs and reinforces the cost optimization principles of the Well-Architected Framework. To delete the resources created in this tutorial, you can ask Amazon Q Developer CLI to guide you through the cleanup process using the following prompt:

Provide the commands in the correct order to help me clean up all the AWS resources we created for the static website project, including the S3 bucket, its contents, etc.

Amazon Q Developer CLI will provide you with the appropriate AWS CLI commands to securely delete the resource. Typically, this involves deleting all objects in the S3 bucket first, then deleting the bucket itself. If you have upgraded your project with CloudFront, you will also need to disable and delete the distribution. This practice will be useful as you progress to more complex projects with multiple AWS services and potentially higher costs.

**Integration with AWS Training Resources**

While Amazon Q Developer CLI provides robust project guidance, it works best when combined with the comprehensive learning resources that AWS provides. The hands-on experience from this project complements the training courses available on [AWS Skill Builder.](https://skillbuilder.aws/) For example, the [Introduction to Amazon S3](https://skillbuilder.aws/learn/R54NZHEX5K/introduction-to-amazon-simple-storage-service-s3/SKTY8SPYDX) course provides deeper context on static website hosting capabilities, while the “AWS Command Line Interface Basics” course helps you understand CLI commands better.

Build a learning rhythm that combines project work with Amazon Q Developer CLI and structured AWS training courses. Start with the basics on AWS Skill Builder, implement them using the Amazon Q Developer CLI tutorial, and then reflect on what you’ve built. This approach solidifies your knowledge while creating real-world products for your portfolio.

**Conclusion**

The journey from AWS Certification knowledge to real-world implementation doesn’t have to be difficult. By using the Amazon Q Developer CLI as a project advisor and implementation guide, you’ve discovered a simple approach to building project-based AWS solutions. This approach will help you create portfolio-worthy projects and deepen your understanding of AWS services through hands-on experience. Remember, every AWS expert starts with simple projects like the static website you just deployed following the instructions in this article. As you gain confidence, use the Amazon Q Developer CLI to explore more complex architectures and implementations. The hands-on experience from these projects, combined with the training resourcesAWS, will provide a solid foundation for your learning journey.

**Additional Resources**

To continue your learning journey, explore the following AWS resources:

* [AWS Command Line Interface Basics](https://skillbuilder.aws/learn/VZ6UJAWE63/aws-command-line-interface-cli-basics/BBJTE8CY94)

* [Amazon Q Developer CLI User Guide](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/command-line.html)

* [Amazon S3 Getting Started](https://skillbuilder.aws/learn/H99Y6PR2F7/amazon-s3-getting-started/TCVDGQFEJR)

* [Amazon CloudFront Getting Started](https://skillbuilder.aws/learn/5ER4A2FQNV/amazon-cloudfront-getting-started/ZA4XJ48BP1)

We encourage you to start with the static website project presented in this article. Once you are comfortable, upgrade the project with CloudFront to learn about CDNs. Share your implementations, ask questions in the AWS community forums, and keep building. Your next AWS project is just a prompt away.

**About the Authors**

**Ifeanyi Otuonye**
Ifeanyi Otuonye is a Technical Account Manager and a 10-time AWS Certified professional. As a strategic advisor, he helps customers achieve their business goals with AWS Cloud services. Passionate about education and inspiration, he develops content and resources that make cloud learning accessible, empowering professionals to grow in knowledge, influence, and impact. You can connect with him on [LinkedIn](https://www.linkedin.com/in/ifeanyi-otuonye/).

**Favour Ezeugwa**
Favour Ezeugwa is a Solutions Architect at Amazon Web Services (AWS), where she helps customers design scalable, secure, and cost-effective cloud architectures. With a background in computer information systems and a passion for generative AI and cloud security, Favour has led key projects including the development of AI assistants and serverless applications. She is an advocate for hands-on learning, mentorship, and using technology to create meaningful change.

**Source:[https://aws.amazon.com/en/blogs/training-and-certification/from-theory-to-practice-using-amazon-q-developer-cli-to-generate-tailored-aws-project s/](https://aws.amazon.com/vi/blogs/training-and-certification/from-theory-to-practice-using-amazon-q-developer-cli-to-generate-tailored-aws-projects/)**
