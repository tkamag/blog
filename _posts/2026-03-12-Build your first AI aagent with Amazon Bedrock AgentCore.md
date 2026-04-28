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

🚀 **AgentCore Runtime** - A serverless deployment model is provided to host and scale AI agents efficiently, eliminating the need for infrastructure management while ensuring automatic scalability and operational flexibility.

- Same signature for ALL frameworks

- Payload = user input (100MB max)
 
- Context = session metadata

- Return dict serialized to JSON


````python
@app.entrypoint
def agent_invocation(payload, context):
    # Receives:
    # - payload: dict with user input
    # - context: RequestContext with headers, sessionid
    
    # Must return
    # - dict with result
    
    return {"result": "Hello World"}
````

### B.3 Examples

- Strands Agents example:

````python
from strands import Agent
from bedrock_agentcore.runtime import BedrockAgentCoreApp

agent = Agent(tools=[file_read, file_write])  # Simple Agent with tool use
app = BedrockAgentCoreApp(__name__)

@app.entrypoint
def agent_invocation(payload, context):
    user_message = payload.get("prompt", "")
    result = agent(user_message, context)     # Context is not mandatory

    return {"result": result.message}
````

- LanGraph Agents example:

````python
from  langgraph.graph import StateGraph
from bedrock_agentcore.runtime import BedrockAgentCoreApp

app = BedrockAgentCoreApp()

# Build your graph
graph_builder = StateGraph(State)
graph_builder.add_node("agent", call_node)
graph = graph_builder.compile()

@app.entrypoint
def agent_invocation(payload, context):
    message = [{"role": "text", "context": payload.get("prompt", "")}]
    result = graph.invoke({"message": message})
    return {"result"; result["message"][-1].content}
````

- CrewAI Agents example:

````python
from crewai import Agent, Crew, Task
from bedrock_agentcore.runtime import BedrockAgentCoreApp

app = BedrockAgentCoreApp()

# Define agent and crew
researcher = Agent(
    role="Research",
    goal="Analyze market trends and provide insights",
    backstory="Expert in market research with deep analytical skills")

Writer = Agent(
    role="Writer",
    goal="Create engaging content based on research",
    backstory="Skilled writer with experience in technical content")

crew = Crew(agents=[researcher, Writer], tasks=[task1, task2], verbose=2)

@app.entrypoint
def agent_invocation(payload, context):
    result = crew.kickoff(inputs={"topic": payload.get("prompt", "")})
    return {"result": result}
````

- Custom Framework example:

````python
from bedrock_agentcore.runtime import BedrockAgentCoreApp
import anthropic

app = BedrockAgentCoreApp()
client = anthropic.Anthropic 

@app.entrypoint
def agent_invocation(payload, context):
    # Custom logic - no framework needs
    message = payload.get("prompt", "")

    # Build your own Agent logic
    response = client.messages.create(
        model="claude-3-haiku-20240307",
        max_tokens=1000,
        messages=[
            {"role": "user", "content": message}
        ]
    )
    return {"result": response.content[0].text}
````