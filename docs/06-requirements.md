<!-- File: docs/06-requirements.md -->
# Requirements Specification (SRS)

## 1. User Roles & Personas
* **Viewer (`ROLE_VIEWER`):** Read-only access to authorized meetings, transcripts, summaries, and action items. Can trigger document export.
* **Member / Organizer (`ROLE_MEMBER`):** Uploads meeting audio, initiates AI transcription/summarization, edits transcripts, renames speakers, approves/rejects action items.
* **Administrator (`ROLE_ADMIN`):** Manages workspace users and roles, configures global retention limits, inspects audit logs, and monitors worker run performance (`model_runs`).
* **Compliance Auditor (`ROLE_AUDIT`):** Read-only access to immutable append-only audit records and data verification logs.

---

## 2. Functional Requirements (FR)

### Module Domain: Media & Ingestion
* **FR-01 (Audio Upload & Streaming):** The system shall allow authorized users to upload audio files (WAV, MP3, M4A, OGG) up to 500 MB in size and up to 3 hours in duration.
  * *Acceptance Criteria:* Ingestion verifies magic bytes via `ffprobe`; spoofed file extensions are rejected with HTTP 415. The stream computes SHA-256 on-the-fly without buffering the entire payload into RAM.
* **FR-02 (Browser Direct Recording):** The web interface shall provide client-side audio capture using the HTML5 MediaStream Recording API, producing standard WAV or WebM containers.
  * *Acceptance Criteria:* Recording can be paused, resumed, and submitted directly with meeting metadata.

### Module Domain: Speech & AI Worker Pipeline
* **FR-03 (Audio Preprocessing & VAD):** The worker shall normalize ingested audio to single-channel 16 kHz WAV and discard silence intervals longer than 500 ms using Voice Activity Detection.
  * *Acceptance Criteria:* Silent sections generate zero downstream ASR tokens.
* **FR-04 (ASR & Word-Level Timestamps):** The system shall transcribe speech into text with word-level start and end timestamps and automatic language detection (Kazakh, Russian, English).
  * *Acceptance Criteria:* Output contains word array with `[start_ms, end_ms, word, probability]`.
* **FR-05 (Speaker Diarization & Alignment):** The worker shall distinguish between distinct speakers and assign each transcribed word to the speaker turn with maximal temporal overlap.
  * *Acceptance Criteria:* Resulting transcript segments map strictly to distinct speaker labels (`SPEAKER_00`, `SPEAKER_01`, etc.).
* **FR-06 (Map-Reduce Summarization):** The worker shall segment long transcripts into overlapping chunks, generate intermediate chunk summaries, and reduce them into a cohesive agenda summary, key decisions, and discussion flow.
  * *Acceptance Criteria:* Summary output adheres 100% to the Pydantic JSON schema defined in `prompts/summary.json`.
* **FR-07 (Verifiable Action Item Extraction):** The worker shall extract actionable tasks, identifying the assignee, verbatim source quote, and relative deadline.
  * *Acceptance Criteria:* The validation stage (`WRK-11`) programmatically verifies that the exact candidate quote exists in the segment. If the quote is missing or hallucinated, the candidate item is rejected. Relative dates ("by Friday") are resolved against meeting date.

### Module Domain: Collaboration & Management
* **FR-08 (Interactive Transcript Editing):** Users shall be able to edit segment text and rename speaker aliases across the entire transcript.
  * *Acceptance Criteria:* Original AI-generated text is preserved in historical columns; all manual corrections emit an append-only audit event.
* **FR-09 (Multi-Format Protocol Export):** The system shall generate downloadable meeting minutes in DOCX, PDF, Markdown, and structured JSON.
  * *Acceptance Criteria:* Generated DOCX/PDF files open cleanly in MS Word/Adobe Reader, containing meeting header, agenda, decisions, speaker-attributed transcript, and verified action items.
* **FR-10 (Full-Text & Fuzzy Search):** Users shall be able to search past transcripts and summaries within their assigned workspace using exact keywords and fuzzy spellings.
  * *Acceptance Criteria:* Queries match morphological variants in Kazakh and Russian via `pg_trgm`; results return snippet highlights with deep links to audio player timestamps.

---

## 3. Non-Functional Requirements (NFR)

* **NFR-01 (Air-Gapped Confidentiality):** Under no operational condition shall audio data, transcripts, or prompt payloads be transmitted to external network hosts.
  * *Acceptance Criteria:* Worker container runs inside an isolated Docker bridge network (`ai`) with `internal: true`. Network integration tests verify that outbound socket connection attempts trigger `EHOSTUNREACH` or timeout errors.
* **NFR-02 (Processing Throughput & Latency):** The AI worker pipeline shall achieve a combined Real-Time Factor (RTF) $\le 0.35$ on an NVIDIA RTX 3060/4060 GPU (a 60-minute meeting must process in under 21 minutes).
* **NFR-03 (System Reliability & Fault Tolerance):** Worker failures or unhandled exceptions must not corrupt job queue state.
  * *Acceptance Criteria:* Failed jobs are tagged with explicit error codes and stack traces in PostgreSQL; worker retries transient database disconnections using exponential backoff.
* **NFR-04 (Auditability & Compliance):** All sensitive actions (logins, role changes, transcript edits, exports, deletions) must be recorded irrevocably.
  * *Acceptance Criteria:* PostgreSQL `audit_log` table allows `INSERT` only; `UPDATE` and `DELETE` operations are blocked by trigger constraints.
* **NFR-05 (Accessibility & Internationalization):** Web UI must support full localization in Kazakh (`kk`), Russian (`ru`), and English (`en`) without hard-coded UI strings.