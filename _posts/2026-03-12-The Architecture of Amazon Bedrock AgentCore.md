---
layout: article
title: "Amazon Bedrock AgentCore Architecture"
date: 2026-03-11
modify_date: 2026-04-27
excerpt: "Amazon Bedrock AgentCore"
tags: [AWS, Sagemaker, Bedrock, Machine Learning, AgentCore]
mathjax: false
mathjax_autoNumber: false
key: aws-sagemaker-bedrock-agentcore-runtime-gateway-identity-memory
---
- [A. Amazon Bedrock Agentcore](#aamazon-bedrock-agentcore)
  - [A.1 AgentCore components](#a1-agentcore-components)

## A.Amazon Bedrock AgentCore

According to AWS, [Amazon Bedrock AgentCore](https://docs.aws.amazon.com/bedrock-agentcore/) is a **fully managed, agnostic** service that enables you to deploy and operate highly capable agents securely, at scale using any framework and model.

Amazon Bedrock AgentCore is presented as a comprehensive set of capabilities for the secure, large-scale deployment and operation of AI agents, independent of the underlying agentic framework or large language model. Its value proposition is particularly compelling: enabling organizations to accelerate the transition of AI agents into production environments while maintaining stringent standards for enterprise-grade security and reliability.

[![My image alt description](/blog/assets/images/posts-img/agentcore/01.png)](/blog/assets/images/posts-img/agentcore/01.png)

**Amazon Bedrock AgentCore** is:

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

The image below illustrates how these features interconnect and operate together within the overall architecture.

[![My image alt description](/blog/assets/images/posts-img/agentcore/03.png)](/blog/assets/images/posts-img/agentcore/03.png)

What really happens?

* A user or frontend application initiates a request to the agent by calling the **invoke API**. This interaction typically begins within the **AgentCore runtime**, where the agent is hosted and executed. From there, the agent can either directly interact with a large language model(LLM) or leverage an underlying framework to orchestrate and manage those interactions.

* The next thing is that we need observability(this is automatically activated) for you in AWS Cloudwatch.

* The next thing is actually the identity. How can we make sure that the user that is calling the agent is a user that is allowed to call the agent? For that  we can use **OAuth, an API key or even IAM permissions and roles**. And this is handled by **AgentCore identity**.

    > It's also called **Inbound OAuth**


  > At this stage, identity services can be invoke again, **as the agent may need to interact with external systems**. This corresponds to **outbound communication**, where proper authentication and authorization are required before making those calls.
