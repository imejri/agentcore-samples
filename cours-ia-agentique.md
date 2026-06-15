# Cours - IA Agentique et AWS AgentCore

## Introduction aux Frameworks Agentiques

Agentic frameworks transform Large Language Models, or LLMs, from simple question-answering systems into goal-oriented agents that can execute complex tasks. These frameworks provide key capabilities for autonomous work and problem-solving.

---

## Agentic AI Framework Capabilities

### Architecture Overview

```mermaid
graph TD
    F["Framework"]
    A["Agents"]
    L["LLM"]
    T["Tools"]
    M["Memory"]

    F <--> A
    F <--> L
    F <--> T
    F <--> M
    A <--> L
    T <--> M

    style F fill:#4a90d9,stroke:#2c5f8a,color:#fff,font-weight:bold
    style A fill:#5bb85b,stroke:#3d7a3d,color:#fff
    style L fill:#f0ad4e,stroke:#c78c3e,color:#fff
    style T fill:#d9534f,stroke:#a63c39,color:#fff
    style M fill:#9b59b6,stroke:#7d3c98,color:#fff
```

### Key Capabilities

| Capability | Description |
|---|---|
| **Agent Orchestration** | Coordinates information flow and decision-making across single or multiple agents to achieve complex goals without human intervention. |
| **Model and Tool Integration** | Helps agents interact with LLMs for reasoning. Connects agents to external systems, APIs, and data sources to enrich context with knowledge. |
| **Memory Management** | Provides persistent or session-based state to maintain context across interactions. Important for long-running autonomous tasks. |
| **Workflow Definition** | Supports structured patterns like chains, routing, parallelization, and reflection loops that enable autonomous reasoning. |
| **Deployment and Monitoring** | Facilitates the transition from development to production with observability for autonomous systems. Helps agents operate reliably at scale. |

---

## Detailed Capabilities

### 1. Agent Orchestration

Agent orchestration coordinates information flow and decision-making across single or multiple agents to achieve complex goals without human intervention.

### 2. Model and Tool Integration

Model and tool integration helps agents interact with LLMs for reasoning. This integration also connects agents to external systems, APIs, and data sources to enrich context with knowledge.

### 3. Memory Management

Memory management provides persistent or session-based state to maintain context across interactions. This capability is important for long-running autonomous tasks.

### 4. Workflow Definition

Workflow definition supports structured patterns like chains, routing, parallelization, and reflection loops that enable autonomous reasoning.

### 5. Deployment and Monitoring

Deployment and monitoring facilitate the transition from development to production with observability for autonomous systems. This helps your agents operate reliably at scale.

---

## Open-Source Frameworks

There are open-source frameworks for building AI agents. They provide building blocks for tool use, memory, routing, collaboration, and production ops.

```mermaid
graph LR
    subgraph Frameworks["Open-Source Agentic Frameworks"]
        direction TB
        C["1. CrewAI"]
        LG["2. LangGraph & LangChain"]
        LI["3. LlamaIndex"]
        S["4. Strands Agents SDK"]
    end

    C --> |"Role-based collaboration"| UC1["Content, Research, Operations"]
    LG --> |"Stateful graph workflows"| UC2["Multi-step Workflows"]
    LI --> |"Data & RAG-first"| UC3["Enterprise QA & Analytics"]
    S --> |"Typed tool-using agents"| UC4["Automation & Microservices"]

    style C fill:#e74c3c,stroke:#c0392b,color:#fff
    style LG fill:#3498db,stroke:#2980b9,color:#fff
    style LI fill:#9b59b6,stroke:#8e44ad,color:#fff
    style S fill:#27ae60,stroke:#1e8449,color:#fff
```

### 1. CrewAI

> **Use case:** Coordinated content, research, and operations.

CrewAI enables role-based agent collaboration. It orchestrates specialist teams with task decomposition, handoffs, review and feedback, and optional human-in-the-loop (HITL) support. Good for coordinated content, research, and operations.

**Key features:**
- Role-based agent collaboration
- Task decomposition and handoffs
- Review and feedback loops
- Optional human-in-the-loop (HITL) support

---

### 2. LangGraph and LangChain

> **Use case:** Multi-step workflows needing tracing and persistence.

LangGraph and LangChain support complex, stateful agent apps. LangGraph models control flow as a graph (branching, loops, checkpoints). LangChain provides tool calling and memory plus a large ecosystem. Use for multi-step workflows needing tracing and persistence.

**Key features:**
- Control flow modeled as a graph
- Branching, loops, and checkpoints
- Tool calling and memory
- Large ecosystem with tracing support

---

### 3. LlamaIndex

> **Use case:** Enterprise QA and analytics across many data systems.

LlamaIndex is data and Retrieval Augmented Generation (RAG)-first. It offers indexes, retrievers, and routers so agents can query heterogeneous sources (docs, SQL, APIs) and synthesize answers. Choose for enterprise QA and analytics across many data systems.

**Key features:**
- Data and RAG-first approach
- Indexes, retrievers, and routers
- Query heterogeneous sources (docs, SQL, APIs)
- Answer synthesis across multiple data systems

---

