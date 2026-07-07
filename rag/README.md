# 🧠 RAG Study Hub

> This folder is dedicated to Retrieval-Augmented Generation concepts, system design, and interview-ready preparation.

---

## 1. Topics covered in a proper RAG system

A production-grade RAG system is not just "search + LLM". It is a full pipeline that combines retrieval quality, prompt design, evaluation, and operations.

### Core topics
- Problem framing and use case selection
- Data ingestion from PDFs, websites, databases, APIs, and internal documents
- Document parsing and preprocessing
- Chunking strategy and chunk overlap
- Embedding generation and vector representations
- Vector indexing and storage
- Retrieval strategy: keyword, semantic, or hybrid
- Re-ranking and context filtering
- Prompt construction with retrieved context
- Grounded answer generation
- Hallucination mitigation and guardrails
- Evaluation: faithfulness, relevance, precision, recall, latency, and cost
- Caching and performance optimization
- Security, privacy, and access control
- Monitoring, logging, and observability
- Index refresh and knowledge-base maintenance

### End-to-end RAG flow
1. Ingest data
2. Chunk documents
3. Embed chunks
4. Store embeddings in a vector database
5. Retrieve relevant context for a query
6. Re-rank and filter results
7. Send context + query to the LLM
8. Generate a grounded response
9. Evaluate and improve the pipeline

---

## 2. Types of RAG and when to use them

| Type | What it is | Best when | Advantages | Tradeoffs |
|---|---|---|---|---|
| Naive RAG | Simple retrieve-then-generate pipeline using chunking, embeddings, and vector search | You need a fast baseline or prototype | Easy to build, low complexity, quick to demo | Lower accuracy, weaker handling of complex queries |
| Advanced RAG | Adds query rewriting, hybrid search, metadata filters, re-ranking, and context compression | You need better precision and production readiness | Better retrieval quality, more robust answers | More complexity, higher latency, more engineering effort |
| Hybrid RAG | Combines keyword search and vector search | Your data has exact phrases and semantic meaning | Stronger recall and precision than either method alone | More tuning required and slightly more complex to maintain |
| Modular RAG | Splits the system into separate components like retrievers, rerankers, memory, planners, and tools | You need flexibility for enterprise or multi-step workflows | Highly extensible and customizable | More moving parts, harder to debug |
| Graph RAG | Uses knowledge graphs or entity relationships for retrieval | You need multi-hop reasoning or relational understanding | Better for connected knowledge and reasoning over relationships | Harder to build and maintain, more setup cost |
| Agentic RAG | Uses an agent to decide when to retrieve, what to retrieve, and how to use tools | You need dynamic, tool-driven workflows and planning | Can handle multi-step tasks and better decision making | Higher complexity, more latency, more failure modes |

---

## 3. Which RAG type should you use?

### Use Naive RAG when
- You are building a quick proof of concept
- Your documents are simple and structured
- Accuracy requirements are moderate
- You want the fastest path to a working demo

### Use Advanced RAG when
- You are building for production
- You need better ranking and context quality
- You care about faithfulness and answer precision
- Your users ask complex questions over large documents

### Use Hybrid RAG when
- You need both exact matching and semantic matching
- Your corpus contains technical terms, product names, or code identifiers
- You want stronger retrieval coverage

### Use Modular RAG when
- You want to scale the system over time
- You need separate components for search, reranking, memory, and tools
- You want flexibility for future changes

### Use Graph RAG when
- Your content has strong relationships between entities
- You need multi-hop reasoning over connected knowledge
- You are solving knowledge discovery or complex domain questions

### Use Agentic RAG when
- The workflow involves planning, multiple tools, or repeated retrieval
- You need the system to decide the next action dynamically
- Your use case is not just answering one question but solving a task

---

## 4. Resources you should study for RAG

### Practical deep dive
- [advanced-rag-strategies.md](advanced-rag-strategies.md) — a concise summary of the main advanced RAG patterns from the referenced repository, including re-ranking, agentic RAG, contextual retrieval, query expansion, multi-query retrieval, hierarchical RAG, self-reflective RAG, and fine-tuned embeddings.

### Official documentation
- LlamaIndex documentation for RAG patterns and retrieval pipelines
- LangChain and LangGraph documentation for orchestration and agentic workflows
- OpenAI Agents SDK and Responses API for tool calling and multi-step workflows
- Pinecone, Weaviate, ChromaDB, and FAISS documentation for vector storage and retrieval
- RAGAS documentation for evaluation of faithfulness, relevance, and grounding

### GitHub repositories and code examples
- RAG Techniques repository for practical notebooks on chunking, reranking, and graph RAG
- OpenAI Agents SDK repository for agent patterns and tool use
- Microsoft Agent Framework repository for hosted agent patterns
- Generative AI and GenAI Agents repositories for hands-on projects

### Repo resources already available in this workspace
- [../resources/documentation.md](../resources/documentation.md) — tool docs and platform references
- [../resources/github-repos.md](../resources/github-repos.md) — curated GitHub repositories
- [../resources/free-courses.md](../resources/free-courses.md) — structured learning paths
- [../resources/youtube-channels.md](../resources/youtube-channels.md) — concept videos and walkthroughs
- [../resources/question-banks.md](../resources/question-banks.md) — extra interview questions
- [../GENAI_INTERVIEW_PLAYBOOK.md](../GENAI_INTERVIEW_PLAYBOOK.md) — interview structure and answer framework

