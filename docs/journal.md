## Week 7 — Issue Selection

**Issue:** [#34 — Implement a re-ranking step that uses an LLM to score retrieved chunks before generation](https://github.com/ascherj/pathreview/issues/34)

**Problem Summary:**

Issue: Add an LLM-based re-ranking step to the RAG retrieval pipeline.

Current behavior: `rag/retriever/hybrid.py` ranks retrieved chunks using vector similarity and keyword scores only. There's no semantic relevance check, so numerically high-ranked chunks may still be off-topic.

Desired behavior: After hybrid retrieval, an optional re-ranking pass prompts a smaller LLM to score each chunk's relevance to the query, then passes only the top-k re-ranked chunks to the generator.

Scope: New module `rag/retriever/reranker.py` for the scoring logic, plus a modification to `hybrid.py` to call it as an optional step. Tier 3 — touches how retrieval and generation connect.

Why it matters: Filters out chunks that pass vector/keyword thresholds but are semantically irrelevant, improving feedback quality without adding a heavier model to the always-on path.
