# Local AI Meeting Assistant

**Local AI Meeting Assistant** is a privacy-focused, fully offline AI system for meeting transcription, speaker diarization, automated summarization, and action items extraction.

---

## Problem Statement & Target Users
- **Problem Statement:** Cloud-based meeting summary tools (e.g., Otter.ai, Read AI) require uploading audio to external servers, exposing confidential business discussions to data privacy and compliance risks.
- **Target Users:** Enterprises, legal and financial institutions, government agencies, and teams requiring 100% data privacy and offline processing.
- **Expected Outcomes:** A secure, local meeting assistant capable of processing multi-speaker recordings with verifiable action items (linked to original audio timestamps) and formatted protocol exports.

---

## Team Members & Responsibilities

| Member | Track | Primary Role & Responsibility |
| :--- | :--- | :--- |
| **Yerassyl Jetibay** | **Track A — Platform & Data** | Backend API, Database Architecture, Data Retention & Infrastructure (`src/api`, `deploy/`) |
| **Assanali Yessenbekov** | **Track B — UX & Quality** | Web Application UI/UX, Component Library, E2E & Usability Testing (`src/web`, `docs/08-ux/`) |
| **Zhanassyl Sherkenov** | **Track C — Local AI** | AI Worker Pipeline, ASR (Faster-Whisper), Diarization (PyAnnote), LLM Summarization & Model Benchmarking (`src/worker`, `eval/`) |

**Supervisor:** Almas Ospanov

---

## Project Management & Tracking
- **YouTrack Board:** [LAM Project Board](https://yerassyl.youtrack.cloud/projects/LAM/issues)

---

## Development Status & Scope
- **Current Status:** Phase 1 — Analysis, Architecture, and System Requirements Specification.
- **Code Implementation:** Scheduled to begin in November.

---

## Selected Technologies
- **Speech-to-Text (ASR):** Faster-Whisper
- **Speaker Diarization:** PyAnnote Audio
- **LLM / Summarization:** Ollama (`qwen2.5` / `llama3`)
- **Backend API:** Python, FastAPI, PostgreSQL, Alembic
- **Frontend:** Web Application UI
- **Infrastructure:** Docker Compose, Caddy Reverse Proxy

---

## Project Documentation
- `docs/01-proposal.md` — Project Proposal
- `docs/03-literature-review.md` — Literature Review (12+ sources)
- `docs/04-existing-systems.md` — Comparison of Existing Systems
- `docs/05-technology-comparison.md` — Technology Stack Alternatives
- `docs/06-requirements.md` — Functional & Non-Functional Requirements
- `docs/07-architecture.md` — System Architecture & Component Diagrams
- `docs/09-verification-plan.md` — Verification and Evaluation Plan
- `docs/11-supervisor-feedback.md` — Supervisor Feedback & Action Notes

---

## Setup & Execution Instructions
> *Detailed setup instructions will be added as soon as runnable code modules are deployed in November.*
