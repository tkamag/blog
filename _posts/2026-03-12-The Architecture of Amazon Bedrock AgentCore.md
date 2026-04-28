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

* 🚀 AgentCore Runtime - Serverless deployment to host and scaling AI agents
* 🧠 AgentCore Memory - Allows us to create Long-term and Short-term memory for the agent, Persistent knowledge with event and semantic memory
* 🔗 AgentCore Gateway - Transform existing APIs into agent tools or MCP, help us to build our own MCP server in just few steps
* 📊 AgentCore Observability - Real-time tracing and monitoring your agent.
* 🔐 AgentCore Identity - Secure authentication, access management and setup securely OAuth flow, API keys and save those informations in a vault.
* AgentCore Tools: Which include
  * 💻 AgentCore Code Interpreter - Secure code execution in isolated sandboxes where agent can create code snippet for data transformation, ...
  * 🌐 AgentCore Browser - Fast, secure cloud-based browser for web interaction with agent.

[![My image alt description](/blog/assets/images/posts-img/agentcore/03.png)](/blog/assets/images/posts-img/agentcore/03.png)