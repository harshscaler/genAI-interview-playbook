# 🏗️ System Design — Interview Questions

> Priority: 🔴 High — tested at Happiest Minds, BCG, Cargill, and general senior GenAI rounds

---

**Q1. Design a production-ready GenAI application architecture end-to-end.**

Layers needed:
```
User → UI → API Gateway → Auth → Orchestration Layer
                                        ↓
                              [LLM] ← [RAG Retrieval]
                                        ↓
                           Safety Layer → Observability → Feedback Loop
```

Key components:
- Rate limiting and cost controls at the API gateway
- Prompt versioning (treat prompts like code)
- Semantic caching before hitting the LLM
- Fallback models (if primary LLM is down, route to backup)
- Input/output safety scanning
- Full trace logging for every request
- Human escalation path for low-confidence answers

---

**Q2. Design a conversational AI agent for an enterprise knowledge base.**

This is the most common 2026 GenAI system design prompt. Cover:
- RAG pipeline for document retrieval (see RAG questions)
- Conversation memory (short-term in context, long-term in vector store)
- Tool use for live data (e.g., database lookup, API calls)
- Multi-turn conversation management
- Access control — different users see different documents
- Audit logging for compliance
- Fallback to human agent when confidence is low

---

**Q3. How would you reduce latency in a GenAI system?**

In order of impact:
1. **Streaming** — start sending tokens to the user immediately (SSE), don't wait for full response
2. **Semantic caching** — return cached answers to similar queries, skip LLM entirely
3. **Prompt caching** — cache repeated system prompts at the API level
4. **Model right-sizing** — use a smaller/faster model for simple queries
5. **Async tool calls** — run independent tool calls in parallel
6. **Reduce context length** — pass fewer, more targeted chunks
7. **Quantization** — use quantized models for inference (faster, smaller)

Measure p95 and p99 latency, not just averages.

---

**Q4. How would you design a multi-tenant GenAI system with data isolation?**

- Store each tenant's documents separately with tenant_id metadata in the vector DB
- Add tenant_id as a mandatory filter on every similarity search — never search across tenant boundaries
- Encrypt embeddings at rest per tenant
- Separate API keys per tenant for the LLM provider
- Audit log every query with tenant_id, user_id, and retrieved document IDs
- Rate limit per tenant to prevent one tenant starving others

---

**Q5. How do you handle traffic spikes in a GenAI system?**

- Queue bursty workloads with an async task queue (Celery, SQS) — don't call LLM APIs synchronously under spike
- Implement adaptive retry with jitter and backoff — don't hammer provider on rate limit errors
- Pre-scale compute during predictable peak times
- Use semantic caching aggressively — spikes often involve similar queries
- Implement graceful degradation — fall back to a faster/cheaper model under extreme load

---

**Q6. Design a document-processing pipeline for unstructured data (PDFs, emails, images).**

```
Input → Parser → Cleaner → Chunker → Embedder → Vector DB
                                                      ↓
                                              Query Pipeline
```

- PDFs: use PyMuPDF or pdfplumber for text extraction, handle tables and images separately
- Emails: parse MIME, extract body text, preserve thread context
- Images: use a multimodal model or OCR (Tesseract) for text extraction
- Normalize all content to clean text before chunking
- Store original source format metadata alongside embeddings for citation

---

**Q7. What is model tiering / routing and how do you implement it?**

Route queries to different models based on complexity:
- Simple, well-defined queries → small fast model (e.g., GPT-4o-mini, Haiku)
- Complex reasoning, ambiguous queries → large capable model (e.g., GPT-4o, Sonnet)

Implementation: a classifier (or even a simple rule) decides the tier before calling the LLM. If the small model returns low-confidence output (e.g., "I don't know"), escalate to the large model. This can reduce cost by 60–80% in systems with mixed query complexity.
