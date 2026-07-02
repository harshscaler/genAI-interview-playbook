# 🔍 RAG Pipelines — Interview Questions

> Priority: 🔴 HIGHEST — "Design a RAG system for a customer support chatbot" is the most commonly reported opening question in 2026 GenAI technical rounds across multiple companies.

---

## RAG Interview Prep: What Can Be Asked and What You Should Do

### What is RAG?

RAG (Retrieval-Augmented Generation) is a method where an LLM first retrieves relevant information from an external source and then uses that retrieved context to generate a grounded answer.

It is useful when you want to:
- reduce hallucinations
- use private or recent data
- make responses more accurate and explainable

### What interviewers usually ask about RAG

Common questions include:
- What is RAG and why was it created?
- How does a RAG pipeline work step by step?
- What are the different types of RAG?
- What are the tradeoffs between simple and advanced RAG?
- How do you improve retrieval quality?
- How do you reduce hallucinations in RAG?
- How would you design a RAG system for a chatbot or enterprise search tool?

### What you should be ready to explain

You should be able to talk about:
1. **Ingestion** — where the source documents come from.
2. **Chunking** — how documents are split into smaller pieces.
3. **Embedding and indexing** — how content is converted and stored for retrieval.
4. **Retrieval** — how relevant chunks are found for a query.
5. **Ranking / re-ranking** — how the best results are selected.
6. **Generation** — how the LLM uses the retrieved context to answer.
7. **Evaluation** — how you measure faithfulness, relevance, latency, and cost.

### Types of RAG

| Type | Description | Best Use Case |
|---|---|---|
| **Naive RAG** | Basic retrieve-then-generate flow using chunking, embeddings, and vector search. | Simple prototypes and baseline systems |
| **Advanced RAG** | Adds query rewriting, hybrid search, metadata filtering, re-ranking, and context compression. | Production systems that need better accuracy |
| **Modular RAG** | Uses separate modules like retrievers, rerankers, memory, tools, and planners. | Complex workflows and enterprise applications |
| **Graph RAG** | Uses relationships between entities to retrieve connected knowledge. | Multi-hop reasoning and knowledge discovery |
| **Agentic RAG** | Uses an agent to decide when and how to retrieve information. | Dynamic and tool-driven systems |

### Tradeoffs to mention in interviews

| Area | Tradeoff |
|---|---|
| **Chunk size** | Smaller chunks are more specific, but larger chunks preserve better context. |
| **Accuracy vs latency** | Better retrieval usually increases response time and cost. |
| **Recall vs precision** | More retrieval can improve recall but also introduce noise. |
| **Simple vs advanced architecture** | Simpler systems are easier to build, but advanced systems are more robust. |
| **Keyword vs vector search** | Keyword search is precise for exact terms, while vector search is better for semantic meaning. |

### What you can do in practice

To show strong understanding, you can describe how you would:
- start with a simple baseline RAG system
- test chunking strategies on sample documents
- compare keyword search, vector search, and hybrid search
- add reranking for better retrieval quality
- evaluate answers using faithfulness, relevance, and latency metrics
- improve the system by adding metadata filters, caching, or guardrails

### Interview-ready takeaway

A strong answer should show that RAG is not just about putting documents into a prompt. It is a full system design and product problem involving retrieval quality, chunking, indexing, ranking, prompting, evaluation, and tradeoffs.

---

## Questions & Answers

**Q1. What is RAG and why was it developed?**

RAG (Retrieval-Augmented Generation) combines retrieval with generation to overcome three key LLM limitations: hallucination (models generate false but plausible facts), outdated knowledge (training data has a cutoff date), and inability to access private enterprise data. Instead of relying only on what the model learned during training, RAG retrieves relevant documents at inference time and gives them to the model as context to generate grounded answers.

---

**Q2. Walk me through the RAG pipeline end-to-end.**

```
Ingest → Chunk → Embed → Index → [Query Time] → Retrieve → Rank → Synthesize
```

