# UX / prototype

Prototype link: <Figma/Penpot URL> (committee must be able to open it)

The UX is designed for the following five scenarios:

1. **Ingestion with consent.** The user selects an audio file, confirms that all participants consented to recording and processing, chooses the meeting languages (Kazakh and/or Russian), and starts a local processing job.
2. **Processing stepper.** A progress stepper shows upload validation, transcription, speaker diarisation, summarisation, and action-item extraction. Each stage exposes clear status and actionable errors.
3. **Synchronized transcript playback.** The user plays the meeting audio while the transcript follows the current timestamp. Selecting a transcript segment seeks the audio to the corresponding quote.
4. **Action-item verification with audio quote seek.** Each proposed action item shows its owner, deadline and supporting transcript quote. The reviewer can seek directly to that audio quote, edit the fields, and confirm or reject the item.
5. **Export.** The user exports the reviewed transcript, summary and action items as DOCX, PDF, Markdown or JSON. Signing minutes is outside the project scope.

| Screen / scenario | Use case | FR IDs | Export file |
|---|---|---|---|
| Ingestion with consent | Start a consented local processing job | FR-01, NFR-02 | |
| Processing stepper | Monitor pipeline progress and errors | FR-02 | |
| Synchronized transcript playback | Review transcript against audio | FR-03 | |
| Action-item verification with audio quote seek | Verify and edit extracted tasks | FR-04 | |
| Export | Download reviewed outputs | FR-05 | |

The target accessibility conformance level is **WCAG 2.2 AA**.
