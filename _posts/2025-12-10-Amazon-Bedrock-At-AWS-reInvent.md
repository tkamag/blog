---
layout: article
title: "Amazon Bedrock at AWS re:invent 2025"
date: 2025-12-10
modify_date: 2025-12-10
excerpt: "Amazon Bedrock new features"
tags: [AWS, Sagemaker, Bedrock, knowledgebase, Agentcore]
mathjax: false
mathjax_autoNumber: false
key: aws-sagemaker-bedrock-opensearch-tips-knowledgebase-Agentcore
---
- [A.Amazon Bedrock](#aamazon-bedrock)
  - [A.1 More open weight model options](#a1-more-open-weight-model-options)
  - [A.2 New Mistral AI models](#a2-new-mistral-ai-models)
  - [A.3 Reinforcement Fine-tunning](#a3-reinforcement-fine-tunning)
  - [A.4 Amazon Bedrock Inference tiers](#a4-amazon-bedrock-inference-tiers)
  - [A.5 Amazon Bedrock knowledge base multimodel Retreival](#a5-amazon-bedrock-knowledge-base-multimodel-retreival)
  - [A.6 Amazon Bedrock Agentcore](#a6-amazon-bedrock-agentcore)
    - [A.6.1  Amazon Bedrock Agentcore Policy](#a61--amazon-bedrock-agentcore-policy)
    - [A.6.2  Amazon Bedrock Agentcore Evaluations](#a62--amazon-bedrock-agentcore-evaluations)
    - [A.6.3  Episodic Functionality of AgentCore Memory](#a63--episodic-functionality-of-agentcore-memory)
    - [A.6.4  Bi-directional streaming in AgentCore Runtime](#a64--bi-directional-streaming-in-agentcore-runtime)



[![My image alt description](/blog/assets/images/posts-img/reInvent_2025/01.png)](/blog/assets/images/posts-img/reInvent_2025/01.png)

In response to the rapid rise of **Generative AI** and machine learning workloads, AWS introduced numerous enhancements to Amazon Bedrock at AWS re:Invent 2025. We will examine these announcements in detail and provide clarity on their key aspects.

# A.Amazon Bedrock

[![My image alt description](/blog/assets/images/posts-img/reInvent_2025/02.png)](/blog/assets/images/posts-img/reInvent_2025/02.png)

At ReInvent 2025, Amazon announced the general availability of an additional 18 fully managed open weight models in Amazon Bedrock from new providers like Google, MiniMax AI, Mistral AI, Moonshot AI, NVIDIA, OpenAI, and Qwen, including the new Mistral Large 3 and Ministral 3 3B, 8B, and 14B models.

## A.1 More open weight model options

You can use these open weight models for a wide range of use cases across industries:

[![My image alt description](/blog/assets/images/posts-img/reInvent_2025/03.png)](/blog/assets/images/posts-img/reInvent_2025/03.png)

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

## A.2 New Mistral AI models

These four Mistral AI models are now available first on Amazon Bedrock, each optimized for different performance and cost requirements.

[![My image alt description](/blog/assets/images/posts-img/reInvent_2025/04.png)](/blog/assets/images/posts-img/reInvent_2025/04.png)

## A.3 Reinforcement Fine-tunning

[![My image alt description](/blog/assets/images/posts-img/reInvent_2025/05.png)](/blog/assets/images/posts-img/reInvent_2025/05.png)

**Amazon Bedrock reinforcement fine-tuning** enables you to customize foundation models using human feedback, aligning them closely with your business objectives and brand voice. This RLHF-based approach goes beyond simple prompt engineering, allowing models to better understand your requirements and consistently generate more accurate and relevant outputs.

This guide is designed for ML engineers, data scientists, and cloud architects looking to enhance their AI applications through Amazon Bedrock model optimization. It explains how reinforcement learning–based fine-tuning works, why it delivers superior results compared to standard techniques, and how to apply it effectively in production environments.

[![My image alt description](/blog/assets/images/posts-img/reInvent_2025/06.png)](/blog/assets/images/posts-img/reInvent_2025/06.png)

> So what is **reinforcement fine tuning**? It's a technique that enables you to customize models with the last need of data.

> So compared to supervised fine tuning, right, **you would have to come up with a large data set of label data like telling the model, this is the good responses that I want**. And you would need thousands, maybe dozens of thousands of good responses to get the model, you know, prepared to handle these kind of answers.

With **reinforcement fine tuning**, what you do is that you do a little more work in the data
preparation, but you need a lot less data. You give them a representative set of
data as an input and you let them know what good looks like, right? With a responses scoring strategy. So with that approach, you can customize the model, achieve greater accuracy with a lot of less data volume to be input to the model.

## A.4 Amazon Bedrock Inference tiers

[![My image alt description](/blog/assets/images/posts-img/reInvent_2025/07.png)](/blog/assets/images/posts-img/reInvent_2025/07.png)

The new Flex tier offers cost-effective pricing for non-time-critical applications like model evaluations and content summarization while the Priority tier provides premium performance and preferential processing for mission-critical applications. For most models that support Priority Tier, customers can realize up to 25% better output tokens per second (OTPS) latency compared to standard tier. These join the existing Standard tier for everyday AI applications with reliable performance.

## A.5 Amazon Bedrock knowledge base multimodel Retreival

[![My image alt description](/blog/assets/images/posts-img/reInvent_2025/08.png)](/blog/assets/images/posts-img/reInvent_2025/08.png)

Now you can have in the knowledge base data indexation, not only by the text search, but also by image and video similarity and all the similarity, **simplifying how you store and how you search
data that you're going to use to augment your application.**

## A.6 Amazon Bedrock Agentcore

[![My image alt description](/blog/assets/images/posts-img/reInvent_2025/15.png)](/blog/assets/images/posts-img/reInvent_2025/15.png)

**Agents** are autonomous softwares that leverage AI to reason, plan and complete tasks on behalf of human systems.

The key value proposition of Agent Core is its support for any model and any agent framework. Whether you’re using Anthropic, OpenAI, Amazon Nova, or other foundation models, Agent Core works seamlessly with them. It also integrates with popular agent frameworks such as LangChain, CrewAI, and Amazon’s own Strands Agents. This broad compatibility makes Agent Core an ideal platform for building and scaling agent-based capabilities.

### A.6.1  Amazon Bedrock Agentcore Policy

[![My image alt description](/blog/assets/images/posts-img/reInvent_2025/11.png)](/blog/assets/images/posts-img/reInvent_2025/11.png)

> It's a natural language policy engine that automatically converts your policies that you've written in natural language (in plain English, french, etc ....) into code.

For exammple, if you are a financial services firm, you can say agent cannot access customer banking data outside of business hours or from non-approved geographic regions. The system automatically converts this into enforceable policies.

**How does it work??**

[![My image alt description](/blog/assets/images/posts-img/reInvent_2025/12.png)](/blog/assets/images/posts-img/reInvent_2025/12.png)

So **agent core policy is tied to the gateway**, which is the gateway to access all the different APIs and resources. Every single request flows through gateway. 

As you can see here, the policy intercepts it to evaluate against the defined rules that you have.

You can run it in two modes.

- One is the log only mode for auditing and understanding agent behavior patterns

- Enforcement mode to actively block unauthorized actions.

This gives you complete control over which tools agents can access, what data they can interact with and what actions they permitted to perform.

### A.6.2  Amazon Bedrock Agentcore Evaluations

[![My image alt description](/blog/assets/images/posts-img/reInvent_2025/12(1).png)](/blog/assets/images/posts-img/reInvent_2025/12(1).png)

It provides the continuous automated quality monitoring with built-in evaluators. We have about 13 built-in evaluators that cover the full spectrum of agent performance.

[![My image alt description](/blog/assets/images/posts-img/reInvent_2025/12(2).png)](/blog/assets/images/posts-img/reInvent_2025/12(2).png)

### A.6.3  Episodic Functionality of AgentCore Memory

[![My image alt description](/blog/assets/images/posts-img/reInvent_2025/13.png)](/blog/assets/images/posts-img/reInvent_2025/13.png)

> **Episodic memory** enables agents to recognize patterns and learn from experience.

> Instead of storing every single raw event, it identifies important moments, summarizes them into compact records and organizes them as episodes.

### A.6.4  Bi-directional streaming in AgentCore Runtime

[![My image alt description](/blog/assets/images/posts-img/reInvent_2025/14.png)](/blog/assets/images/posts-img/reInvent_2025/14.png)

> **Bi-directional streaming memory** enables rfeal-time conversational agents with seamless interruption handling.