### 4. Strands Agents SDK

> **Use case:** Reliable automation and microservice tasks.

Strands Agents SDK is a lightweight Python SDK for typed tool-using agents. It emphasizes safety (permissions, timeouts, retries) and easy backend embedding. Use for reliable automation and microservice tasks.

**Key features:**
- Lightweight Python SDK
- Typed tool-using agents
- Safety emphasis (permissions, timeouts, retries)
- Easy backend embedding

---

## The Agentic Loop with Strands Agents

### How the Agentic Loop Works

The agentic loop is the core mechanism that allows a Strands agent to reason, act, and iterate until it produces a final response. The agent receives a prompt, invokes a model for reasoning and tool selection, executes tools as needed, and returns a final response when the task is complete.

```mermaid
graph LR
    P["Prompt"] -->|"Invoke agent"| A["Agent"]
    
    subgraph Loop["Agentic loop"]
        A -->|"Invoke model"| M["Model"]
        M -->|"Get response, reasoning, tool selection"| A
        A -->|"Execute tool"| T["Tools"]
        T -->|"Return result"| A
    end
    
    A -->|"Return final response"| R["Result"]

    style P fill:#f5f5f5,stroke:#333,color:#333
    style A fill:#87ceeb,stroke:#4a90d9,color:#333,font-weight:bold
    style M fill:#f5f5f5,stroke:#333,color:#333
    style T fill:#f5f5f5,stroke:#333,color:#333
    style R fill:#f5f5f5,stroke:#333,color:#333
    style Loop stroke:#999,stroke-dasharray:5 5
```

**Loop steps:**
1. The **Prompt** invokes the agent with a user query.
2. The **Agent** invokes the **Model** to get reasoning and tool selection.
3. The **Model** returns its response (reasoning + selected tool) to the Agent.
4. The **Agent** executes the selected **Tool**.
5. The **Tool** returns its result to the Agent.
6. The Agent repeats steps 2-5 as needed, then returns the **final response**.

---

### Strands Agents Example: RecipeBot

The RecipeBot agent accepts a user query and returns a recipe. To create the agent, you define three components: a **system prompt**, a **model**, and **tools**.

```mermaid
graph TD
    A["Agent"]
    SP["system prompt"]
    M["Model"]
    T["Tools"]

    SP -.- A
    A <-->|"reasoning"| M
    A <-->|"execution"| T

    style A fill:#87ceeb,stroke:#4a90d9,color:#333,font-weight:bold
    style SP stroke:#999,stroke-dasharray:5 5,fill:#fff,color:#333
    style M fill:#f5f5f5,stroke:#333,color:#333
    style T fill:#f5f5f5,stroke:#333,color:#333
```

**Components:**
- **System prompt**: Instructions that define the agent's behavior and persona (e.g., "You are a helpful cooking assistant").
- **Model**: The LLM backend used for reasoning (e.g., Amazon Bedrock).
- **Tools**: External capabilities the agent can use (e.g., web search to find recipes).

---

### Using the Agent

```python
from strands import Agent

recipe_agent = Agent(
    system_prompt=system_prompt,
    model=bedrock_model,
    tools=[websearch]
)

response = recipe_agent("Suggest a recipe with chicken and broccoli.")
```

---

### RecipeBot Workflow

The following steps describe the end-to-end flow when a user interacts with the RecipeBot agent:

```mermaid
sequenceDiagram
    participant User
    participant recipe_agent as recipe_agent
    participant BedrockModel as BedrockModel()
    participant websearch as websearch

    User->>recipe_agent: 1. User query ("Suggest a recipe with chicken and broccoli.")
    recipe_agent->>recipe_agent: 2. Agent initialization
    recipe_agent->>BedrockModel: 3. LLM processing
    BedrockModel->>recipe_agent: Tool selection
    recipe_agent->>websearch: 4. Tool usage (web search)
    websearch->>recipe_agent: 5. Tool result
    recipe_agent->>BedrockModel: Process tool result
    BedrockModel->>recipe_agent: 5. LLM response
    recipe_agent->>User: 6. Generated response
```

**Steps:**
1. **User query**: The user sends a question to the `recipe_agent`.
2. **Agent initialization**: The agent loads the system prompt, model, and tools.
3. **LLM processing**: The agent sends the query to `BedrockModel()` for reasoning.
4. **Tool usage**: The model decides to use `websearch` to find relevant recipes.
5. **Tool result and LLM response**: The search results are returned to the agent, then processed by the model to formulate a coherent answer.
6. **Generated response**: The final recipe suggestion is returned to the user.

---

## Comparison Table

| Framework | Focus | Best For | Key Strength |
|---|---|---|---|
| **CrewAI** | Role-based collaboration | Content, Research, Operations | Team orchestration with HITL |
| **LangGraph / LangChain** | Stateful graph workflows | Multi-step workflows | Branching, loops, checkpoints |
| **LlamaIndex** | Data & RAG | Enterprise QA & Analytics | Heterogeneous data querying |
| **Strands Agents SDK** | Typed tool agents | Automation & Microservices | Safety and reliability |

---

*Document en cours de construction - Prochaine section : AWS AgentCore*
