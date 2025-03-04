---
layout: article
title: "Getting Started with Amazon Unified Data Studio"
date: 2024-12-10
modify_date: 2024-12-10
excerpt: "Getting Started with Amazon Unified Data Studio"
tags: [AWS, Sagemaker]
mathjax: false
mathjax_autoNumber: false
key: aws-sagemaker-tips
---

One question, people are always asked is **what'is the best tool do i have to learn to have a career in data and AI?**? And the answer is AWS Sagemaker Unified Data Studio.

Sagemaker Unified Data Studio is probably the only tool require to do both your analytical and AI workloads.

In this article, we will walk you through the steps to get started with Amazon Unified Data Studio and give you a high level overview and details aspects of the features you can use to get started.

[![My image alt description](/blog/assets/images/posts-img/unified-studio/01.jpg)](/blog/assets/images/posts-img/unified-studio/01.jpg)

### Settings your account

1. You have the choice between :

   * Creating a unified studio domain
   * Creating an amazon dataZone domain
Let's start from scratch an create one unified studio domain.

2. Once you click on unified studio domain, you have two option:

    [![My image alt description](/blog/assets/images/posts-img/unified-studio/04.jpg)](/blog/assets/images/posts-img/unified-studio/04.jpg)

   * **Quick setup (recommended for exploration)**
   * **Manual setup (recommended for organizations)**

3. We can create a VPC or use an existing one.

    [![My image alt description](/blog/assets/images/posts-img/unified-studio/05.jpg)](/blog/assets/images/posts-img/unified-studio/05.jpg)

4. Once w've setup our VPC (because everything is deploy in a VPC), we can know fill others forms. Amazon also create some roles on your behalf.
   1. For **Data analytics, machine learning, and SQL analytics resources**:These resources will allow users to consume, process, and produce data assets with SQL, AWS Glue, Amazon EMR, Amazon SageMaker, Amazon MWAA, and Amazon Redshift Serverless
   2. For **Generative AI resources Info**: These resources will create a project profile that will allow users to explore, experiment, and collaborate on generative AI application development using the Amazon Bedrock foundation models and tool

    [![My image alt description](/blog/assets/images/posts-img/unified-studio/06_.jpg)](/blog/assets/images/posts-img/unified-studio/06_.jpg)

5. Once you have created your unified studio domain, you can start to use it to explore the data, model and application that you have created.

    [![My image alt description](/blog/assets/images/posts-img/unified-studio/07.jpg)](/blog/assets/images/posts-img/unified-studio/07.jpg)

6. We have an overview of the domain created

    [![My image alt description](/blog/assets/images/posts-img/unified-studio/08.jpg)](/blog/assets/images/posts-img/unified-studio/08.jpg)

    a. **Domain details**: WIth Amazon SageMaker Unified Studio URL, Domain ARB, and Domain metadata.
  
7. Next, we have a configuration with **IAM Identity center** where we can configure SSO credentials.

8. We also have projects profiles. **Project profiles** define the tools and capabilities available in projects in Amazon SageMaker Unified Studio. Use a template below to create a project profile.

   a. **Data analytics and AI/ML model development**: Analyze data and build ML and GenAI models powered by Amazon EMR, AWS Glue, Amazon Athena, Amazon SageMaker AI and Amazon SageMaker Lakehouse.

   b. **Generative AI**: Explore, build, and collaborate on generative AI applications using Amazon Bedrock foundation models and tools.

   c. **SQL analytics**: Use the SQL editor to query data in Amazon SageMaker Lakehouse, Amazon Redshift and Amazon Athena.

9. At users management level, you can:

    [![My image alt description](/blog/assets/images/posts-img/unified-studio/09.jpg)](/blog/assets/images/posts-img/unified-studio/09.jpg)

    a. **Manage users**: Enable access to Amazon SageMaker Unified Studio for users with SSO credentials, or add an IAM user below. By default, this domain supports IAM user credentials.

    b. **Associate account**: You can associate another AWS account.

    c. **Blueprints**: You can leverage some blueprints( AmazonBedrockGenerativeAI blueprints, LakehouseCatalog blueprints; etc...).

    d. **Projects profiles**: As explained earlier, three projects profiles.
        - **Data analytics and AI/ML model development**: Best suit for builders.
        - **Generative AI**: Best Suit for business as well as data scientists who want to play with models.
        - **SQL analytics**: Best suit for business.

    e. **Amazon Bedrock models**: You can request access to some foundations models as soon as those models are part of Amazon Bedrock catalog models.

    f. **connections**: Allow you to connect to external stuff like GitHub, GitLab, etc... and store your code in these version control.

    g. **Amazon Q**: Enable Amazon Q, the generative AI-powered assistant that you can tailor to your business needs.

    h. **Tags**: A tag is a label that you assign to an AWS resource. Each tag consists of a key and an optional value. You can use tags to search and filter your resources or track your AWS costs

As you see Sagemaker Unified Data Studio is a very powerful service who have access to a lot of others AWS services.

Next time we will dep dive into Sagemaker Unified Data Studio portal.
