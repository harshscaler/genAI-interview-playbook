# 🧠 LLM Foundations — Interview Questions

> Priority: 🔴 High — tested at Eightfold AI, Happiest Minds, BCG, and general GenAI screening rounds

---

## Questions & Answers

**Q1. What is the difference between traditional AI and generative AI?**

Traditional AI systems are trained to classify, predict, or optimize over a fixed output space — for example, classifying an email as spam or predicting house prices. Generative AI systems produce new content (text, images, code) by learning the underlying distribution of training data. The core shift is from discriminative models that answer "which category?" to generative models that answer "what comes next?"

---

**Q2. What is a token? Why does tokenization matter for LLMs?**

A token is the smallest unit of input an LLM processes — it can be a word, a subword, or punctuation. Tokenization converts raw text into numerical IDs the model can process. It matters because: (a) context windows are measured in tokens, not words — exceeding them truncates input, and (b) the tokenizer determines how the model "sees" rare or technical words. Poor tokenization for specialized domains (legal, medical) can hurt model performance.

---

**Q3. What are the differences between BPE, WordPiece, and character-level tokenization?**

BPE (Byte Pair Encoding) — used by GPT models. Iteratively merges the most frequent character pairs to build a vocabulary. Balances vocabulary size and OOV handling well.

WordPiece — used by BERT. Similar to BPE but chooses merges that maximize training data likelihood rather than frequency. Better for understanding tasks.

Character-level — operates on individual characters. No OOV problem but very long sequences and loses semantic meaning in individual tokens.

---

**Q4. What are embeddings and how do they capture meaning?**

Embeddings are dense, continuous vector representations of tokens. They map discrete tokens into a high-dimensional space where semantically similar words are close together. The embedding layer converts token IDs into vectors the model processes. In retrieval contexts, separate embedding models (like text-embedding-3-small) convert full sentences or documents into vectors for similarity search — these are NOT the same as the LLM's internal embeddings.

---

**Q5. What are positional encodings and why do transformers need them?**

Transformers process all tokens in parallel through self-attention, which makes them unaware of token order by default. Positional encodings add order information by injecting a position-dependent signal into each token's embedding. Modern models use Rotary Positional Embeddings (RoPE) which handle long-context windows well and are compatible with FlashAttention.

---

**Q6. What is self-attention? Explain it simply.**

Self-attention lets each token in a sequence look at every other token and decide how much to "attend to" it when forming its representation. For each token, we compute Query (what am I looking for?), Key (what do I offer?), and Value (what do I actually contribute?). Attention scores = softmax(Q·Kᵀ / √d), then multiply by V. This lets the model capture long-range dependencies — "bank" in "river bank" attends differently to surrounding words than "bank" in "savings bank."

---

**Q7. What is multi-head attention and why does it help?**

Multi-head attention runs self-attention multiple times in parallel with different learned projections (heads), then concatenates results. Each head can learn to attend to different relationships simultaneously — one head might focus on syntactic structure, another on semantic similarity. This gives the model richer, more expressive representations than a single attention head.

---

**Q8. What is the difference between encoder-only, decoder-only, and encoder-decoder models?**

Encoder-only (e.g., BERT) — processes the full input bidirectionally, sees all tokens at once. Best for understanding tasks: classification, NER, embeddings.

Decoder-only (e.g., GPT, Llama, Claude) — generates one token at a time, can only attend to previous tokens (causal masking). Best for generation tasks and now dominant for most tasks in 2026.

Encoder-decoder (e.g., T5, BART) — encoder processes input, decoder generates output. Best for seq2seq tasks: translation, summarization.

---

**Q9. Why are decoder-only models dominant even for non-generation tasks in 2026?**

Decoder-only models benefit from the KV Cache during inference — previously computed key-value pairs are cached and reused, dramatically speeding up generation. BERT-style bidirectional encoders can't use KV Cache because they need to attend to the full sequence. At scale, this inference efficiency advantage is enormous. Additionally, instruction tuning has made decoder-only models capable of almost any task.

---

**Q10. What is a context window and what happens when you exceed it?**

The context window is the maximum number of tokens (input + output) an LLM can process in a single call. When exceeded, earlier tokens are truncated — the model loses earlier context. In RAG systems, this makes chunking critical: you can't feed a 500-page PDF directly into an LLM.

---

**Q11. What is the difference between pre-training, fine-tuning, and instruction tuning?**

Pre-training — training on massive unlabeled text data to predict the next token. Produces a "base" model that completes text.

Fine-tuning — further training on a smaller task-specific labeled dataset to specialize the model.

Instruction tuning (SFT) — fine-tuning on (instruction, response) pairs to teach the model to follow instructions rather than just complete text. Produces an "instruct" or "chat" model.

---

**Q12. What is RLHF?**

Reinforcement Learning from Human Feedback. After SFT, humans rank model outputs by quality. A "reward model" is trained on these rankings. The LLM is then fine-tuned using RL to maximize the reward model's score, aligning the model's outputs with human preferences. DPO (Direct Preference Optimization) is a simpler alternative that achieves similar results without a separate reward model.

---

**Q13. What is LoRA and why is it used?**

Low-Rank Adaptation (LoRA) is a parameter-efficient fine-tuning (PEFT) method. Instead of updating all model weights during fine-tuning, it trains small low-rank matrices added to each layer. This reduces GPU memory requirements drastically. A company can maintain separate LoRA adapters for different use cases (finance, HR, customer support) without storing multiple full model copies.

---

**Q14. What is quantization?**

Reducing the numerical precision of model weights — for example, from FP32 to INT8 or INT4. This reduces model size, memory usage, and inference cost/latency with acceptable quality loss for most tasks. QLoRA combines LoRA fine-tuning with 4-bit quantization to fine-tune large models on consumer hardware.

---

**Q15. What is the KV Cache and how does it speed up inference?**

During autoregressive generation, the model recomputes Key and Value matrices for all previous tokens at each step — this is expensive. The KV Cache stores these pre-computed K and V matrices and reuses them, so each new token generation only needs to compute K, V for the new token. This makes generation significantly faster, especially for long outputs.
