---
layout: article
title: "Amazon Bedrock AgentCore - The Architecture"
date: 2026-03-11
modify_date: 2026-04-27
excerpt: "Amazon Bedrock AgentCore"
tags: [AWS, Sagemaker, Bedrock, Machine Learning, AgentCore]
mathjax: false
mathjax_autoNumber: false
key: aws-sagemaker-bedrock-agentcore-runtime-gateway-identity-memory
---
- [A. Amazon Bedrock Agentcore](#aamazon-bedrock)
  - [A.1 Sagemaker AI serverless Model Customization](#a1-sagemaker-ai-serverless-model-customization)
  - [A.2 Sagemaker AI Serverless MLflow](#a2-sagemaker-ai-serverless-mlflow)
  - [A.3 Sagemaker HyperPod Checkpointless Training](#a3-sagemaker-hyperpod-checkpointless-training)
  - [A.4 Elastic trainig for HyperPod](#a4-elastic-trainig-for-hyperpod)

## A.Amazon Bedrock AgentCore

According to AWS, [Amazon Bedrock AgentCore](https://docs.aws.amazon.com/bedrock-agentcore/) is a **fully managed, agnostic** service that enables you to deploy and operate highly capable agents securely, at scale using any framework and model.

Amazon Bedrock AgentCore is presented as a comprehensive set of capabilities for the secure, large-scale deployment and operation of AI agents, independent of the underlying agentic framework or large language model. Its value proposition is particularly compelling: enabling organizations to accelerate the transition of AI agents into production environments while maintaining stringent standards for enterprise-grade security and reliability.

[![My image alt description](/blog/assets/images/posts-img/agentcore/01.png)](/blog/assets/images/posts-img/agentcore/01.png)

Amazon Bedrock AgentCore is:

* ✅ Framework agnostic: Works with deployed agents from multiple frameworks (Strands, LangGraph, CrewAI, custom MCP)

* ✅ Sophisticated authentication: Dual inbound/outbound auth with OAuth 2.0/3.0 support

* ✅ Session isolation: Each session runs in dedicated microVMs with complete security boundaries

* ✅ API transformation: Gateway automatically converts existing APIs/Lambda to MCP tools

* ✅ Enterprise security: VM-level isolation, comprehensive audit trails, SSO integration

* ✅ Production ready from day one: Scaling, security, observability

* ✅ Work with Any LLM(Claude, GPT, Llama, Bedrock, etc...)

### A.1 AgentCore components

 AgentCore platform consists of six core components:

[![My image alt description](/blog/assets/images/posts-img/agentcore/02.png)](/blog/assets/images/posts-img/agentcore/02.png)

* 🚀 **AgentCore Runtime** - A serverless deployment model is provided to host and scale AI agents efficiently, eliminating the need for infrastructure management while ensuring automatic scalability and operational flexibility.

* 🧠 **AgentCore Memory** - Enables the creation of both long-term and short-term memory for agents, supporting persistent knowledge through event-based and semantic memory mechanisms.

* 🔗 **AgentCore Gateway** - Facilitates the transformation of existing APIs into agent-compatible tools or MCP components, and streamlines the creation of custom MCP servers in just a few steps.

* 📊 **AgentCore Observability** - Provides real-time tracing and monitoring capabilities for AI agents, ensuring visibility into their behavior, performance, and execution flows.

* 🔐 **AgentCore Identity** - Provides secure authentication and access management capabilities, including support for OAuth flows and API key configuration, while ensuring sensitive credentials are stored securely in a vault.

* **AgentCore Tools**: Which include
  * 💻 **AgentCore Code Interpreter** - Enables secure code execution within isolated sandbox environments, allowing agents to generate and run code snippets for tasks such as data transformation while maintaining strict security boundaries.

  * 🌐 **AgentCore Browser** - Provides a fast, secure, cloud-based browser environment for agent-driven web interactions.

[![My image alt description](/blog/assets/images/posts-img/agentcore/03.png)](/blog/assets/images/posts-img/agentcore/03.png)