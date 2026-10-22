<!-- File: docs/01-proposal.md -->
# Project Proposal: Local AI Meeting Assistant

## 1. Project Title & Metadata
* **Project Name:** Local AI Meeting Assistant
* **Academic Year:** 2026/2027
* **Supervisor:** Almas Ospanov
* **Team 4 Members & Responsibilities:**
  * **Yerassyl Jetibay (Track A — Platform & Data):** Backend API, Database Architecture, Job Queue, Storage Port, Security & Deployment (Caddy, Docker Compose, CI/CD).
  * **Assanali Yessenbekov (Track B — UX & Quality):** Frontend Web SPA (React 19 + TypeScript), Real-time Interaction (SSE), Usability Testing, E2E Testing with Playwright.
  * **Zhanassyl Sherkenov (Track C — Local AI):** AI Worker Pipeline, ASR (Faster-Whisper), Diarization (PyAnnote), Local LLM Runtime (Ollama/llama.cpp), Action Item Extraction & Model Evaluation.

---

## 2. Problem Statement
Modern corporate and public organizations generate substantial amounts of audio recordings from daily board meetings, administrative planning sessions, and technical syncs. Converting these discussions into structured minutes and actionable assignments is predominantly manual, labor-intensive, and prone to subjective omission.

Existing SaaS alternatives (e.g., Otter.ai, Fireflies.ai, Microsoft Copilot) depend strictly on public cloud infrastructure. This creates critical compliance barriers for enterprises, financial entities, healthcare providers, and state institutions due to data privacy regulations (GDPR, national confidentiality mandates, trade secret protections). Furthermore, commercial cloud solutions offer inconsistent support for local multi-lingual environments (Kazakh, Russian, and mixed code-switching speech) and often produce hallucinated action items without traceable evidence.

---

## 3. Target Users & Stakeholders
1. **Meeting Organizers & Secretaries:** Need automated transcription, speaker labelling, and structured protocol exports (DOCX, PDF, Markdown) with minimal post-editing.
2. **Meeting Participants:** Need verified, accountable action items clearly linked to original audio quotes with playback validation.
3. **Enterprise Compliance & Security Officers:** Mandate that raw audio, transcripts, and LLM prompts never leave the organization's perimeter or internal network.
4. **System Administrators:** Require lightweight on-premises deployment, automated retention policies, append-only audit logging, and observable health metrics.

---

## 4. Aim and Objectives
**Aim:** To design and implement a secure, fully on-premises, containerized AI-powered meeting assistant that performs local multi-lingual speech transcription, speaker diarization, verifiable summarization, and action item extraction without external internet access during runtime.

**Key Objectives:**
1. Architect an isolated three-tier on-premises deployment (`edge`, `app`, `ai` networks) managed via Docker Compose, preventing any outbound connections from processing containers.
2. Build an asynchronous, reliable batch-processing worker pipeline integrating VAD (Silero), ASR (Faster-Whisper), Diarization (PyAnnote.audio), and Word-Speaker Alignment.
3. Construct a deterministic Map-Reduce summarization and action item extraction stage powered by an on-premises LLM engine (Ollama/llama.cpp) enforcing strict JSON schemas and verifiable quote validation.
4. Deliver a responsive React 19 web application supporting live processing progress via SSE, interactive transcript audio playback, inline speaker renaming, and protocol export.
5. Provide comprehensive validation tools including automated WER/DER/F1 evaluation scripts and end-to-end integration tests using deterministic fake engines.

---

## 5. Scope and Boundaries
* **In Scope:**
  * Single-server Docker Compose on-premises deployment.
  * Audio file ingestion (WAV, MP3, M4A, OGG) via stream-buffering and browser recording.
  * Multi-lingual transcription supporting Kazakh, Russian, and English.
  * Map-Reduce summarization and quote-verified action item extraction.
  * Role-based access control (Admin, Member, Viewer) with workspace multi-tenancy.
  * Append-only audit logging and scheduled workspace retention policies.
* **Out of Scope (Phase 1):**
  * Real-time live transcription streaming during ongoing speech (processing starts post-recording).
  * Video stream and screen-share OCR analysis.
  * Distributed multi-server Kubernetes clusters (deferred to production scaling phases).
  * Outbound calendar synchronization (MS Outlook/Google Calendar).

---

## 6. Engineering Complexity & Deliverables
The project comprises **49 modular components** across four domains:
* **Backend API (14 modules):** Modular FastAPI service covering core authentication, RBAC, media streaming with magic-byte verification, PostgreSQL `LISTEN/NOTIFY` job coordination, `pg_trgm` full-text search, append-only audit logs, and multi-format exporters.
* **AI Worker (14 modules):** Decoupled Python worker leveraging clean architecture ports (`Transcriber`, `Diarizer`, `Summarizer`, `Storage`), Silero VAD, PyAnnote diarization, Faster-Whisper ASR, deterministic speaker alignment, prompt versioning, and Hallucination-prevention quote validation.
* **Web Client (13 modules):** React 19 SPA featuring SSE progress steppers, synchronized audio player with word-level click-to-seek, tri-lingual localization (`kk`, `ru`, `en`), and Playwright E2E coverage.
* **Infra & Quality (8 modules):** Strictly air-gapped Docker Compose networking, Caddy reverse proxy, cold backup scripts, k6 load testing, and WER/DER benchmarking harnesses.