<!-- File: docs/07-architecture.md -->
# System Architecture & Component Design

## 1. Architectural Overview & Security Isolation
The **Local AI Meeting Assistant** is deployed as an on-premises, single-server system orchestrated via Docker Compose. The architecture prioritizes zero-trust network segregation, transactional queue integrity, and modular AI pipeline extensibility.

### 1.1 Network Segmentation Topology
The system enforces strict boundary isolation using three Docker networks:
1. **`EDGE` (External Ingress):** Exposes only ports 80/443 via Caddy reverse proxy. Enforces TLS termination, HSTS, security headers, rate limiting, and request size caps (max 500 MB).
2. **`APP` (Internal Network):** Private network containing the FastAPI application server, PostgreSQL 18 database, and persistent file volume storage. Direct external traffic is blocked.
3. **`AI` (Air-Gapped Processing Network):** Isolated internal bridge network (`internal: true`) hosting the Python AI Worker and the local LLM runtime (Ollama/llama.cpp). Containers on this network have **no default gateway** and cannot access the public internet.

[ Clients: Browser React 19 SPA ]
│ (HTTPS / 443)
▼
┌───────────────────────┐
│  EDGE: Caddy Proxy    │
└──────────┬────────────┘
│ (HTTP /api & SSE)
▼
┌────────────────────────────────────────────────────────┐
│  APP Network                                           │
│   ┌────────────────────────┐  Claim  ┌──────────────┐  │
│   │  API: FastAPI (Python) │ ◄─────► │ PostgreSQL18 │  │
│   └───────────┬────────────┘ (SKIP   │ (Jobs/Audit) │  │
│               │              LOCKED) └──────▲───────┘  │
│               ▼                             │          │
│       ┌───────────────┐                     │          │
│       │ File Storage  │                     │          │
│       │ (WAV / Audio) │                     │          │
│       └───────▲───────┘                     │          │
└───────────────┼─────────────────────────────┼──────────┘
│ Stream Audio                │ State & Runs
┌───────────────┼─────────────────────────────┼──────────┘
│  AI Network   │                             │
│   ┌───────────┴────────────┐  HTTP Prompt   ┌──────────────┐
│   │ AI Worker (Python)     │ ─────────────► │ LLM Runtime  │
│   │ (VAD/ASR/Diar/Align)   │ ◄───────────── │ (Ollama)     │
│   └────────────────────────┘  JSON Schema   └──────────────┘
│   (internal: true - ZERO outbound internet traffic)     │
└─────────────────────────────────────────────────────────┘


---

## 2. End-to-End Processing Scenario
1. **Upload & Verification:** Client streams media file via HTTPS. Caddy proxies to FastAPI `/meetings`. The `media` module verifies magic bytes, computes SHA-256, streams chunks to local volume storage, and commits meeting record.
2. **Atomic Job Enqueue:** In the same database transaction, an asynchronous task entry is inserted into `jobs` table with status `PENDING`.
3. **Live Progress Subscription:** The client connects to `GET /meetings/{id}/events` via Server-Sent Events (SSE). FastAPI subscribes to PostgreSQL `LISTEN/NOTIFY` channels.
4. **Queue Claiming:** The background AI Worker executes `SELECT ... FOR UPDATE SKIP LOCKED` on the `jobs` table. This guarantees safe, race-free concurrency across multiple worker instances.
5. **AI Pipeline Execution:**
   * `preprocess`: Normalizes audio to WAV 16 kHz mono via `ffmpeg`.
   * `vad`: Detects speech regions, stripping dead silence (Silero VAD).
   * `asr`: Transcribes word tokens with timestamps and segment language (Faster-Whisper).
   * `diarization`: Computes speaker activity turns and embeddings (PyAnnote.audio).
   * `alignment`: Aligns words with speaker turns via maximal temporal overlap.
   * `chunking`: Breaks transcript into token-bounded dialogue chunks.
   * `summarize`: Executes Map-Reduce summarization using Ollama with strict JSON schemas.
   * `extract`: Generates candidate action items with explicit quotes and assignees.
   * `validate`: Deterministically validates that each quote exists in the segment text, normalizes relative dates against meeting timestamp, and eliminates duplicates.
6. **Completion & SSE Emission:** Worker saves segments, speakers, summaries, and action items to DB. A `NOTIFY` event fires, pushing completion status to the browser UI.

---

## 3. Subsystem Breakdown (49 Modules Overview)

