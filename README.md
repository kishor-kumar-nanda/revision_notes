# 🚀 LangChain, LangGraph & Deep Agents — Production Reference Guide

A comprehensive, production-grade architectural reference and revision guide covering modern **LangChain (LCEL & Primitives)**, **LangGraph (State Machines & Orchestration)**, and **Deep Agents (Autonomous Harnesses)**.

## 📖 Overview

This repository hosts an interactive single-page reference guide (`index.html`) featuring:
- **46 Exhaustive Topics** with zero placeholders, full runnable code, and strict production libraries (`langchain_core`, `langgraph`, `langchain_qdrant`, `pydantic`, `psycopg_pool`).
- **3-Pillar Breakdown for Every Concept:**
  - 🟢 **The Modern Pattern:** How it is built in production.
  - 🔴 **The "Trash" Legacy Way:** Why older approaches (e.g., `AgentExecutor`, raw string prompts, naive memory) fail.
  - 🟡 **Scalability Impact:** How the pattern handles 10k RPS and distributed concurrency.
- **Side-by-Side Deep Agents ➔ LangGraph Mappings:** Complete translation of high-level Deep Agent patterns into explicit `StateGraph`, `TypedDict`, `Annotated`, `add_messages`, nodes, and conditional edges.
- **Developer Features:**
  - ☀️ Light Mode & 🌙 Dark Mode toggle (persisted via `localStorage`).
  - ☰ Full-Width Stacked View & ◫ Side-by-Side View toggle.
  - ↩ Line Wrap toggle for comfortable reading on all screen sizes.
  - 🔍 Instant fuzzy search filter across all classes, tools, and topics.
  - 📋 One-click copy buttons for all code blocks.

---

## 🗺️ Curriculum Structure

### Part 1: Pure LangChain (LCEL & Primitives — 26 Topics)
1. **Architecture & Package Separation** (`langchain-core` vs `langchain` vs partner packages)
2. **Chat Models & `init_chat_model`** (Multi-provider runtime swapping)
3. **Message Types & Multimodal** (`SystemMessage`, `ToolMessage`, multimodal content blocks)
4. **ChatPromptTemplate & MessagesPlaceholder** (Dynamic AST prompt compilation)
5. **Structured Outputs** (`with_structured_output` with Pydantic v2 schemas)
6. **Output Parsers** (`StrOutputParser`, `JsonOutputParser`, streaming chunks)
7. **LCEL Composition** (UNIX pipe `|`, `RunnableParallel`, `RunnablePassthrough.assign`)
8. **LCEL Resilience** (`with_retry` with backoff jitter, `with_fallbacks` cascading)
9. **Document Loaders** (Memory-safe `lazy_load` generators)
10. **Semantic Text Splitters** (`RecursiveCharacterTextSplitter`, code-aware splitters)
11. **Embeddings & Caching** (`OpenAIEmbeddings`, `CacheBackedEmbeddings` KV store)
12. **Production Vector Stores** (Qdrant with HNSW, MMR diversity search)
13. **Hybrid Search** (`EnsembleRetriever` BM25 + Dense vector with RRF fusion)
14. **ParentDocumentRetriever** (Small-to-big retrieval: small chunks for search, full parent context for LLM)
15. **Self-Querying Retriever** (Natural language to structured vector metadata filters)
16. **Contextual Compression & Rerankers** (`ContextualCompressionRetriever` + Cross-Encoder)
17. **Document Indexing API** (`langchain.indexes.index` + `SQLRecordManager` deduplication & sync)
18. **Tools & Tool Calling** (`@tool` decorator, `bind_tools`, `ToolMessage` contracts)
19. **Stateful Session History** (`RunnableWithMessageHistory` + session store)
20. **Caching Layer** (`set_llm_cache` with In-Memory & Redis backends)
21. **Observability & Callbacks** (`AsyncCallbackHandler` token telemetry & latency profiling)
22. **Event Streaming** (`astream_events` version 2 with granular lifecycle hooks)
23. **Dynamic Runtime Config** (`configurable_fields` & `ConfigurableField` overrides)
24. **Semantic Few-Shot** (`SemanticSimilarityExampleSelector` dynamic in-context learning)
25. **Message Trimming** (`trim_messages` context window protection)
26. **End-to-End RAG Blueprint** (Unified LCEL pipeline with sources and citations)

---

### Part 2: LangGraph Core Orchestration (12 Topics)
1. **Graph Architecture vs Linear Chains** (Why `AgentExecutor` was deprecated)
2. **State & Custom Reducers** (`TypedDict`, `Annotated`, `add_messages`, custom list appenders)
3. **ToolNode & `tools_condition`** (Automated tool call parsing and execution)
4. **Custom ReAct Loop from Scratch** (Manual agent node, tool node, cycles, zero shortcuts)
5. **Persistence & Checkpointers** (`AsyncPostgresSaver` with connection pools & `thread_id`)
6. **Human-in-the-Loop** (Dynamic `interrupt()` & `Command(resume=...)` approval gates)
7. **Multi-Agent Supervisor Pattern** (Central router coordinating specialized worker agents)
8. **Subgraphs & State Isolation** (Modular nested graphs with private state boundaries)
9. **Streaming Modes** (`stream_mode="updates"|"values"|"messages"`)
10. **Store API** (`AsyncPostgresStore` for cross-thread user preferences)
11. **Time-Travel & Debugging** (`get_state_history`, state replay, and historical forking)
12. **Production Hardening** (PostgreSQL pool sizing, MsgPack security, transaction isolation)

---

### Part 3: Deep Agents ➔ LangGraph Mappings (8 Direct Blueprints)
1. **Sandbox Execution Backend** (`VercelSandbox` ephemeral execution inside a LangGraph Node)
2. **Virtual Filesystem (VFS) & Offloading** (Offloading 10k+ token outputs to disk/S3 with pointer summaries)
3. **Dynamic Planning & Todo Lists** (Plan-and-Execute state machine with `todos: list[dict]`)
4. **Sub-Agent Spawning with Context Isolation** (Parallel child subgraph dispatch via `asyncio.gather`)
5. **Middleware & PII Scrubbing** (Pre-model sanitization node redacting PII before API egress)
6. **MCP (Model Context Protocol) Integration** (Dynamic tool server discovery mapped to `ToolNode`)
7. **Guardrails & Safety Routing** (Fail-closed conditional edges blocking prompt injections)
8. **Frontend `useStream` & Event Telemetry** (FastAPI SSE event stream powering React hooks)

---

## 🖥️ How to View

Open `index.html` directly in any web browser:
```bash
# macOS
open index.html

# Linux
xdg-open index.html

# Windows
start index.html
```

Or deploy to **GitHub Pages** (Settings ➔ Pages ➔ Source: `Deploy from branch main / root`).
