---
marp: true
theme: gaia
paginate: true
title: "GraphRAG: Advancing Retrieval-Augmented Generation"
description: "An introduction to GraphRAG, its improvements over baseline RAG, and why it matters."
---

# GraphRAG:  
Advancing Retrieval-Augmented Generation

*Unlocking deeper knowledge with graphs*

---

## Baseline RAG

**RAG = Retrieval-Augmented Generation**

- Combines large language models (LLMs) with an external retrieval system
- Steps:
  1. **Query**: User input sent to retrieval module
  2. **Retrieve**: Most relevant documents ("chunks") retrieved from a corpus
  3. **Generate**: LLM generates answer conditioned on retrieved context

- Widely used for QA, chatbots, internal knowledge assistants

---

## Baseline RAG: Example

> **Question**: "Describe the benefits of Graph Neural Networks."

- **Retrieval**: Top 3 document chunks about Graph Neural Networks
- **Generation**: LLM reads chunks & produces an answer

---

## Shortcomings of Baseline RAG

- **Shallow Retrieval**: Only surfaces top text "chunks"; misses deeper connections
- **Limited Context**: Context sometimes fragmented or incomplete
- **No Relationship Awareness**: Can't connect data points not in the same chunk
- **Hallucination**: LLM might fabricate links or answers when info is spread across documents

---

## The Need for Deeper Retrieval

- Many questions require **integrating** facts or concepts scattered across sources
- Classic RAG retrieves isolated passages, not the relationships **between** them

---

## Introducing GraphRAG

**GraphRAG** = Graph-based Retrieval-Augmented Generation

- Enhances classic RAG by incorporating a structured knowledge graph
    - Nodes: Entities, concepts, or document chunks
    - Edges: Semantic relationships (e.g., "cites", "explains", "relates to")
- Integrates retrieval and generation with graph-structured information

---

## How Does GraphRAG Work?

1. **Build Knowledge Graph** from your corpus (documents, entities, relationships)
2. **Query** traverses the graph to identify relevant nodes AND their relationships
3. **Retrieval** gathers richer, connected context (not just top chunks)
4. **LLM Generation** now draws on both text and graph structure

---

## Benefits of GraphRAG

- **Richer Context**: Surfaces connected facts across documents
- **Relationship Awareness**: Reveals how concepts are linked
- **Reduced Hallucination**: LLM gets explicit relations, not just text blobs
- **Better Answers**: Especially for multi-hop, complex, or synthesis questions

---

## Example: GraphRAG vs Baseline RAG

**Baseline RAG:**
> *Finds three paragraphs about A and B separately — misses the fact they're related*

**GraphRAG:**
> *Finds A and B, plus an edge showing "A leads to B", improving the answer's accuracy*

---

## When to Use GraphRAG

- Precise Q&A over interrelated data
- Discovery/insight in complex domains (scientific, legal, enterprise knowledge)
- Any use case where **relationships** between facts matter

---

## Summary

- **Baseline RAG:** Easy to set up, but shallow and context-limited
- **GraphRAG:** Adds depth by connecting facts, reduces hallucination, and enables smarter systems

**Questions? Let's discuss!**

---