1. **Ingest** — Parse source documents (PDFs, web pages, databases)
2. **Chunk** — Split documents into smaller segments
3. **Embed** — Convert chunks to vector embeddings using an embedding model
4. **Index** — Store embeddings in a vector database with metadata
5. **Query** — Embed the user's question using the same embedding model
6. **Retrieve** — Similarity search returns top-k relevant chunks
7. **Rank** — Optional re-ranking step for better precision
8. **Synthesize** — Feed user query + retrieved chunks into LLM to generate answer

---

**Q3. What is chunking and what strategy would you choose?**

Chunking splits large documents into smaller segments before embedding, because LLMs have context window limits and retrieval quality depends on chunk relevance.

- **Fixed-size chunking** — split every N tokens with M% overlap. Simple and fast. Start with 300–800 tokens, 10–20% overlap.
- **Semantic chunking** — split at logical paragraph or section boundaries. Retains context better but computationally heavier.

Too large → retrieval misses the specific relevant content. Too small → context fragmentation, loses surrounding meaning. Overlap preserves continuity across boundaries.

---

**Q4. What is the difference between keyword search and vector search?**

**Keyword search (BM25)** — matches exact terms. Fast, transparent, great for precise queries. Fails on synonyms or paraphrasing.

**Vector search (semantic search)** — converts query and documents to embeddings, finds semantic neighbors via cosine similarity. Handles paraphrasing and synonyms well. Slower, less transparent.

**Hybrid search** — combines both approaches (BM25 + vector). Most production RAG systems use hybrid search because it outperforms either approach alone — BM25 catches exact matches that vector search misses; vector search catches semantic matches that BM25 misses.

---

**Q5. Compare FAISS, ChromaDB, Pinecone, and Weaviate.**

| Vector DB | Best For | Deployment | Notes |
|---|---|---|---|
| FAISS | Local prototyping, research | In-process / local | Facebook's library, very fast, no persistence out-of-the-box |
| ChromaDB | Development, small-medium scale | Local or cloud | Easy to set up, good for prototyping |
| Pinecone | Production, managed, large scale | Managed cloud | No infra management, expensive at scale |
| Weaviate | Hybrid search built-in | Self-hosted or cloud | Strong hybrid search native support |

---

**Q6. What is re-ranking and when would you use it?**

Raw vector search returns top-50 results by approximate similarity — noisy because the fast ANN (Approximate Nearest Neighbor) search trades precision for speed. A re-ranker (cross-encoder, e.g., Cohere Rerank) takes those 50 candidates and re-scores them with higher precision, returning the top-5 most relevant chunks to send to the LLM. Use re-ranking when retrieval precision is critical and you can afford the extra latency.

---

**Q7. How do you evaluate a RAG system?**

RAG evaluation is system-level — not just LLM output quality.

**Retrieval metrics:**
- Recall@k — are the relevant chunks in the top-k results?
- MRR (Mean Reciprocal Rank) — how high is the first relevant result?

**Generation metrics (via RAGAS):**
- Faithfulness — is the answer grounded in the retrieved chunks?
- Answer relevance — does the answer actually address the question?
- Context precision — are the retrieved chunks relevant?

Build a small "gold set" of question-answer pairs and run automated evaluation using RAGAS. Human spot-checks for top queries.

---

**Q8. How do you handle hallucination in a RAG system?**

Hallucinations in RAG usually come from two sources: (a) bad retrieval — the relevant chunks weren't retrieved, so the model generates from memory, and (b) bad prompting — the model isn't instructed to stay grounded.

Mitigations:
- Instruct the model explicitly: "Answer only based on the provided context. If the answer isn't in the context, say 'I don't know'."
- Use faithfulness scoring to detect ungrounded answers
- Add fallback messages when retrieval confidence is low
- Use re-ranking to improve retrieval quality

---

**Q9. When should you use RAG vs fine-tuning?**

