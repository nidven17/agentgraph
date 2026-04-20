# AgentGraph

An interactive AI agent demo showcasing LangGraph-style multi-tool orchestration, ReAct reasoning loops, and RAG retrieval patterns — built with the Claude API.

**[Live Demo →]([#](https://nidven17.github.io/agentgraph/))**

---

## What It Does

AgentGraph demonstrates the core patterns used in production AI agent systems:

- **Multi-step reasoning** — the agent plans, routes, acts, and synthesizes across multiple nodes before responding
- **Tool orchestration** — routes queries to the right tool: web search, calculator, or RAG retriever
- **ReAct loop** — Reason → Act → Observe → repeat, with a visible execution trace panel
- **Conditional routing** — a router node dispatches to different tool nodes based on query type
- **State aggregation** — results from parallel tool calls are merged before synthesis

## Architecture

```
START → planner (LLM) → router → [web_search | calculator | rag_retriever]
                                          ↓
                               aggregator → synthesizer → response
                                    ↑
                              (re-enters if needed)
```

| Node | Type | Description |
|------|------|-------------|
| `planner` | LLM node | Decomposes the user query and selects tools |
| `router` | Conditional edge | Routes to one or more tool nodes |
| `web_search` | Tool node | Retrieves current information via Tavily API |
| `calculator` | Tool node | Evaluates math expressions and estimates |
| `rag_retriever` | Tool node | Semantic search over a vector knowledge base |
| `aggregator` | State node | Merges results from parallel tool executions |
| `synthesizer` | LLM node | Generates the final grounded response |

## Stack

- **Frontend**: Vanilla HTML/CSS/JS — no framework, fast to load
- **LLM**: Claude claude-sonnet-4-20250514 via Anthropic API
- **Agent pattern**: ReAct (Reason + Act), inspired by LangGraph node graph architecture
- **Fonts**: JetBrains Mono + Syne

## Running Locally

1. Clone the repo:
   ```bash
   git clone https://github.com/YOUR_USERNAME/agentgraph.git
   cd agentgraph
   ```

2. Open `index.html` and replace the API key placeholder:
   ```js
   const ANTHROPIC_API_KEY = 'YOUR_API_KEY_HERE';
   ```
   Get a free key at [console.anthropic.com](https://console.anthropic.com)

3. Open `index.html` in your browser — no build step needed.

> **Note on API key security**: For a public deployment, proxy API calls through a backend rather than exposing your key in client-side code. This demo is intended for local use or private portfolio sharing.

## Deploying to GitHub Pages

1. Push to GitHub
2. Go to **Settings → Pages**
3. Set source to `main` branch, `/ (root)`
4. Your live URL will be `https://YOUR_USERNAME.github.io/agentgraph`

## Key Concepts (for interviews)

**LangGraph** — A library where agent logic is expressed as a graph of nodes and edges. Nodes are functions (LLM calls or tool calls), edges are transitions, and state flows through the graph. Conditional edges enable dynamic routing.

**ReAct pattern** — The agent alternates between Reasoning (deciding what to do) and Acting (calling a tool), looping until it has enough information to respond.

**RAG (Retrieval Augmented Generation)** — Instead of relying on model training data, relevant documents are retrieved from a vector store at query time and included in the prompt as grounding context.

**Tool calling** — The model outputs a structured function call (not free text), the application executes it, and the result is fed back into the conversation.

---

Built by **Nidhi Venigalla** · [https://www.linkedin.com/in/nidhi-venigalla](#)
