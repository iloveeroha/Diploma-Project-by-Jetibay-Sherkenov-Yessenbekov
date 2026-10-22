<!-- File: docs/08-ux/README.md -->
# UX Specifications & Key User Scenarios

## 1. Overview
The **Local AI Meeting Assistant** user interface is engineered as a responsive Single Page Application (SPA) using React 19 and TypeScript (`src/web`). The interface prioritizes executive clarity, accessible audio review, and zero-friction protocol verification.

---

## 2. Core User Journeys

[Journey 1: Ingestion]  ──► Upload Audio / Record in Browser ──► Set Title & Language ──► Live SSE Progress Stepper
│
[Journey 2: Review]     ◄── Verified Action Items Board    ◄── Synchronized Transcript   ◄────────┘
│                        (Click-to-Seek Audio)
▼
[Journey 3: Export]     ──► Select Protocol Format (DOCX / PDF / MD / JSON) ──► Download Signed Minutes


### Journey 1: Audio Ingestion & Real-Time Processing Stepper
* **Screen:** `/meetings/new`
* **Interaction:** 
  1. User drags and drops a recording (WAV, MP3, M4A) or toggles browser recording.
  2. User selects expected primary language (Kazakh, Russian, English) and confirms consent.
  3. Client opens an SSE connection (`GET /meetings/{id}/events`).
  4. The UI displays an active 5-stage stepper:
     `Preprocess` $\rightarrow$ `Transcribe` $\rightarrow$ `Diarize & Align` $\rightarrow$ `Summarize` $\rightarrow$ `Validate Items`.

### Journey 2: Synchronized Interactive Transcript Playback
* **Screen:** `/meetings/{id}`
* **Interaction:**
  1. The audio player remains docked at the top or bottom of the viewport.
  2. Clicking on any word or segment immediately seeks the audio player to that exact millisecond.
  3. Speakers are displayed with distinct colored badges (`SPEAKER_00`, `SPEAKER_01`).
  4. Organizers can click on a speaker name to rename it across the entire meeting history.

### Journey 3: Verifiable Action Items Triage
* **Screen:** Tab `/meetings/{id}#actions`
* **Interaction:**
  1. Extracted tasks are grouped in an interactive triage card list.
  2. Each card clearly shows: **Task Description**, **Assignee**, **Due Date**, and **Verbatim Source Quote**.
  3. A **"Play Quote"** button on each card instantly plays the specific 5–10 second audio clip where the commitment was made.
  4. User marks items as `Accepted`, `Modified`, or `Rejected`.

### Journey 4: One-Click Protocol Export
* **Screen:** Modal `/meetings/{id}/export`
* **Interaction:**
  1. User selects target format: **Formal DOCX**, **Archival PDF**, **Markdown**, or **Raw JSON**.
  2. File generates server-side via `API-11` and downloads immediately.

---

## 3. Prototype Link & Wireframe Assets
* **Figma Interactive Prototype:** ``
* **Design System:** Custom Tailwind CSS components adhering to WCAG 2.1 AA accessibility guidelines