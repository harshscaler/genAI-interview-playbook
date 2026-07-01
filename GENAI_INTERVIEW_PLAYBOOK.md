# GenAI Interview Playbook for Students

This playbook is meant to be shared with students as a practical guide for GenAI and LLM interviews. It covers what to study, how to answer questions, and what to mention when discussing projects, systems, and real-world usage.

---

## 1. What interviewers are really looking for

In GenAI interviews, companies usually want to see four things:

- Clear understanding of core concepts like LLMs, embeddings, RAG, agents, and evaluation.
- The ability to explain tradeoffs such as accuracy vs latency, cost vs quality, and reliability vs flexibility.
- Practical experience through projects, demos, or real-world use cases.
- A production mindset: safety, observability, security, prompt quality, and monitoring.

If a student can explain a concept clearly, connect it to a project, and discuss tradeoffs, they usually perform well.

---

## 2. How to answer GenAI interview questions

A strong answer usually follows this structure:

1. Define the concept simply.
2. Explain why it matters.
3. Show how it works.
4. Mention tradeoffs or limitations.
5. Give a small example from your project or experience.

A good template is:

- What is it?
- Why do we use it?
- How does it work?
- When should we use it?
- What are the risks or alternatives?

Example phrase:

> “I would explain it as X because it helps with Y. In my project, I used it for Z, and I chose this approach because it improved A while keeping B under control.”

---

## 3. Topics that should be mentioned in interviews

### A. LLM fundamentals

Students should be able to mention:

- LLMs generate text by predicting the next token based on context.
- They can hallucinate when the model lacks enough grounding or confidence.
- Fine-tuning is useful for style or domain adaptation, but RAG is often better for factual grounding.
- Context window, temperature, prompt clarity, and model choice affect quality.

What to say:

- “I understand that LLMs are probabilistic systems and not guaranteed to be factually correct.”
- “I would reduce hallucinations by grounding the model with retrieval, clear instructions, and verification steps.”

### B. Prompt engineering

Students should mention:

- Clear instructions improve reliability.
- Few-shot examples help the model follow a format or pattern.
- Prompt design should be tested and evaluated, not assumed to work once.
- Guardrails and structured output help reduce failures.

What to say:

- “I design prompts with explicit constraints, examples, and expected output format.”
- “I evaluate prompt changes using task-specific test cases rather than relying on intuition alone.”

### C. RAG

RAG is one of the most important topics for GenAI interviews.

Students should be able to explain:

- RAG combines retrieval with generation.
- It improves factual grounding by fetching relevant context before generating an answer.
- A typical RAG pipeline includes ingestion, chunking, embedding, indexing, retrieval, ranking, and generation.
- Chunk size, metadata, embedding model, and re-ranking all influence quality.

What to say:

- “I would use RAG when the answer must be grounded in documents or internal knowledge.”
- “For retrieval quality, I would focus on chunking strategy, embedding quality, metadata filtering, and evaluation.”
- “I would add citations or source references to improve trust and transparency.”

### D. Agents and tool use

Students should mention:

- An agent is more than a single LLM call; it can plan, call tools, and make decisions.
- Tool calling, memory, and orchestration make agents useful for multi-step tasks.
- Guardrails and human-in-the-loop validation are important in real systems.

What to say:

- “I see agents as systems that combine reasoning, tools, and state management.”
- “I would use an agent when the task requires multiple steps, external tools, or feedback loops.”
- “I would include guardrails and validation so the system does not act blindly.”

### E. System design and production readiness

Students should talk about:

- Architecture choices for latency, cost, and reliability.
- Caching, batching, and model selection.
- Monitoring, logging, evaluation, and fallback behavior.
- Security, privacy, and access control.

What to say:

- “For production, I would think about latency, cost, and trust, not just response quality.”
- “I would monitor prompt failures, retrieval quality, token usage, and user feedback.”
- “I would design for failure cases, retries, and graceful degradation.”

---

## 4. Strong talking points students can mention

These are safe, useful points to include in interviews:

- “I prefer a layered approach: prompt design, retrieval, evaluation, and monitoring.”
- “I believe good GenAI systems are built with both model quality and engineering discipline.”
- “I focus on grounded outputs, not just fluent responses.”
- “I always think about how to validate the system rather than trust the first output.”
- “I treat reliability and explainability as first-class requirements.”

---

## 5. Projects students should mention

Students should be ready to talk about at least one project. Strong examples include:

- A BrowserUse-style browser automation agent built with Agent SDK that can navigate websites, click through actions, and complete simple tasks.
- An interview taker system that asks questions, evaluates answers, and gives feedback on clarity, correctness, or structure.
- A small Perplexity-style research assistant that searches the web, reads sources, and summarizes findings with citations.
- A structured automation workflow using LangGraph for multi-step tasks such as approvals, branching logic, and stateful execution.
- A RAG chatbot over documents or PDFs.
- A prompt evaluation system with test cases and scoring.
- A deployment demo with API integration or a simple web interface.

When describing a project, students should mention:

- The problem being solved.
- The architecture.
- The choice of model or tools.
- The evaluation method.
- The tradeoffs made.
- What they would improve next.

---

## 6. A simple answer framework for students

When asked any GenAI question, students can use:

- “The concept is...”
- “It is useful because...”
- “In practice, I would...”
- “The tradeoff is...”
- “In my project, I used...”

This keeps the answer structured and professional.

---

## 7. What students should avoid saying

These phrases usually weaken an answer:

- “I just used ChatGPT for everything.”
- “I don’t know much about the internals.”
- “Prompting alone solves everything.”
- “Cost and latency do not matter much.”
- “I did not think about evaluation or safety.”

Instead, students should show curiosity, clarity, and a practical mindset.

---

## 8. A short self-introduction for GenAI interviews

Students can use this 30–45 second introduction:

> “I am interested in building practical GenAI systems that are useful, reliable, and production-ready. I have worked on projects involving LLMs, prompt design, retrieval-based systems, and basic agent workflows. I focus not only on model outputs but also on evaluation, latency, cost, and user trust.”

---

## 9. Final checklist before the interview

Before appearing for a GenAI interview, students should be able to:

- Explain LLMs, embeddings, RAG, and agents in simple words.
- Discuss hallucinations and how to reduce them.
- Explain tradeoffs around cost, quality, latency, and reliability.
- Describe at least one project clearly.
- Mention evaluation, safety, and monitoring.
- Show that they think like an engineer, not just a user of AI tools.

---

## 10. One-line mantra for students

> “In GenAI interviews, do not just say what the model can do. Show how you would build, evaluate, and operate it responsibly.”
