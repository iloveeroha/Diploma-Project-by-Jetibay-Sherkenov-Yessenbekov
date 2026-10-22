<!-- File: docs/09-verification-plan.md -->
# Verification and Evaluation Plan

## 1. Quality Assurance Strategy
System verification is organized across three complementary tiers:
1. **Automated CI/CD Quality Gates:** Unit and contract tests executed on every Pull Request without requiring physical GPU hardware.
2. **AI Model Benchmarking:** Quantitative evaluation of accuracy metrics (WER, DER, ROUGE, F1) against standardized ground-truth datasets.
3. **End-to-End System & Security Validation:** User journey testing with Playwright, k6 load testing, and network egress lockdown verification.

---

## 2. AI Pipeline Metric Targets & Baselines

| Pipeline Stage | Evaluated Metric | Baseline Standard | Project Target | Measurement Dataset / Conditions |
|---|---|---|---|---|
| **Voice Activity Detection** | Detection Error Rate | > 5.0% | **< 2.5%** | Synthetic silence + speech test clips |
| **ASR (Speech-to-Text)** | Word Error Rate (WER) | ~18-20% (Whisper-base) | **< 12.0% (RU/EN)**<br>**< 16.0% (KK)** | AMI Meeting Corpus & Kazakh Speech Corpus |
| **Speaker Diarization** | Diarization Error Rate (DER) | ~20.0% (Spectral cluster) | **< 14.0%** | AMI Corpus multi-speaker meeting sessions |
| **Summarization** | ROUGE-1 / ROUGE-L | 0.35 / 0.28 | **> 0.42 / > 0.34** | Annotated meeting summary ground truth |
| **Action Items Extraction** | Precision / Recall / F1 | 0.65 / 0.60 / 0.62 | **F1 > 0.80** | Expert-annotated action item decision logs |
| **Candidate Quote Validity** | Hallucination Quote Rate | ~15% (unconstrained LLM) | **0.0% (Zero Tolerance)** | Programmatic verbatim substring check |
| **Processing Speed** | Real-Time Factor (RTF) | 1.0 (Real-time speed) | **< 0.35 (GPU)** | 60 min recording processed in < 21 min |

---

## 3. Automated Testing Levels

### 3.1 Unit & Contract Tests (No-GPU CI)
* **Ports & Adapters (`tests/unit/worker/`):** Utilizes `fakes.py` implementations of `Transcriber`, `Diarizer`, and `Summarizer`. All internal stages (`preprocess`, `vad`, `alignment`, `chunking`, `validate`) are 100% unit-tested with synthetic audio arrays and mock string inputs.
* **Database & API Tests (`tests/unit/api/`):** Runs against a temporary PostgreSQL container via Testcontainers or local test DB. Validates token lifecycle, RBAC endpoint guards, and atomic transactions.

### 3.2 End-to-End User Journey Tests (`src/web/e2e/`)
Automated using **Playwright** on the complete Docker Compose stack with fake AI engines:
* **Journey 1:** Login $\rightarrow$ File Upload $\rightarrow$ SSE Progress Monitoring $\rightarrow$ Transcript Verification.
* **Journey 2:** Audio Playback seek synchronization $\rightarrow$ Inline segment editing $\rightarrow$ Speaker renaming.
* **Journey 3:** Action item acceptance and rejection $\rightarrow$ PDF/DOCX protocol download verification.

### 3.3 Security & Egress Isolation Verification
* **Network Egress Test (`tests/security/test_network.py`):** An automated test inside the running `ai-worker` container attempts outbound HTTP/DNS requests to `google.com` and public IP addresses. The test passes **only if the connection is refused or unreachable**.
* **Tenant Isolation Test:** Ensures users from `Workspace_A` receive HTTP 404/403 when requesting meeting IDs belonging to `Workspace_B`.
* **Append-Only Audit Test:** Executes raw SQL `UPDATE` and `DELETE` queries against `audit_log` and verifies that PostgreSQL trigger constraints abort the transaction.