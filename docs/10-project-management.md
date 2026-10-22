<!-- File: docs/10-project-management.md -->
# Project Management, Allocation of Responsibilities, & Risk Registry

## 1. Responsibility Allocation Matrix (RACI)

* **R (Responsible):** The person who does the work to achieve the task.
* **A (Accountable):** The sole person who has the final sign-off and approval.
* **C (Consulted):** Domain expert consulted for advice and decisions.
* **I (Informed):** Updated on progress and outcomes.

| Project Component / Deliverable | Yerassyl Jetibay (Track A) | Assanali Yessenbekov (Track B) | Zhanassyl Sherkenov (Track C) | Supervisor (Almas Ospanov) |
|---|:---:|:---:|:---:|:---:|
| **Project Proposal & Scope (01)** | A / R | C | C | I |
| **Evidence of Relevance & Interviews (02)**| C | A / R | C | I |
| **Academic Literature Review (03)** | I | C | A / R | I |
| **Existing Systems Benchmarking (04)** | C | A / R | C | I |
| **Technology Stack Selection (05)** | A / R | C | C | I |
| **Requirements Specification (06)** | C | A / R | C | I |
| **System Architecture & DB (07)** | A / R | C | C | C |
| **UI/UX Mockups & Frontend (08)** | C | A / R | I | I |
| **Verification & Benchmarking Plan (09)**| C | C | A / R | I |
| **YouTrack Tracking & Project Mgmt (10)** | A / R | C | C | I |
| **Supervisor Review & Checkpoints (11)** | C | C | C | A |

---

## 2. Project Milestones & Timeline

[Oct 2026] ────► Pre-Defense 1: Analysis, Requirements & Architecture (Docs & Diagrams)
[Nov 2026] ────► Sprint 1-2: Core Backend, Docker Infrastructure & AI Worker Ports Setup
[Dec 2026] ────► Sprint 3-4: ASR + Diarization Alignment & React 19 Audio UI Integration
[Jan 2027] ────► Pre-Defense 2: Working MVP Demo (Upload -> Transcription -> Verification)
[Feb 2027] ────► Sprint 5-6: Map-Reduce Summarization, Action Item Quote Matcher & Exporters
[Mar 2027] ────► Sprint 7-8: Security Hardening, k6 Load Tests & Accuracy Benchmarking (WER/DER)
[Apr 2027] ────► Final Pre-Defense & Complete System Delivery


---

## 3. Risk Registry & Mitigation Strategies

| Risk ID | Risk Description | Likelihood | Impact | Mitigation Strategy |
|---|---|:---:|:---:|---|
| **RSK-01** | **Out-of-Memory (OOM) on local GPU** when running Whisper and LLM concurrently. | High | Critical | Sequential execution in AI worker: unload/clear ASR/VAD VRAM cache before initializing LLM context; use 4-bit/8-bit quantized models. |
| **RSK-02** | **CI/CD build failures** due to lack of GPU hardware on GitHub Actions runners. | High | High | Implement clean architecture ports (`ports.py`) with deterministic lightweight mock engines (`fakes.py`) for automated PR testing. |
| **RSK-03** | **Hallucinated Action Items** causing inaccurate task allocation. | Medium | High | Deterministic `WRK-11 (validate)` stage enforcing exact string-matching of quotes against the transcript before DB persistence. |
| **RSK-04** | **Poor Kazakh speech recognition accuracy** due to limited open-source domain audio. | Medium | Medium | Benchmark Faster-Whisper `large-v3` vs `medium`; utilize Kazakh Speech Corpus for domain adaptation and fine-tuning if necessary. |
| **RSK-05** | **Race conditions in multi-worker job claiming.** | Low | Medium | Use atomic