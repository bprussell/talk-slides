---
theme: the-unnamed
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## Harry T
  RAG-Enabled Legal Chatbot - Pension Fund of the Christian Church
drawings:
  persist: false
transition: slide-left
title: 'Harry T - RAG-Enabled Legal Chatbot'
mdc: true
---

# Harry T

**RAG-Enabled Legal Chatbot**

<div class="pt-6">
  <span class="text-lg">Pension Fund of the Christian Church</span>
</div>

---
layout: default
---

# The Original Concept

## Microsoft Copilot Studio POC

**Initial Plan:**
- Proof of concept using Microsoft Copilot Studio
- Document store in SharePoint

**The Problem:**
Copilot Studio lacked the configuration options needed to implement RAG effectively

**The Solution:**
Build a custom solution with proper RAG capabilities

---
layout: default
---

# Solution Architecture

<div class="grid grid-cols-2 gap-6 text-sm">

<div>

## AI & Search
- **LLM**: GPT-4.1 + GPT-4.1-mini
- **Embeddings**: text-embedding-3-small (1536d)
- **Vector Database**: Pinecone (cloud)
- **Text Processing**: LangChain splitter

## User Interface
- **Platform**: Microsoft Teams
- **Framework**: M365 Agents Toolkit (Teams AI SDK)

</div>

<div>

## Document Processing
- **Storage**: Azure Blob Storage
- **Indexing**: Azure Functions (serverless)
- **Formats**: PDF, DOCX, PPTX, TXT, MSG

## Monitoring & Admin
- **Operations**: Azure Table Storage
- **Dashboard**: FastAPI

</div>

</div>

---
layout: default
---

# Document Indexing Pipeline

## Two Content Sources

<div class="grid grid-cols-2 gap-6">

<div>

### Blob Storage Documents
- PDF, DOCX, PPTX, TXT, MSG
- Legacy DOC/PPT formats
- **Trigger**: Azure Function (blob upload)
- **Processing**: Immediate

</div>

<div>

### Website Scraping
- pensionfund.org via sitemap
- Linked PDFs auto-discovery
- **Trigger**: Weekly timer
- **Processing**: Incremental (only new/changed)

</div>

</div>

## Processing Pipeline

1. **Text Extraction** - Format-specific extractors
2. **Chunking** - RecursiveCharacterTextSplitter (1000 chars, 200 overlap)
3. **Embeddings** - OpenAI text-embedding-3-small
4. **Pinecone Upsert** - Store with metadata (chunk, full_text, title, source_type)
5. **Metadata** - Track source, timestamp, parent document ID

---
layout: default
---

# Query Flow Overview

<div class="pt-4 pb-4 px-4">

<div class="flex justify-between items-start mb-6">
  <!-- USER QUESTION aligned with PRE-PROCESS -->
  <div class="flex-1 mx-2 text-center">
    <div class="text-sm opacity-75">User Question</div>
    <div class="text-xl mt-2">↓</div>
  </div>
  <!-- Spacers -->
  <div class="text-2xl px-3 opacity-0">→</div>
  <div class="flex-1 mx-2"></div>
  <div class="text-2xl px-3 opacity-0">→</div>
  <div class="flex-1 mx-2"></div>
</div>

<div class="flex justify-between items-center mb-8">
  <!-- PRE-PROCESS -->
  <div class="border border-blue-400 bg-blue-400 bg-opacity-10 rounded-lg p-5 text-center flex-1 mx-2">
    <div class="text-xs opacity-60 tracking-wide">PHASE 1</div>
    <div class="font-semibold text-sm mt-1">PRE-PROCESS</div>
    <div class="text-xs mt-3 space-y-2 opacity-80">
      <div>Classify</div>
      <div>HyDE Gen</div>
    </div>
  </div>

  <div class="text-2xl text-gray-500 px-3">→</div>

  <!-- RETRIEVAL -->
  <div class="border border-green-400 bg-green-400 bg-opacity-10 rounded-lg p-5 text-center flex-1 mx-2">
    <div class="text-xs opacity-60 tracking-wide">PHASE 2</div>
    <div class="font-semibold text-sm mt-1">RETRIEVAL</div>
    <div class="text-xs mt-3 space-y-2 opacity-80">
      <div>Search</div>
      <div>Re-rank</div>
    </div>
  </div>

  <div class="text-2xl text-gray-500 px-3">→</div>

  <!-- REFINEMENT -->
  <div class="border border-purple-400 bg-purple-400 bg-opacity-10 rounded-lg p-5 text-center flex-1 mx-2">
    <div class="text-xs opacity-60 tracking-wide">PHASE 3</div>
    <div class="font-semibold text-sm mt-1">REFINEMENT</div>
    <div class="text-xs mt-3 space-y-2 opacity-80">
      <div>Extract</div>
      <div>Synthesize</div>
    </div>
  </div>
