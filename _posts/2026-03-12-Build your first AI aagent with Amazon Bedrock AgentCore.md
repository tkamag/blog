---
layout: article
title: "Build Your First AI Agent with Amazon Bedrock AgentCore"
date: 2026-02-25
modify_date: 2026-04-27
excerpt: "Amazon Bedrock AgentCore Runtime"
tags: [AWS, Sagemaker, Bedrock, Machine Learning, AgentCore]
mathjax: false
mathjax_autoNumber: false
key: aws-sagemaker-bedrock-agentcore-runtime-gateway-identity-memory
---
- [A. Amazon Bedrock Agentcore](#aamazon-bedrock-agentcore)
  - [A.1 AgentCore components](#a1-agentcore-components)

## A. Introducing AI Agents

Sometimes people overcomplicate this stuff, so let’s keep it simple.

What's AI agents?

AI agents are systems that:

- (1) think through problems step-by-step,

- (2) connect to external tools when needed and,

- (3) learn from their actions to improve over time.

Unlike traditional chatbots that primarily generate responses based on user prompts, **agents are designed to act autonomously by planning, executing, and iterating on tasks to achieve a defined goal**. 

**For example**, instead of simply describing a dataset when asked, an agent can retrieve the relevant data, perform analysis, generate insights, and even trigger follow-up actions—such as updating a system or producing a report—without continuous user guidance.

Unlike traditional models that handle isolated tasks, an agent coordinates multiple capabilities while maintaining a coherent understanding of the overall objective. 

Rather than simply following predefined instructions, agents can adapt and make informed decisions about the next steps based on insights gathered throughout the process, operating in a way that more closely resembles human problem-solving.

- ✅ Framework agnostic: Works with deployed agents from multiple frameworks (Strands, LangGraph, CrewAI, custom MCP)

## B. Building AI Agents with LangGraph

Now that you understand what AI agents are and why they matter, let’s build one using **AgentCore runtime** — a powerful agnostic framework for building robust AI agents.

What I particularly appreciate about the **Amazon Bedrock AgentCore** is its ability to make an agent’s reasoning process explicit and traceable. Moreover, regardless of the open-source framework used, it standardizes deployment so that all agents can be deployed and operated in a consistent manner.

### B.1 How it works

There are 4 mains steps to achieve:

- ✅ Import ``BedrockAgentCoreApp``
- ✅ Create your agent (any framework)
- ✅ Define`` @app.entrypoint``
- ✅ Deploy with agentcore CLI


### B.2 The entrypoint pattern

**Key Points:**

- Same signature for ALL frameworks
- Payload = user input (100MB max)
- Context = session metadata
- Return dict serialized to JSON

[![My image alt description](/blog/assets/images/posts-img/agentcore/11.png)](/blog/assets/images/posts-img/agentcore/11.png)

- 🚀 **AgentCore Runtime** - A serverless deployment model is provided to host and scale AI agents efficiently, eliminating the need for infrastructure management while ensuring automatic scalability and operational flexibility.

| Figure | Description |
|--------|-------------|
| [![My image alt description](/blog/assets/images/posts-img/agentcore/11.png)](/blog/assets/images/posts-img/agentcore/11.png) | - Same signature for ALL frameworks
|  | - Same signature for ALL frameworks