### 3.1 Backend API Subsystem (`src/api`, Track A) — 14 Modules
* `API-01 (core)`: Environment settings, DB session engine, security guards, structured logging.
* `API-02 (auth)`: JWT issuance, refresh token rotation, brute-force lockout.
* `API-03 (users/admin)`: User lifecycle, role management, workspace retention configs.
* `API-04 (meetings)`: Meeting CRUD, filtering, pagination, workspace isolation.
* `API-05 (media)`: Stream-upload handler, magic bytes & ffprobe verification, SHA-256 computation.
* `API-06 (jobs)`: Atomic job enqueue, cancellation, retry/regenerate, SSE event forwarding.
* `API-07 (transcripts)`: Segment & speaker retrieval, manual text correction preserving originals.
* `API-08 (summaries)`: Versioned summary retrieval.
* `API-09 (action_items)`: Task listing, state transitions (Accepted/Rejected), evidence linking.
* `API-10 (search)`: Full-text and trigram search (`pg_trgm`) across meeting corpus.
* `API-11 (export)`: Protocol generation into DOCX, PDF, Markdown, and JSON.
* `API-12 (audit)`: Append-only event logger (`audit.record()`).
* `API-13 (health)`: Liveness (`/healthz`), readiness (`/readyz`), Prometheus metrics (`/metrics`).
* `API-14 (retention_job)`: Scheduled background task pruning expired meetings and audio files.

### 3.2 AI Worker Subsystem (`src/worker`, Track C) — 14 Modules
* `WRK-01 (runner)`: Job polling loop, state transitions, backoff retry, failure diagnosis.
* `WRK-02 (ports)`: Clean Architecture `Protocol` classes (`Transcriber`, `Diarizer`, `Summarizer`, `Storage`).
* `WRK-03 (preprocess)`: Audio conversion and volume normalization via `ffmpeg`.
* `WRK-04 (vad)`: Voice activity detection and speech timestamp segmentation.
* `WRK-05 (asr)`: Faster-Whisper adapter producing word-level timestamps.
* `WRK-06 (diarization)`: PyAnnote 3.1 speaker clustering adapter.
* `WRK-07 (alignment)`: Pure-Python deterministic word-to-speaker alignment algorithm.
* `WRK-08 (chunking)`: Overlapping context window chunker preserving speaker/timestamp tags.
* `WRK-09 (summarize)`: Map-Reduce summary adapter with Pydantic output validation.
* `WRK-10 (extract)`: Candidate action item extractor with quote attribution.
* `WRK-11 (validate)`: Programmatic quote verifier and relative date resolver.
* `WRK-12 (adapters)`: Concrete implementations (`faster_whisper.py`, `pyannote.py`, `ollama.py`, `fakes.py`).
* `WRK-13 (runs)`: Hardware, model digest, prompt version, and RTF metrics tracker (`model_runs`).
* `WRK-14 (prompts)`: Version-controlled prompt templates and JSON schemas.

### 3.3 Web Subsystem (`src/web`, Track B) — 13 Modules
* `WEB-01 (auth)`: Login screen, session refresh, language selector.
* `WEB-02 (meetings)`: Meeting catalogue, status badges, search input, filters.
* `WEB-03 (upload)`: Drag-and-drop file upload, browser microphone recording, consent check.
* `WEB-04 (processing)`: Multi-stage progress stepper connected to SSE feed.
* `WEB-05 (transcript)`: Synchronized audio playback, clickable segment seek, inline editing.
* `WEB-06 (summary)`: Structured agenda, key decisions, "AI-generated" disclaimer badges.
* `WEB-07 (actions)`: Action item triage board (Accept/Reject), quote review with 1-click play.
* `WEB-08 (search)`: Search results screen with snippet highlights and deep-linking.
* `WEB-09 (export)`: Format selector modal (DOCX, PDF, MD, JSON) with instant download.
* `WEB-10 (admin)`: System admin console for user roles, retention, and audit inspect.
* `WEB-11 (shared)`: Atomic UI component system, OpenAPI generated client, date formatters.
* `WEB-12 (locales)`: I18n translation catalogs (`kk.json`, `ru.json`, `en.json`).
* `WEB-13 (e2e)`: Playwright end-to-end regression suites running on mock worker engines.

### 3.4 Infrastructure & Quality Subsystem (Track A/B/C) — 8 Modules
* `INF-01`: Docker Compose topologies (`dev`, `prod`, GPU runtime).
* `INF-02`: Caddy reverse proxy configuration with TLS and security limits.
* `INF-03`: GitHub Actions CI pipeline (linting, static typing, tests, container builds).
* `INF-04`: Cold backup script automation for PostgreSQL and audio volumes.
* `INF-05`: k6 / Locust load testing scenarios targeting 1,000 requests/day.
* `INF-06`: Security test suite verifying RBAC boundaries and worker network isolation.
* `INF-07`: Feasibility benchmarking harness evaluating WER, DER, F1, and RTF.
* `INF-08`: Usability testing kit, SUS survey instruments, and UX findings reports.