</div>

<div class="flex justify-between items-end mt-6">
  <!-- Spacers -->
  <div class="flex-1 mx-2"></div>
  <div class="text-2xl px-3 opacity-0">→</div>
  <div class="flex-1 mx-2"></div>
  <div class="text-2xl px-3 opacity-0">→</div>
  <!-- RESPONSE aligned with REFINEMENT -->
  <div class="flex-1 mx-2 text-center">
    <div class="text-xl mb-2">↓</div>
    <div class="text-sm opacity-75">Response to User</div>
  </div>
</div>

</div>

---
layout: default
---

# Question Classification

<div class="text-sm">

**GPT-4.1-mini** classifies the question into one of 5 types:

- **`yes_no`** - Balanced positive/negative hypotheticals
- **`capability`** - Implementation status hypotheticals
- **`procedural`** - Comprehensive procedure hypotheticals
- **`data_lookup`** - Skips HyDE (better for tables & numbers)
- **`informational`** - Standard hypothetical answers

This classification determines the retrieval strategy for that specific query.

</div>

---
layout: default
---

# HyDE Generation

<div class="text-sm">

**GPT-4.1** generates hypothetical answers based on the question type from classification

### Type-Specific Hypotheticals
- **yes_no questions** → Hypothetical pros and cons
- **capability questions** → Hypothetical feature status
- **procedural questions** → Hypothetical step-by-step processes
- **informational questions** → Hypothetical answer summaries

### Why HyDE?
Embedding a complete hypothetical answer is often closer to relevant documents than the sparse question text itself

</div>

---
layout: default
---

# Multi-Query Search

<div class="text-sm">

Instead of searching once, we search **three times** with different embeddings:

1. **HyDE Result** - The hypothetical answer(s) from HyDE generation
2. **Original Query** - The user's actual question
3. **Simplified Query** - A stripped-down version of the question

### Merging & Boosting
Results are merged and documents found by **multiple searches are boosted** in ranking - they're likely more relevant.

</div>

---
layout: default
---

# Advanced Re-ranking

<div class="text-sm">

### Title Boosting
Multi-word title matches weighted higher

### Diversity Filtering
Avoid near-duplicate results

### Data Lookup Special Handling
- Retrieve top-30 (vs top-10)
- Exponential title boosting
- Re-rank to top-10
- Better for tables & numbers

</div>

---
layout: default
---

# Extraction

<div class="text-sm">

**GPT-4.1** extracts information from all retrieved documents

### Process
- XML-formatted context sent to GPT-4.1
- Prompt: "Extract ALL relevant info from ALL documents"
- Output: Structured JSON with citations per fact

### Goal
Gather complete information without filtering - we'll filter in the next stage

</div>

---
layout: default
---

# Refinement

<div class="text-sm">

**GPT-4.1** synthesizes extraction results into a concise response

### Process
- Takes all extracted information
- Removes contradictions
- Combines duplicate findings
- Preserves all citation markers [1], [2], etc.
- Temperature=0 for data_lookup (prevents number hallucination)

### Goal
Balance completeness with readability

</div>

---
layout: default
---

# Citation Handling

<div class="text-sm">

Citations are generated differently based on document source:

### Blob Storage Documents
- Auto-generate SAS URLs
- 24-hour expiry for security
- Direct download links

### Website Content
- Use direct public URLs
- No auth required

### Citation Preview
- Display relevant snippet with each citation
- Help users verify the answer

</div>

---
layout: default
---

# Operation Tracking

<div class="text-sm">

## Unique Operation IDs
- Every query gets a UUID `operation_id`
- Tracks full pipeline: Classification → Retrieval → Generation → Refinement → Feedback
- Stored in Azure Table Storage

## User Feedback Loop
- Thumbs up/down reactions in Microsoft Teams
- Each reaction correlated with its `operation_id`
- Enables analysis of what works and what doesn't
- Drives continuous improvement of the system

</div>

---
layout: default
---

# Admin Dashboard

<div class="text-sm">

**FastAPI-based monitoring and analytics**

- View all RAG operations in real-time
- Analyze feedback patterns and trends
- Monitor performance metrics
- Correlate user feedback with specific operations

</div>

