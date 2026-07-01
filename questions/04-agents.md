# 🤖 Agents & Orchestration — Interview Questions

> Priority: 🟡 Medium — Eightfold AI confirmed take-home agent build task; BCG and Cargill test agentic workflow design

---

**Q1. What is an AI agent?**

An AI agent is an LLM that can take actions in the world — not just generate text. It has access to tools (APIs, search, code execution, databases), a reasoning loop, and memory. It iteratively reasons → acts → observes → reasons again until it completes a task. The key difference from a simple LLM call: it can take multiple steps autonomously, calling tools as needed.

---

**Q2. What is the difference between LangChain, LangGraph, CrewAI, and AutoGen?**

LangChain — orchestration framework for LLM applications: chains, agents, retrievers, memory, tools. Broadest ecosystem, best starting point.
LangGraph — built on LangChain, adds stateful graph-based orchestration for complex multi-step agents with cycles and branching. Better for production agents.
CrewAI — framework specifically for multi-agent collaboration with defined roles (Researcher, Writer, etc.) and task assignment. Good for multi-agent pipelines.
AutoGen — Microsoft's framework for multi-agent conversations, strong for code-execution agents and research-type workflows.

---

**Q3. What is the OpenAI Agents SDK and when would you choose it over LangGraph or LangChain?**

The OpenAI Agents SDK is a Python-first agent runtime that manages tool execution, handoffs, guardrails, memory/sessions, and tracing with a relatively small set of primitives. It is a strong choice when you want a lightweight, opinionated runtime for agentic apps without building the orchestration loop yourself. Use LangGraph when you need explicit stateful graph control, and LangChain when you want a larger ecosystem of connectors and abstractions.

---

**Q4. What is the difference between an agent loop, a handoff, and an MCP tool?**

An agent loop is the reasoning → action → observation cycle that continues until the task is done. A handoff allows one agent to delegate a subtask to another specialized agent. An MCP tool exposes capabilities or external data to the agent through a standard protocol, making tool integration more modular and reusable.

---

**Q5. How does tool use / function calling work?**

The LLM is given a list of available tools with their descriptions, parameters, and expected outputs. When the LLM determines a tool should be called, it outputs a structured JSON specifying the tool name and arguments — it doesn't call the tool itself. The application layer intercepts this, calls the actual tool, and feeds the result back to the LLM as an observation. The LLM then decides what to do next.

---

**Q4. What are the two types of agent memory?**

Short-term (conversation memory) — the recent conversation history passed in the context window. Implemented by storing last N exchanges. Limited by context window size.

Long-term (external memory) — past interactions stored in a vector database. The agent retrieves relevant past memories based on semantic similarity to the current query. Enables persistence across sessions and handling much larger history than fits in the context window.

---

**Q5. What can go wrong in an agent / multi-agent system?**

- Infinite loops — agent keeps calling tools without reaching a stopping condition
- Hallucinated tool calls — agent tries to call a tool that doesn't exist or with wrong parameters
- Context overflow — too many tool observations fill up the context window
- Prompt injection via tool results — a tool returns malicious text that hijacks the agent's instructions
- Cascading errors — one agent produces wrong output, next agent builds on it

Mitigations: max_iterations limit, validate tool inputs/outputs, separate instructions from content with clear delimiters, constrain tool descriptions tightly.

---

**Q6. Eightfold AI style: How would you approach a 3-day take-home agent build task?**

Day 1: Define the scope clearly. Pick the simplest architecture that demonstrates agentic behavior: one LLM, 2–3 tools, a clear reasoning loop. Set up evaluation metrics before writing a single line of code — "red flag if candidate doesn't start with evals" per multiple interview reports.

Day 2: Build the core loop. Implement tool calling, memory, and basic error handling. Write 10 test cases covering happy path and edge cases.

Day 3: Add observability (log every reasoning step and tool call), clean up code, write a README explaining architecture choices and tradeoffs, record a 2-minute demo.

Key things to demonstrate: natural interaction, clear reasoning steps visible in logs, graceful degradation on errors, and the ability to explain every design decision.

---

**Q7. How do you evaluate an agent's reliability?**

- Task completion rate — does it finish the task correctly?
- Tool call accuracy — does it call the right tool with the right arguments?
- Step efficiency — does it reach the answer in a reasonable number of steps?
- Hallucination rate — does it make up tool results or intermediate facts?
- Failure mode coverage — does it handle tool errors, invalid inputs, and context overflow gracefully?

Build a fixed test suite of tasks with known correct answers and run the agent against it on every code change.
