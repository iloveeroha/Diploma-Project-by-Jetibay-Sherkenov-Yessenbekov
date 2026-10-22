<!-- File: docs/05-technology-comparison.md -->
# Key Technology Decisions & Comparisons

## 1. Overview
In accordance with system requirements, three foundational architectural decisions were subjected to structured trade-off evaluations:
1. **Decision 1: Application Server & API Framework**
2. **Decision 2: Persistent Storage, Search, & Queue Coordination**
3. **Decision 3: Core AI Speech & LLM Runtime Stack**

---

## 2. Decision 1: Application Server & API Platform

### 2.1 Alternatives Considered
* **Alternative A: Python (FastAPI + Pydantic v2 + Uvicorn)**
* **Alternative B: Go (Golang with Gin / Fiber)**
* **Alternative C: Node.js / TypeScript (NestJS + Fastify)**

### 2.2 Comparison Matrix

| Evaluation Criteria | Alternative A: FastAPI (Python) | Alternative B: Gin/Fiber (Go) | Alternative C: NestJS (Node.js) |
|---|---|---|---|
| **Ecosystem Synergy with AI Stack** | **Native (Direct shared models, PyTorch, NumPy)** | Poor (Requires CGO or IPC bridges) | Weak (Subprocess/gRPC calls needed) |
| **Contract Generation & Typing** | **Native Pydantic v2 -> OpenAPI JSON** | Struct tags / Swagger CLI tools | Decorators / TypeScript reflection |
| **I/O & Async Concurrency** | High (asyncio event loop) | Exceptional (Goroutines) | High (V8 event loop) |
| **Developer Velocity & Team Skills** | High (Primary competence across Tracks A & C) | Medium (Steeper learning curve) | Medium |
| **SSE & Streaming Support** | **Built-in `StreamingResponse`** | Native channels | Native stream pipes |

### 2.3 Rationale & Selection
**Selected: Alternative A (FastAPI).**  
FastAPI provides optimal balance between high asynchronous I/O performance and native interoperability with Python's data/AI ecosystem. Pydantic v2 facilitates compile-time type safety and automatically generates `/openapi.json`, from which Track B generates typed TypeScript API clients. This eliminates schema drift between backend and frontend.

---

## 3. Decision 2: Data Storage, Search Engine, & Job Queue

### 3.1 Alternatives Considered
* **Alternative A: PostgreSQL 18 (Single Storage, Queue via `SKIP LOCKED`, `pg_trgm` Search)**
* **Alternative B: PostgreSQL (Data) + Redis (Queue) + Elasticsearch / Qdrant (Search)**
* **Alternative C: SQLite + Celery + RabbitMQ**

### 3.2 Comparison Matrix

| Evaluation Criteria | Alternative A: PostgreSQL 18 Unified | Alternative B: Polyglot (PG + Redis + ES) | Alternative C: SQLite + RabbitMQ |
|---|---|---|---|
| **Infrastructure Footprint** | **Minimal (1 single container/process)** | Heavy (3-4 separate memory-hungry daemons)| Medium |
| **Transactional Consistency** | **ACID (Meeting creation + Job enqueue in 1 txn)**| Eventual consistency / 2PC risks | Weak concurrency on SQLite |
| **Full-Text & Trigram Search** | **Built-in `pg_trgm` (multilingual fuzzy search)**| Superior full-text/vector capability | Basic FTS5 |
| **Backup & Disaster Recovery** | **Trivial (`pg_dump` covers DB, logs, and queue)** | Complex distributed state backups | Fragmented files |
| **Job Queue Mechanics** | **Native `FOR UPDATE SKIP LOCKED` + SSE NOTIFY** | Redis Pub/Sub + Celery worker | AMQP protocol broker |

### 3.3 Rationale & Selection
**Selected: Alternative A (PostgreSQL 18 Unified).**  
For on-premises deployment on a single server, minimizing operational complexity is critical. PostgreSQL 18 handles relational schemas, transactional job locking (`FOR UPDATE SKIP LOCKED`), real-time event distribution (`LISTEN/NOTIFY`), and tri-lingual trigram search (`pg_trgm`) within a single ACID-compliant engine. This eliminates distributed synchronization bugs and simplifies cold backup automation to a single nightly cron task.

---

## 4. Decision 3: Speech Processing & Local LLM Engine

### 4.1 Alternatives Considered
* **Alternative A: Faster-Whisper (CTranslate2) + PyAnnote 3.1 + Ollama / llama.cpp (Open-Weight)**
* **Alternative B: Vanilla OpenAI Whisper (PyTorch) + SpeechBrain + vLLM**
* **Alternative C: Whisper.cpp + LocalAI**

### 4.2 Comparison Matrix

| Evaluation Criteria | Alternative A: Faster-Whisper + PyAnnote + Ollama | Alternative B: Vanilla Whisper + vLLM | Alternative C: Whisper.cpp + LocalAI |
|---|---|---|---|
| **Transcription Inference Speed** | **Fast (CTranslate2 INT8 optimization)** | Slow (PyTorch FP32/FP16 unoptimized) | Fast (C++ AVX/Metal/CUDA) |
| **Diarization Precision (DER)** | **State-of-the-art (<12% DER via PyAnnote 3.1)** | Moderate (SpeechBrain clustering) | Naive energy/spectrogram clustering |
| **LLM Structured Output / JSON Schema** | **Strict enforcement via Ollama/llama.cpp grammars** | Guided decoding via outlines/vLLM | Partial grammar support |
| **VRAM Footprint** | **Balanced (~6-8 GB for ASR + Diarization + 7B LLM)**| High (>16 GB VRAM needed for vLLM) | Minimal (~4-6 GB) |
| **Automated CI/CD Mockability** | **Clean Python Protocols (`ports.py` + `fakes.py`)** | Difficult without CUDA GPU | C-library wrapping complexity |

### 4.3 Rationale & Selection
**Selected: Alternative A.**  
Faster-Whisper delivers up to 4x throughput improvements over raw PyTorch implementations. Ollama / llama.cpp allows running modern quantized models (Qwen-2.5-7B-Instruct or Llama-3-8B-Instruct) while enforcing deterministic JSON schema validation via GBNF grammars. Decoupling these components behind Python `Protocol` interfaces ensures that tests and CI can execute without GPU hardware using zero-overhead mock engines (`fakes.py`).