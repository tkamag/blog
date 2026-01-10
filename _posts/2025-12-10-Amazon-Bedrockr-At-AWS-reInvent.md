---
layout: article
title: "Amazon Bedrock at AWS re:invent 2025"
date: 2025-12-10
modify_date: 2025-12-10
excerpt: "Amazon Bedrock new features"
tags: [AWS, Sagemaker, Bedrock]
mathjax: false
mathjax_autoNumber: false
key: aws-sagemaker-bedrock-opensearch-tips
---

***

[![My image alt description](/blog/assets/images/posts-img/reInvent_2025/01.png)](/blog/assets/images/posts-img/reInvent_2025/01.png)


In response to the rapid rise of **Generative AI** and machine learning workloads, AWS introduced numerous enhancements to Amazon Bedrock at AWS re:Invent 2025. We will examine these announcements in detail and provide clarity on their key aspects.

## A.1

[![My image alt description](/blog/assets/images/posts-img/reInvent_2025/02.png)](/blog/assets/images/posts-img/reInvent_2025/02.png)


At ReInvent 2025, Amazon announced the general availability of an additional 18 fully managed open weight models in Amazon Bedrock from new providers like Google, MiniMax AI, Mistral AI, Moonshot AI, NVIDIA, OpenAI, and Qwen, including the new Mistral Large 3 and Ministral 3 3B, 8B, and 14B models.

<table>
  <tr>
    <th>Model provider</th>
    <th colspan="1">Model name</th>
    <th>Description</th>
    <th>Use cases</th>
  </tr>
  <tr>
    <td rowspan="3">Google</td>
    <td><a href="https://huggingface.co/google/gemma-3-4b-it" target="_blank">Gemma 3 4B</a></td>
    <td>Efficient text and image model that runs locally on laptops. Multilingual support for on-device AI applications.</td>
    <td>On-device AI for mobile and edge applications, privacy-sensitive local inference, multilingual chat assistants, image captioning and description, and lightweight content generation.</td>
  </tr>
  <tr>
    <td><a href="https://huggingface.co/google/gemma-3-12b-it" target="_blank">Gemma 3 12B</a></td>
    <td>Balanced text and image model for workstations. Multi-language understanding with local deployment for privacy-sensitive applications.</td>
    <td>Workstation-based AI applications; local deployment for enterprises; multilingual document processing, image analysis and Q&A; and privacy-compliant AI assistants.</td>
  </tr>
    <tr>
    <td><a href="https://huggingface.co/collections/google/gemma-3-release" target="_blank">Gemma 3 27B</a></td>
    <td>Powerful text and image model for enterprise applications. Multi-language support with local deployment for privacy and control..</td>
    <td>Enterprise local deployment, high-performance multimodal applications, advanced image understanding, multilingual customer service, and data-sensitive AI workflows..</td>
  </tr>
  <tr>
    <td>Moonshot AI</td>
    <td><a href="https://huggingface.co/moonshotai/Kimi-K2-Thinking" target="_blank">Kimi K2 Thinking</a></td>
    <td>Deep reasoning model that thinks while using tools. Handles research, coding and complex workflows requiring hundreds of sequential actions..</td>
    <td>Complex coding projects requiring planning, multistep workflows, data analysis and computation, and long-form content creation with research.</td>
  </tr>
  <tr>
    <td>MiniMax AI</td>
    <td><a href="https://huggingface.co/MiniMaxAI/MiniMax-M2" target="_blank">MiniMax M2</a></td>
    <td>Built for coding agents and automation. Excels at multi-file edits, terminal operations and executing long tool-calling chains efficiently.</td>
    <td>Coding agents and integrated development environment (IDE) integration, multi-file code editing, terminal automation and DevOps, long-chain tool orchestration, and agentic software development.</td>
  </tr>
<tr>
    <td rowspan="2">NVIDIA</td>
    <td><a href="https://huggingface.co/google/gemma-3-4b-it" target="_blank">NVIDIA Nemotron Nano 2 9B</a></td>
    <td>High efficiency LLM with hybrid transformer Mamba design, excelling in reasoning and agentic tasks.</td>
    <td>Reasoning, tool calling, math, coding, and instruction following.</td>
  </tr>
  <tr>
    <td><a href="https://huggingface.co/google/gemma-3-12b-it" target="_blank">NVIDIA Nemotron Nano 2 VL 12B</a></td>
    <td>BAdvanced multimodal reasoning model for video understanding and document intelligence, powering Retrieval-Augmented Generation (RAG) and multimodal agentic applications.</td>
    <td>Multi-image and video understanding, visual Q&A, and summarization.</td>
  </tr>
</table>

[![My image alt description](/blog/assets/images/posts-img/reInvent_2025/03_.png)](/blog/assets/images/posts-img/reInvent_2025/03.png)

[![My image alt description](/blog/assets/images/posts-img/reInvent_2025/04_.png)](/blog/assets/images/posts-img/reInvent_2025/04.png)


## A.2

![Image](https://github.com/user-attachments/assets/b4286695-dea3-4b6b-97cd-7e6aeb14a682)

Next, we have [Amazon SageMaker Lakehouse](https://aws.amazon.com/sagemaker/lakehouse/) announcement **that unifies your data across multiple sources for your analytics and AI initiatives with a single copy of data, regardless of how your data is stored**.

Data in S3 and Redshift is unified through one copy of data, functionally combining all of your transactional, warehouse, and data-like data into one system. The lakehouse is built on AWS Glue Data Catalog and Lake Formation. Data from the operational database, such as Amazon Aurora, RDS, and DynamoDB, are also available in the lakehouse. The zero ETL integrations with third-party SaaS applications, such as Salesforce, SAP, and ServiceNow, are available in the lakehouse once the zero ETL connections are sent up.

