# ⚙️ Production — Cost & Latency Questions

> Priority: 🟡 Medium — tested at BCG, Cargill, UST production roles

---

**Q1. What is the cost/latency/quality tradeoff triangle in GenAI systems?**

Every GenAI system lives in a tradeoff between three constraints:
- **Quality** — better models cost more and are slower
- **Latency** — streaming and caching help, but retrieval + generation adds time
- **Cost** — LLMs charge per token; retrieval, embedding, and infra also cost money

You can't optimize all three simultaneously. The key is identifying which matters most for your use case and designing around it. A customer support chatbot prioritizes quality and latency. A batch document-processing pipeline prioritizes cost.

---

**Q2. What is multi-layer caching in a GenAI system?**

Three layers, applied in order before hitting the LLM:
1. **Response cache** — exact cache: same query → cached answer. Hash the query string.
2. **Semantic cache** — embed query, check similarity against cached queries. Similar query → cached answer.
3. **Retrieval cache** — cache the retrieved chunks for a given query, skip vector DB lookup on repeat.
4. **Prompt cache** — cache repeated system prompts at the API level (supported by Anthropic, OpenAI).

Applying all four can reduce LLM API costs by 40–80% in high-traffic systems.

---

**Q3. What should you log in a GenAI application?**

Every request should log:
- User query (anonymized if PII risk)
- Retrieved chunks (which documents, chunk IDs, similarity scores)
- Final prompt sent to LLM (for debugging prompt changes)
- LLM response
- Latency breakdown (retrieval time, LLM time, total)
- Token usage and cost per request
- Model and prompt version used
- User feedback (thumbs up/down)

This trace allows you to debug: "this answer was wrong — which retrieval chunk caused it?"

---

**Q4. How do you handle PII in a GenAI application?**

- Detect PII in user queries before sending to LLM (using NER or a PII detection model)
- Redact or pseudonymize before logging
- Scan LLM outputs for PII before returning to users
- Don't include PII in fine-tuning datasets
- Have a data retention policy for logs (auto-delete after N days)

---

**Q5. What is prompt compression and how does it reduce cost?**

Prompt compression removes redundant or low-information content from prompts while preserving meaning. Techniques: summarize verbose retrieved chunks before injecting them, remove boilerplate from system prompts, use shorter few-shot examples. Can reduce input tokens by 30–50% with minimal quality loss on structured tasks.

---

**Q6. How do you monitor a GenAI system in production?**

Track at two levels:
- **Technical metrics:** latency (p50, p95, p99), token usage/cost per request, error rate, cache hit rate, retrieval latency
- **Quality metrics:** faithfulness score (sampled), user satisfaction (thumbs up/down), task completion rate, hallucination rate (sampled)

Set up alerts on: latency spikes, cost anomalies (runaway token usage), quality degradation (faithfulness score drops), and error rate increases.
