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

### A.3 Sagemaker HyperPod Checkpointless Training

[![My image alt description](/blog/assets/images/posts-img/reInvent_2025/28(2).png)](/blog/assets/images/posts-img/reInvent_2025/28(2).png)

[Amazon SageMaker HyperPod](https://aws.amazon.com/sagemaker/ai/hyperpod/) now introduces checkpointless training, a **foundational capability for large-scale foundation model training that eliminates the need for checkpoint-based, job-level restarts during fault recovery**. 
> Instead of interrupting training workflows, **this approach preserves forward training progress in the presence of failures**, reducing recovery times from hours to minutes.

Traditional checkpoint-based recovery requires halting the entire training cluster, manually diagnosing failures, and restoring model state from persisted checkpoints—often leaving high-cost AI accelerators underutilized for extended periods.
> Checkpointless training fundamentally changes this model by maintaining training state across the distributed cluster and enabling seamless, in-place recovery.

With **checkpointless training**, failed nodes are automatically replaced during runtime, and model state is recovered via peer-to-peer state transfer from healthy accelerators, without relying on external checkpoint restoration. By removing checkpoint dependencies from the recovery path, **this approach significantly reduces idle accelerator time, lowers operational costs, and shortens overall training cycles**. At scale, [Amazon SageMaker HyperPod](https://aws.amazon.com/sagemaker/ai/hyperpod/) achieves over 95% training goodput on clusters comprising thousands of AI accelerators.

To get started, visit the [Amazon SageMaker HyperPod](https://aws.amazon.com/sagemaker/ai/hyperpod/) product page and see the [checkpointless training GitHub page](https://github.com/aws/sagemaker-hyperpod-checkpointless-training) for implementation guidance.

### A.4 Elastic trainig for HyperPod

[![My image alt description](/blog/assets/images/posts-img/reInvent_2025/29.png)](/blog/assets/images/posts-img/reInvent_2025/29.png)

Elastic training is a new [Amazon SageMaker HyperPod](https://aws.amazon.com/sagemaker/ai/hyperpod/) capability that automatically scales training jobs based on compute resource availability and workload priority.
> Elastic training jobs can start with minimum compute resources required for model training and dynamically scale up or down through automatic checkpointing and resumption across different node configurations (world size).

Scaling is achieved by automatically adjusting the number of data-parallel replicas.

During high cluster utilization periods, elastic training jobs can be configured to automatically scale down in response to resource requests from higher-priority jobs, freeing up compute for critical workloads. When resources free up during off-peak periods, elastic training jobs automatically scale back up to accelerate training, then scale back down when higher-priority workloads need resources again.