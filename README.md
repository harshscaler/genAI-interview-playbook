# 🚀 GenAI Placement Prep 

> A student-ready GenAI / LLM interview prep hub focused on what companies ask, what students should build, and which resources to use.

---

## 📂 Repository Structure

```
scaler-genai-placement-prep/
│
├── README.md                        ← You are here
├── questions/                       ← Interview question banks
│   ├── README.md
│   ├── 01-foundations.md
│   ├── 02-prompt-engineering.md
│   ├── 03-rag.md
│   ├── 04-agents.md
│   ├── 05-system-design.md
│   ├── 06-production-cost-latency.md
│   └── 07-hr-round.md
├── rag/                             ← Dedicated RAG study material
│   └── README.md
└── resources/                       ← Learning resources and project ideas
    ├── README.md
    ├── github-repos.md
    ├── free-courses.md
    ├── youtube-channels.md
    ├── documentation.md
    └── question-banks.md
```

---

## ⚡ Quick Start for Students

| If you have... | Start here |
|---|---|
| 1 day | [Top questions](./questions/README.md) + [HR round tips](./questions/07-hr-round.md) |
| 1 week | Complete the most important question categories + build one GenAI project |
| 1 month | Build 2–3 projects, revise all question banks, and run mock interviews |

### How to use this repo
- Start with the question banks in `questions/`.
- Use `resources/` for tool docs, SDKs, project ideas, and external prep.
- Check `companies/` for company-specific GenAI relevance and hiring expectations.
- Answer questions with a focus on tradeoffs, reliability, and production readiness.

### Most important files
- `questions/README.md` — GenAI question bank overview
- `questions/03-rag.md` — RAG pipeline questions (highest priority)
- `rag/README.md` — dedicated RAG concepts, system design, and tradeoffs guide
- `questions/04-agents.md` — agent and orchestration questions
- `questions/07-hr-round.md` — HR AI tool fluency questions
- `resources/documentation.md` — official docs for Agent SDKs and vector databases
- `companies/README.md` — company-specific GenAI prep guidance

### Agent SDK & Agentic AI resources to prioritise
- OpenAI Agents SDK
- Microsoft Foundry Agent Service / Hosted Agents
- Model Context Protocol (MCP)
- LangGraph for structured agent orchestration

---

## 🎯 Interview topics covered
- LLM fundamentals
- Prompt engineering
- Retrieval-augmented generation (RAG)
- Agents & orchestration
- GenAI system design
- Production cost, latency, and observability
- HR / AI tool fluency

---

## 🔥 What companies ask by category

### LLM fundamentals
- What is an LLM and how does it work?
- What causes hallucinations and how do you reduce them?
- What are embeddings and how are they used in retrieval?

### Prompt engineering
- How do you design prompts for accuracy and robustness?
- How do you evaluate prompt changes?
- What are common prompt engineering mistakes?

### RAG pipelines
- What is RAG and why does it exist?
- Design a RAG system for a customer support chatbot.
- How do you choose chunk size, retriever type, and re-ranking strategy?

### Agents & orchestration
- What is an AI agent and how is it different from a simple LLM call?
- How does tool calling / function calling work?
- When should you use OpenAI Agents SDK vs LangChain or LangGraph?
- What are handoffs, guardrails, and agent memory?

### System design & production
- How do you design a production-ready GenAI system with caching, scaling, and privacy?
- What is the cost/latency/quality tradeoff?
- What should you log in a GenAI application?
- How do you monitor and secure a GenAI system?

### HR / behavioral
- How do you use AI tools in your daily workflow?
- Do you trust AI-generated code? How do you verify it?
- Where should AI not be used?
- What GenAI/AI projects have you built?

---

## 🧠 What students should do

### Prepare answers
- Use the question banks in `questions/` as the core interview checklist.
- Practice structured answers with: definition, why it matters, how it works, tradeoffs, and an example.
- Keep AI tool answers concrete: mention tools, use cases, and verification steps.

### Build projects
- RAG chatbot with document ingestion, vector search, and grounded answer generation.
- Agent prototype with tool calling, validation, guardrails, and a simple reasoning loop.
- Deployment demo with FastAPI or a minimal web UI showing prompt history and tool call trace.
- Portfolio-ready case study with architecture, tradeoffs, and testing notes.

### Share with students
- A one-page prep checklist with key topics and question categories.
- A short study plan: 1 day (must-know), 1 week (project + revision), 1 month (portfolio + mocks).
- A list of practical project ideas and resource links.
- Guidance on how to explain tradeoffs and safety in every answer.

---

## 📚 Recommended resources
- [GENAI_INTERVIEW_PLAYBOOK.md](./GENAI_INTERVIEW_PLAYBOOK.md) — student-ready guide for interviews, talking points, and answer structure
- [resources/documentation.md](./resources/documentation.md) — tool docs, Agent SDKs, MCP, vector DBs, APIs
- [resources/github-repos.md](./resources/github-repos.md) — interview repos and agent examples
- [resources/free-courses.md](./resources/free-courses.md) — learning paths and project courses
- [resources/youtube-channels.md](./resources/youtube-channels.md) — quick GenAI concept videos
- [resources/question-banks.md](./resources/question-banks.md) — external question collections

---

## 🚀 Project ideas for GenAI rounds
- Build a BrowserUse-style browser automation agent using Agent SDK for web navigation and action execution.
- Create an interview taker system that asks questions, evaluates answers, and provides feedback.
- Build a small Perplexity-style research assistant that searches the web, gathers sources, and summarizes results.
- Create structured automation flows with LangGraph for multi-step tasks, approvals, and stateful execution.
- Add a RAG-based customer support bot with grounded answers and retrieval quality controls.
- Build an agentic task assistant that uses two tools (e.g. search + calculator or document lookup).
- Add a FastAPI wrapper for a GenAI app with logging, prompt history, and tool call trace.
- Prepare a portfolio-ready project with architecture notes, tradeoffs, and test cases.

---

## 🏢 Company prep note
- Use `companies/README.md` for company-specific GenAI relevance.
- Most placement companies will test GenAI in HR/tool-fluency rounds.
- For GenAI-first roles, focus on RAG, agents, and production deployment examples.

---