### How to use these resources effectively
1. Read the documentation to understand the concepts.
2. Build a small project to practice each concept.
3. Revise interview answers using the same examples you built.
4. Use the question bank to test your understanding under interview conditions.

---

## 5. What more should be covered in a proper RAG prep plan

A strong RAG preparation plan should go beyond the basics and include the following areas:

### A. Advanced retrieval techniques
- Hybrid search
- Re-ranking
- Query rewriting and expansion
- Context compression
- Metadata filtering

### B. Evaluation and quality control
- Faithfulness
- Answer relevance
- Context precision and recall
- Human review and gold datasets
- Automated evaluation with RAGAS

### C. Production readiness
- Chunking strategy for large corpora
- Caching and latency optimization
- Observability and tracing
- Cost control and model routing
- Versioning of indices

### D. Security and reliability
- Prompt injection defense
- PII handling
- Role-based access control
- Guardrails and safe output policies

### E. Advanced system patterns
- Multi-hop reasoning
- Graph RAG
- Agentic RAG
- Multi-modal RAG
- Memory and conversational state

---

## 6. How this can be covered in a proper format

### Recommended study structure

| Area | What to learn | How to cover it |
|---|---|---|
| Fundamentals | RAG basics, embeddings, chunking | Read docs and explain the pipeline end-to-end |
| Retrieval quality | Hybrid search, reranking, metadata filters | Build a mini project and compare results |
| Evaluation | Faithfulness, relevance, recall, latency | Create a small test set and evaluate outputs |
| Production | Caching, observability, scaling | Write a deployment note and discuss tradeoffs |
| Security | Prompt injection, access control, privacy | Add guardrails and explain them in interviews |
| Advanced patterns | Graph RAG, agentic RAG, multi-modal RAG | Read one example and summarize the architecture |

### Suggested practical roadmap
1. Build a baseline RAG bot using documents and a vector database.
2. Improve retrieval with hybrid search and reranking.
3. Evaluate the system with test questions and quality metrics.
4. Add safety, logging, and caching.
5. Compare Naive, Advanced, and Agentic RAG approaches in one notes file.

### Best way to prepare for interviews
- Prepare one clear answer for each of these: what RAG is, how it works, when to use it, what tradeoffs exist, and how to evaluate it.
- Always include architecture, retrieval quality, cost, latency, and reliability in your answer.
- Use one real project example so your answer feels concrete and practical.

---

## 7. Major tradeoffs in RAG systems

| Dimension | Tradeoff |
|---|---|
| Accuracy vs latency | Better retrieval and larger context improve quality but increase response time |
| Cost vs quality | More retrieval steps, reranking, and larger prompts improve answers but cost more |
| Recall vs precision | More retrieved context increases the chance of finding the right answer but also adds noise |
| Simplicity vs robustness | Simple systems are easier to build, but advanced systems are more reliable |
| Freshness vs maintenance | Updating the knowledge base keeps answers current but adds ingestion and re-indexing cost |
| Explainability vs flexibility | Simpler retrieval methods are easier to explain, while agentic and modular systems are more powerful but harder to reason about |

---

## 8. Advantages of one RAG approach over another

### Naive RAG
Advantages:
- Fast to implement
- Easy to explain in interviews
- Good for baseline systems

Limitations:
- Often struggles with precision and context quality

### Advanced RAG
Advantages:
- Better retrieval quality
- Better performance in production
- Stronger grounding and fewer hallucinations

Limitations:
- More complex and expensive

### Hybrid RAG
Advantages:
- Stronger recall for exact and semantic queries
- Usually performs better than pure vector search

Limitations:
- Requires tuning and careful evaluation

### Modular RAG
Advantages:
- Flexible architecture
- Easier to extend with new retrievers or tools

Limitations:
- Higher maintenance cost

### Graph RAG
Advantages:
- Great for connected knowledge and relationship-aware queries
- Better for multi-hop reasoning

Limitations:
- More difficult to design and maintain

### Agentic RAG
Advantages:
- Handles dynamic and complex tasks well
- Can use tools and memory effectively

Limitations:
- Higher complexity and potential latency overhead

---

## 9. Interview-ready summary

A strong answer in interviews should show that RAG is not just about adding documents to a prompt. It is a system design problem that includes:
- retrieval quality
- chunking strategy
- embedding choice
- ranking and filtering
- grounding and prompt design
- evaluation and monitoring
- cost, latency, and security tradeoffs

### Good interview takeaway
- Start simple with Naive RAG
- Move to Advanced or Hybrid RAG when quality matters
- Choose Graph RAG when relationships matter
- Choose Agentic RAG when the task requires reasoning and tool use

---

## 10. Quick checklist for mastering RAG

- Understand the full pipeline from ingestion to generation
- Be ready to explain chunking and embedding choices
- Know the difference between keyword, vector, and hybrid retrieval
- Be able to discuss reranking and context compression
- Mention evaluation metrics like faithfulness, relevance, and latency
- Compare tradeoffs between simplicity and robustness
- Explain when RAG is better than fine-tuning
