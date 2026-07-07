# Advanced RAG Strategies Guide

> This note is a curated summary of the ideas in the repository https://github.com/coleam00/ottomator-agents/tree/main/all-rag-strategies, adapted for interview prep and study.

## 1. Why this matters

A basic RAG pipeline is often enough for a demo, but production systems usually need extra retrieval strategies to improve precision, recall, and robustness. The repository highlights 11 practical patterns that are useful both in real systems and in technical interviews.

## 2. The 11 strategies at a glance

| Strategy | Core idea | Best for | Main tradeoff |
|---|---|---|---|
| Re-ranking | Retrieve a larger candidate set first, then re-rank with a stronger model | Precision-critical search | Extra latency and cost |
| Agentic RAG | Let an agent decide when to search, what to search, and when to use tools | Multi-step or tool-driven workflows | More complexity and less predictability |
| Knowledge Graphs | Combine vector search with entity/relationship lookup | Connected or relational knowledge | Higher setup and maintenance cost |
| Contextual Retrieval | Add document-level context to each chunk before embedding | Long documents with ambiguous chunks | More ingestion cost |
| Query Expansion | Rewrite or enrich the query before retrieval | Ambiguous or short queries | Extra LLM call |
| Multi-Query RAG | Run several query variations in parallel | Broad or vague questions | More retrieval calls |
| Context-Aware Chunking | Split text at meaningful structure boundaries instead of arbitrary lengths | Documents with headings, sections, tables | Slightly more complex ingestion |
| Late Chunking | Embed the full document first, then chunk embeddings | Preserve full-document context | More advanced implementation |
| Hierarchical RAG | Search small chunks but return parent context | Long documents with layered structure | Data model complexity |
| Self-Reflective RAG | Grade retrieval quality and retry with a refined query if needed | Hard or low-confidence queries | Highest latency |
| Fine-tuned Embeddings | Train embeddings on domain-specific data | Specialized domains like legal or medical | Requires training data and effort |

## 3. What each strategy means in practice

### 3.1 Re-ranking
- Use a fast first-pass retriever to get a candidate pool.
- Re-rank those candidates with a stronger model to improve relevance.
- Interview angle: this is a common upgrade from naive RAG to production-ready RAG.

### 3.2 Agentic RAG
- The system can decide to search, inspect a full document, call tools, or ask follow-up questions.
- Interview angle: useful when the task is not just “find a fact” but “solve a task”.

### 3.3 Knowledge Graphs
- Useful when relationships matter, such as entities, dependencies, and multi-hop reasoning.
- Interview angle: good answer when the dataset is highly interconnected.

### 3.4 Contextual Retrieval
- Each chunk gets a short explanation of the surrounding document so it becomes more self-contained.
- Interview angle: strong technique for retrieval failures caused by weak chunk semantics.

### 3.5 Query Expansion
- Expand a short query into a richer, more specific version before retrieval.
- Interview angle: useful when the original query is too sparse or ambiguous.

### 3.6 Multi-Query RAG
- Generate several query variants and search with all of them.
- Interview angle: helpful when the user question can be interpreted in multiple ways.

### 3.7 Context-Aware Chunking
- Split documents based on headings, paragraphs, and semantic boundaries.
- Interview angle: often better than fixed-size chunking for long, structured documents.

### 3.8 Late Chunking
- Preserve broad document context by embedding the full document and then deriving chunk embeddings.
- Interview angle: sophisticated approach when context preservation matters more than simplicity.

### 3.9 Hierarchical RAG
- Search over small child chunks, but return a larger parent chunk for context.
- Interview angle: good balance between precision and contextual completeness.

### 3.10 Self-Reflective RAG
- Retrieve first, evaluate whether the results are relevant, and retry with a refined query if they are weak.
- Interview angle: shows robustness and iterative reasoning.

### 3.11 Fine-tuned Embeddings
- Train embeddings on domain-specific examples to improve retrieval for niche tasks.
- Interview angle: strong when generic embeddings are not good enough.

## 4. Interview-ready summary

A strong answer for advanced RAG usually sounds like this:

1. Start with a basic RAG pipeline.
2. Improve retrieval quality with hybrid search and re-ranking.
3. Use better chunking and contextual enrichment for long documents.
4. Add query expansion or multi-query retrieval when the question is ambiguous.
5. Use agentic or graph-based methods only when the task is truly complex.
6. Evaluate faithfulness, relevance, latency, and cost.

## 5. Practical recommendations

- Use re-ranking first if you want a high-impact upgrade.
- Use contextual retrieval when chunk quality is poor.
- Use query expansion or multi-query only when needed, since they add cost.
- Prefer simple, explainable approaches unless the problem clearly demands more complexity.

## 6. Suggested study order

If you are preparing for interviews, study these in this order:

1. Re-ranking
2. Query Expansion
3. Multi-Query RAG
4. Context-Aware Chunking
5. Contextual Retrieval
6. Agentic RAG
7. Hierarchical RAG
8. Knowledge Graphs
9. Self-Reflective RAG
10. Fine-tuned Embeddings

## 7. Key takeaway

The main lesson from this repository is that RAG improves not just by adding an LLM, but by making retrieval smarter. In interviews, the best answers show that you understand the tradeoff between accuracy, latency, cost, and complexity.
