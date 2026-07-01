# 📖 Tool Documentation

> These are the tools students must know hands-on. Read the docs, then build with them.

---

## Orchestration Frameworks
| Tool | Why It Matters | Docs |
|---|---|---|
| LangChain | Most widely used LLM framework — chains, agents, retrievers, memory | https://python.langchain.com/docs |
| LangGraph | Production-grade agent orchestration with stateful graphs | https://langchain-ai.github.io/langgraph |
| LlamaIndex | Strongest retrieval/RAG focus — better than LangChain for pure RAG | https://docs.llamaindex.ai/en/stable |
| CrewAI | Multi-agent frameworks with defined roles and task assignment | https://docs.crewai.com |

## Agent SDKs & Agent Platforms
| Tool | Why It Matters | Docs |
|---|---|---|
| OpenAI Agents SDK | Lightweight, Python-first agent runtime with tools, handoffs, guardrails, sessions, tracing | https://openai.github.io/openai-agents-python/ |
| OpenAI Responses API | Lower-level API for tool calling, state handling, and agent-style workflows | https://platform.openai.com/docs/api-reference/responses |
| Microsoft Foundry Agent Service | Managed agent platform with hosted agents, tools, observability, and enterprise controls | https://learn.microsoft.com/en-us/azure/ai-foundry/agents/overview |
| Model Context Protocol (MCP) | Standard for exposing tools and data sources to agents securely | https://modelcontextprotocol.io/ |
| Anthropic Tool Use | Function calling and tool orchestration patterns for Claude-based agents | https://docs.anthropic.com/en/docs/agents-and-tools/tool-use |

## Vector Databases
| Tool | When to Use | Docs |
|---|---|---|
| ChromaDB | Development, prototyping, small-medium scale | https://docs.trychroma.com |
| FAISS | Local, research, fastest for pure vector search | https://faiss.ai |
| Pinecone | Production managed, large scale | https://docs.pinecone.io |
| Weaviate | When hybrid search is needed natively | https://weaviate.io/developers/weaviate |

## LLM APIs
| Tool | Docs |
|---|---|
| Anthropic (Claude) | https://docs.anthropic.com |
| OpenAI | https://platform.openai.com/docs |
| Hugging Face Inference | https://huggingface.co/docs/api-inference |

## Evaluation
| Tool | Purpose | Docs |
|---|---|---|
| RAGAS | RAG system evaluation (faithfulness, relevance, groundedness) | https://docs.ragas.io |
| LangSmith | LLM application tracing, prompt versioning, evals | https://docs.smith.langchain.com |

## Deployment
| Tool | Purpose | Docs |
|---|---|---|
| FastAPI | Wrap GenAI pipelines in REST APIs | https://fastapi.tiangolo.com |
| Anthropic Prompt Caching | Reduce cost and latency on repeated prompts | https://docs.anthropic.com/en/docs/build-with-claude/prompt-caching |

## Prompt Engineering
| Resource | Link |
|---|---|
| Prompt Engineering Guide | https://www.promptingguide.ai |
| Anthropic Prompt Engineering | https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering |
