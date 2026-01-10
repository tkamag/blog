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

[![My image alt description](/blog/assets/images/posts-img/reInvent_2025/01.png)](/blog/assets/images/posts-img/reInvent_2025/01_.png)


In response to the rapid rise of **Generative AI** and machine learning workloads, AWS introduced numerous enhancements to Amazon Bedrock at AWS re:Invent 2025. We will examine these announcements in detail and provide clarity on their key aspects.

## A.1

[![My image alt description](/blog/assets/images/posts-img/reInvent_2025/02_.png)](/blog/assets/images/posts-img/reInvent_2025/02.png)


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

<div align="center">
<img src="/blog/assets/images/posts-img/reInvent_2025/04_.png" alt="Centered Image" width="600">
</div>

## A.2

![Image](https://github.com/user-attachments/assets/b4286695-dea3-4b6b-97cd-7e6aeb14a682)

Next, we have [Amazon SageMaker Lakehouse](https://aws.amazon.com/sagemaker/lakehouse/) announcement **that unifies your data across multiple sources for your analytics and AI initiatives with a single copy of data, regardless of how your data is stored**.

Data in S3 and Redshift is unified through one copy of data, functionally combining all of your transactional, warehouse, and data-like data into one system. The lakehouse is built on AWS Glue Data Catalog and Lake Formation. Data from the operational database, such as Amazon Aurora, RDS, and DynamoDB, are also available in the lakehouse. The zero ETL integrations with third-party SaaS applications, such as Salesforce, SAP, and ServiceNow, are available in the lakehouse once the zero ETL connections are sent up.

## A.3

![Image](https://github.com/user-attachments/assets/22693f62-a0de-4393-8f3c-ff013875402f)

Amazon Data Zones will work with the Amazon SageMaker catalog and the SageMaker Unified Studio to help with discovery, governance, and collaboration for data and AI across your lakehouse, AI models, and applications.

## A.4

![Image](https://github.com/user-attachments/assets/af3ee094-3dc8-4da0-90ed-831b7f365f67)

This is a major expansion of data that provides you with a unified view of your wider assets, not just your data, but also your ML and your AI models and your applications. You can now further coordinate with the creation of data assets, tracking of data lineage, manual, or ML automated documentation of business data descriptions. Search is also easier across your data and ML assets, with searches invoked from SageMaker Unified Studio or from the Amazon DataZone portal.

## A.5

![Image](https://github.com/user-attachments/assets/a67155b0-1b8f-4775-92b2-b73cb1302666)

Understanding data lineage is a common ask for many people. They think of lineage as the documented changes to the source data schema that can impact downstream transformation jobs or analytics, with the ability to audit data movement and access. 

Data lineage in DataZone and SageMaker Unified Studio will allow you to visualize your data's origins, transformations, and consumption so that you can enhance trust and verification of your data and those providing you the data, making it so that your evolving schemas are a lot more reliable.

## A.6

![Image](https://github.com/user-attachments/assets/83f67b15-1d7e-4d48-a692-831ac735b86f)

SageMaker Lakehouse is also **leveraging a unified connectivity to third party tools with this zero ETL connection**. There are additional service integrations between DynamoDB and SageMaker Lakehouse, as well as SaaS applications like Salesforce, SAP, Zendesk, and ServiceNow that provide an integrated access without building custom ETL pipelines. This is due to a new and existing glue connections and new connections from the SageMaker Unified Studio.

## A.7

![Image](https://github.com/user-attachments/assets/edfbb6e9-51bc-465e-9516-2259d666aa83)

AWS announced last year [SageMaker HyperPod](https://aws.amazon.com/fr/sagemaker-ai/hyperpod/). This is designed to streamline your distributed model training by effectively distributing your training activity across the accelerators in a cluster processing them in parallel.

The HyperPods training cluster is also resilient and self-healing and allows you to pause and inspect training jobs, which is usually a lot more complicated if you've never done that.

AWS know launched [SageMaker HyperPod Task governance](https://docs.aws.amazon.com/sagemaker/latest/dg/sagemaker-hyperpod-eks-operate-console-ui-governance.html), which will dynamically allocate compute resources and provide real-time analytics and insights of your compute allocation and utilization.

You can do things like define priorities, fine-tuning, training, and inference, and then you set up limits for the compute resources by teams and by projects.
You can easily reach thousands of different configurations of the training stack and training performance can be very significantly based on your chosen configurations.

## A.8

![Image](https://github.com/user-attachments/assets/068304ec-65ae-4ed0-a630-9bb5973668e7)

This year AWS introduced [SageMaker HyperPod Recipes](https://docs.aws.amazon.com/sagemaker/latest/dg/sagemaker-hyperpod-recipes.html) to provide a curated, ready-to-use, and customizable SageMaker recipe for pre-training and fine-tuning foundation models, models like llama, mistral, and so on. AWS will continue to add more recipes and more models to help you have a fully managed end-to-end training loop for those models.

