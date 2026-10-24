# Project management and risks

Links: Git repository <URL> · YouTrack <URL>

## Responsibility matrix
| Component | Lead | Contributors | Reviewer |
|---|---|---|---|

## Milestones
| Milestone | Date | Evidence |
|---|---|---|
| Analysis, design and planning checkpoint | 2026-10-24 | |
| pre-defense-1 | TBC | tag pre-defense-1 |
| pre-defense-2 | TBC | tag pre-defense-2 |
| final-pre-defense | TBC | tag final-pre-defense |
| Defense | TBC | |

## Risks
| ID | Risk | Likelihood | Impact | Mitigation | Owner | Trigger |
|---|---|---|---|---|---|---|
| RSK-05 | Race conditions in multi-worker job claiming | Low | Medium | Use atomic PostgreSQL transactions with `SELECT ... FOR UPDATE SKIP LOCKED` to prevent race conditions during multi-worker job acquisition. | Track A | More than one worker claims the same job |

## Dependencies
| Dependency | Needed for | Owner | Status |
|---|---|---|---|
| GPU hardware (RTX 3060/4060 or equivalent) | Local ASR, diarisation and summarisation performance testing | Track C | To confirm |
| Hugging Face `pyannote` access token | Speaker diarisation model access | Track C | To configure |
| Consented meeting recordings | Privacy-compliant evaluation and usability testing | Track B | To collect |
| AITU calendar access | Meeting metadata and calendar integration validation | Track A | To confirm |
