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
- [B. Overview of each components](#b-overview-of-each-components)
  - [B.1 Runtime](#b1-runtime)
  - [B.2 Runtime](#b2-gateway)
  - [B.3 Memory](#b3-memory)
  - [B.4 Identity](#b4-identity)
  - [B.5 Tools](#b5-tools)
  - [B.6 Observability](#b6-observability)
- [C. Select a services](#c-select-a-services)


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

* How can we make sure that the user that is calling the agent is a user that is allowed to call the agent? For that  we can use **OAuth, an API key or even IAM permissions and roles**. And this is handled by **AgentCore identity**.

    > It's also called **Inbound OAuth**

  > At this stage, identity services can be invoke again, **as the agent may need to interact with external systems**. This corresponds to **outbound communication**, where proper authentication and authorization are required before making those calls.
* The agent may need to invoke external tools, such as APIs, which are increasingly packaged as MCP endpoints. In this context, the **AgentCore gateway** facilitates this process by enabling seamless integration and access to those endpoints. So we can now turn APIs into MCP and then connect them to our agents.
* The agent may also need to store short-term interactions with the user, retrieve past conversations, or derive insights from previous exchanges. To support these capabilities, **AgentCore memory** component is integrated into the system.
* Finally, when additional capabilities are required—such as a **code interpreter or a browser—the agent** can invoke these through dedicated tool integrations. All of these components remain interconnected within the runtime environment.

## B. Overview of each components

### B.1 Runtime

**Amazon Bedrock AgentCore Runtime** provides a secure, serverless and purpose-built hosting environment for deploying and running AI agents or tools.

[![My image alt description](/blog/assets/images/posts-img/agentcore/04.png)](/blog/assets/images/posts-img/agentcore/04.png)

[![My image alt description](/blog/assets/images/posts-img/agentcore/04_.png)](/blog/assets/images/posts-img/agentcore/04_.png)

### B.2 Gateway

**Amazon Bedrock AgentCore Gateway** provides an easy and secure way for developers to build, deploy, discover, and connect to tools at scale. AI agents need tools to perform real-world tasks—from querying databases to sending messages to analyzing documents. With Gateway, developers can convert APIs, Lambda functions, and existing services into Model Context Protocol (MCP)-compatible tools and make them available to agents through Gateway endpoints.

[![My image alt description](/blog/assets/images/posts-img/agentcore/05.png)](/blog/assets/images/posts-img/agentcore/05.png)

### B.3 Memory

**AgentCore Memory** addresses a fundamental challenge in agentic AI: statelessness. 
> Without memory capabilities, AI agents treat each interaction as a new instance with no knowledge of previous conversations. 

**AgentCore Memory** provides this critical capability, allowing your agent to build a coherent understanding of users over time.

[![My image alt description](/blog/assets/images/posts-img/agentcore/06.png)](/blog/assets/images/posts-img/agentcore/06.png)

### B.4 Identity

**Amazon Bedrock AgentCore Identity** is an identity and credential management service designed specifically for AI agents and automated workloads. It provides secure authentication, authorization, and credential management capabilities that enable agents and tools to access AWS resources and third-party services on behalf of users while helping to maintain strict security controls and audit trails. 

[![My image alt description](/blog/assets/images/posts-img/agentcore/07.png)](/blog/assets/images/posts-img/agentcore/07.png)

### B.5 Tools

[![My image alt description](/blog/assets/images/posts-img/agentcore/08.png)](/blog/assets/images/posts-img/agentcore/08.png)

### B.6 Observability

**AgentCore Observability** helps you trace, debug, and monitor agent performance in production environments. It offers detailed visualizations of each step in the agent workflow, enabling you to inspect an agent’s execution path, audit intermediate outputs, and debug performance bottlenecks and failures.

[![My image alt description](/blog/assets/images/posts-img/agentcore/09.png)](/blog/assets/images/posts-img/agentcore/09.png)

## C. Select a services

 You always start with a runtime to put in your agent logic and deploy the agent.

[![My image alt description](/blog/assets/images/posts-img/agentcore/10.png)](/blog/assets/images/posts-img/agentcore/10.png)