| Situation | Use RAG | Use Fine-tuning |
|---|---|---|
| Need access to current/private data | ✅ | ❌ |
| Knowledge changes frequently | ✅ | ❌ |
| Need to teach a new task or style | ❌ | ✅ |
| Need to change model behavior | ❌ | ✅ |
| Fast prototyping needed | ✅ | ❌ |

In practice: try RAG first. Fine-tune only when RAG can't solve the problem, because fine-tuning is expensive and data-hungry.

---

**Q10. ⭐ SYSTEM DESIGN: Design a RAG system for a customer support chatbot.**

A complete answer covers all layers:

**Ingestion pipeline:**
- Parse support docs, FAQs, ticket history (PDFs, HTML, structured DB)
- Chunk semantically at paragraph boundaries (~500 tokens, 15% overlap)
- Embed with text-embedding-3-small (or BGE for cost savings)
- Store in Pinecone/Weaviate with metadata: doc_id, date, access_level, category

**Query pipeline:**
- Embed user query with same embedding model
- Hybrid search: BM25 + vector, retrieve top-50
- Re-rank with Cohere Rerank → top-5 chunks
- Inject into prompt with clear delimiters and source citations
- Stream response via SSE

**Safety layer:**
- Input: sanitize for prompt injection
- Output: scan for PII before returning to user
- Guardrails: topic restriction to support scope

**Observability:**
- Log every step: query → retrieved chunks → generated answer → latency → cost
- Set up LangSmith or custom logging for trace-level debugging
- Faithfulness eval on sampled queries (weekly)

**Tradeoffs to mention:**
- Chunking too small → fragmentation. Too large → retrieval misses.
- ChromaDB for dev → Pinecone for prod (managed, scalable)
- Semantic cache: if a query is mathematically similar to a previous one → return cached answer immediately, skip LLM call
- Cost control: route simple queries to a smaller model (gpt-4o-mini), escalate complex ones to gpt-4o

---

**Q11. How do you keep your RAG knowledge base up to date?**

- Trigger re-ingestion pipelines on content changes (webhook or scheduled job)
- Re-embed when the embedding model changes (model drift = stale indexes)
- Version your vector indexes — don't overwrite in place, roll back if quality drops
- Use metadata filters (doc_date, doc_version) so queries can filter to recent content
- Batch re-embeddings during off-peak hours

---

**Q12. What is the "ingest → chunk → embed → index" vs "query time" split?**

Ingestion (offline, one-time or scheduled): expensive operations — parsing, chunking, embedding — done ahead of time and stored.

Query time (online, per user request): embed query (fast), similarity search (fast), LLM generation (fast). All expensive computation is pre-computed.

This split is why RAG can be low-latency at query time even with large document corpora.

---

**Q13. What metadata should you store alongside embeddings in your vector DB?**

- Document ID and source URL
- Creation/update date (for recency filtering)
- Access level / permissions (for multi-tenant data isolation)
- Document category / type (for filtering scope)
- Chunk index within the document (for context window assembly)

Metadata filters let you do "vector search restricted to documents the user has access to" — critical for enterprise RAG.

---

**Q14. How would you design a RAG system to scale to 1 million documents?**

- Use an approximate nearest neighbor (ANN) index (HNSW in Weaviate, IVF in FAISS) — exact search doesn't scale
- Shard the vector index across multiple nodes
- Cache embeddings — don't re-embed unchanged documents
- Use semantic caching at the query layer — cache answers to semantically similar queries
- Separate the ingestion pipeline (batch, async) from the query pipeline (real-time, low-latency)
- Monitor index quality over time — re-index when embedding model updates

---

**Q15. What is a "semantic cache" in a RAG/GenAI system?**

A semantic cache intercepts incoming queries before retrieval. It embeds the query and checks similarity against cached (query, answer) pairs. If a semantically similar query was already answered, return the cached answer immediately — skipping retrieval and LLM generation entirely. This dramatically reduces cost and latency for repeated or similar questions (common in support chatbots where users ask the same thing in different words).
