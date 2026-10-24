# 11. Supervisor feedback record

| | |
| --- | --- |
| Project (official topic) | **EN:** Development of a Local AI-Based System for Automated Transcription, Summarization, and Action-Item Extraction from Corporate Meetings · **RU:** Разработка локальной системы на основе искусственного интеллекта для автоматической транскрибации, суммаризации корпоративных совещаний и выделения поручений · Product name: *Local AI Meeting Assistant* |
| Team (Team 4) | Yerassyl Jetibay, SE-2433, Track A — Platform & Data, GitHub `iloveeroha` · Assanali Yessenbekov, SE-2416, Track B — UX & Quality · Zhanassyl Sherkenov, SE-2433, Track C — Local AI |
| Supervisor | Almas Ospanov, Senior Lecturer, School of Software Engineering, Astana IT University |
| Reviews in this record | **R1**: written review of the repository and the YouTrack project, 22 October 2026 · **R2**: written verification, 23 October 2026: no changes found, verdict *not ready*, decision D-08 · **Re-check**: 24 October 2026, 00:47: still no changes, R2 stands · **Final check** before the `pre-defense-1` tag: 24 October 2026 (§3.2) |
| Who writes what | The supervisor writes sections 1–3 and closes items in R2 and in the final check. The team writes only the *Team response* fields and the PR links. Assanali Yessenbekov (component 11 lead) keeps the summary table (§2.4) current. |

## How the team responds

1. **One YouTrack task per comment** (project `LAM`), and its ID everywhere:
   - branch `LAM-n-sr1-yy-short-topic`;
   - PR title `LAM-n: SR1-yy …`;
   - commit messages `LAM-n: <what changed>`.
2. **Author.** Each student commits from their own GitHub account, with their real name and an e-mail that is verified on GitHub.
3. **PR description:** state the comment ID, what changed and how you checked it. A member of **another track** reviews the PR in GitHub with *Review changes → Approve* or *Request changes* (a comment alone is not a review) and leaves at least one remark on the content. The author then merges with **Create a merge commit**.
4. **Team response line:** fill in the line under the comment (decision, reason, PR link, date) and the matching row of the summary table.
5. **Disagreement** is allowed. Write the reason; I decide in R2.
6. **Do not mark anything *Closed*.** Only the supervisor closes items, in R2.
7. **History:** no force-push and no rewriting of commits that are already on `main`.

## 1. Guidance given before the repository review (not counted as a review)

| Ref | Guidance (date) | How the team used it (evidence in the repository) | Supervisor note (22 Oct) |
| --- | --- | --- | --- |
| G-01 | **Student guidance document** for the topic: MVP, stack, architecture, SDLC stages (05.10.2026) | The product concept, stack and on-premises scope in 01/05/07 follow it. | Used. |
| G-02 | Team-formation and per-student justifications (08–09.10.2026) | Administrative; the track split A/B/C is consistent with the README. | No action. |
| G-03 | **Checkpoint package for 24 October** (v1.0 08.10, v1.1 09.10). It included: <ul><li>component plan C1–C11 with per-student tasks;</li><li>36 YouTrack tasks (`MTG`);</li><li>**repository template v1.1**: docs 00–11, `CONTRIBUTING.md`, `AI_USAGE.md`, PR template, `.gitignore`, `.env.example`, interview guide and consent template, diagram folders, ADR folder;</li><li>**student guide v1.1**: architecture, stack, modules, Git/YouTrack workflow with task IDs, PRs reviewed by another track and merge commits.</li></ul> | <ul><li>File names 01, 03–10 follow the template.</li><li>The template itself was **not imported**: no `CONTRIBUTING.md`, `AI_USAGE.md`, PR template, `.gitignore`, `docs/02-relevance/`, `docs/11-…`, `docs/diagrams/`, `docs/adr/`.</li><li>The team created its own YouTrack project `LAM` with 7 tasks instead of the 36 `MTG` tasks.</li><li>The Git workflow was not used: no branches, PRs or task IDs.</li></ul> | Own tracker accepted (D-01). The missing content and the workflow are not (SR1-01 to SR1-03). |
| G-04 | **Verified literature list**, 10 publications with DOIs, 2021–2026: 3 AITU journal papers (Whisper study; kk/ru/en ASR usability; Kazakh ASR error analysis), 1 Q1 (meeting summarisation survey, TACL), 3 Q2, 3 Q3 (10.10.2026) | Not used. The only overlap is GATSum, cited under a wrong author and year. | See SR1-07. |
| G-05 | **Module overview and consolidated module table**: 49 modules, IDs API-01…INF-08 (13.10.2026) | Reproduced almost verbatim in `07-architecture.md` §3 and `01-proposal.md` §6. | Acceptable as a baseline only if disclosed and complemented by your own diagrams (D-03, SR1-11, SR1-15). |
| G-06 | **Architecture diagram "under the hood"** (PNG + SVG). It includes the correction that the worker must be attached to both internal networks, `app` and `ai` (16.10.2026). | Not used. `07-architecture.md` has an ASCII sketch that places the worker only on the `ai` network. | See SR1-11. |
| G-07 | **Implementation build prompt** for an AI coding agent, Mode T rules (authorship, `AI_USAGE.md`, explain-back), for the phase after 24 October (18.10.2026) | Not applicable before pre-defense 1. | Do not start implementation through an agent until SR1-01, SR1-15 and SR1-18 are addressed. |

## 2. Supervisor review R1 — 22 October 2026

**Scope.**
- Repository [`iloveeroha/Diploma-Project-by-Jetibay-Sherkenov-Yessenbekov`](https://github.com/iloveeroha/Diploma-Project-by-Jetibay-Sherkenov-Yessenbekov), `main` at commit [`c81d54d`](https://github.com/iloveeroha/Diploma-Project-by-Jetibay-Sherkenov-Yessenbekov/commit/c81d54d) (22 October 2026, 13:38 +05:00). This is the only branch; there are no pull requests and no tags.
- The YouTrack project [`LAM`](https://yerassyl.youtrack.cloud/projects/LAM/issues) as seen by a guest on 22 October 2026.

**What I checked directly.**
- Read every file: README, `docs/01`, `03`, `04`, `05`, `06`, `07`, `08-ux/README.md`, `09`, `10`.
- Inspected the complete Git history, all remote refs and the commit authors.
- Read all 7 YouTrack tasks with their fields and comments through the guest API.
- Checked every literature entry in Crossref and by web search.
- Compared the package with the department's component table and its minimum requirements for 24 October.

### 2.1 Status of the 11 components

| # | Component | Status on 22 Oct | Main gap | Comment |
| --- | --- | --- | --- | --- |
| 1 | Project proposal | Present | objectives not measurable; legal context; official title | SR1-05 |
| 2 | Evidence of relevance | **Missing** | no interviews, no plan, not listed in README | SR1-06 |
| 3 | Literature review | Present, **not verifiable** | at least 4 of 12 sources cannot be found; 4 have wrong metadata; no references/DOIs | SR1-07 |
| 4 | Existing systems | Present | own solution counted as a system; no evidence per cell; self-hosted comparators missing | SR1-08 |
| 5 | Technology comparison | Present (formal minimum met) | outdated versions; no auth/egress decisions; sources | SR1-09 |
| 6 | Requirements | Present, incomplete | **no priorities**; no sources; consent/auth/retention/capacity missing | SR1-10 |
| 7 | Architecture and diagrams | **Diagrams missing** | no context, use-case or component diagram; no editable sources | SR1-11 |
| 8 | UX / prototype | **Missing** | no mock-ups; Figma link empty; `prototype/` empty | SR1-12 |
| 9 | Verification and evaluation plan | Present, partial | no baseline system; unsourced baselines; datasets; statistics | SR1-13 |
| 10 | Project management and risks | Present, **truncated** | file cut off at RSK-05; no dependencies; YouTrack/RACI conflicts | SR1-03, SR1-14 |
| 11 | Supervisor feedback | Missing (README links to it) | this record | SR1-16 |

### 2.2 Overall assessment

**Strengths.**
- **The design idea is coherent and fits the topic.** It is on-premises, with internal Docker networks, PostgreSQL as both store and job queue (`FOR UPDATE SKIP LOCKED`, `LISTEN/NOTIFY`), fake engines for CI and deterministic validation of action-item quotes. The same idea is consistent across 01, 05, 07 and 09.
- **Several acceptance criteria are already testable**:
  - FR-01: magic bytes, HTTP 415 and SHA-256 computed while streaming;
  - FR-07: candidates without a verbatim quote are rejected;
  - NFR-01: an outbound connection must fail with `EHOSTUNREACH` or a timeout;
  - NFR-04: a trigger blocks `UPDATE` and `DELETE` on the audit log.
- **The verification plan already contains the security tests that matter for this topic**: egress, workspace isolation and the append-only audit. It also sets a zero-tolerance metric for quote validity.
- **The technology comparison meets the formal minimum**: 3 decisions with 3 alternatives each, including non-Python back ends.
- **The risk register names real technical risks**: GPU out-of-memory, Kazakh ASR accuracy, hallucinated items, CI without a GPU.
- **The README** has the required sections, and the YouTrack board is readable without a login with three members assigned.

**Main problems for 24 October** (details below):

1. **No evidence of progressive, individual contribution (SR1-01).**
   - The repository has 3 commits.
   - Two are README edits on 15 October.
   - The third, on **22 October at 13:38**, uploads all ten documents at once: 11 files, +551 lines, message "Добавил docs, prototype и src", author `erasyl <erasyl@example.com>`.
   - Assanali and Zhanassyl have **no commits**, although YouTrack and your own RACI make them responsible for components 02, 03, 04, 06, 08 and 09.
   - There are no branches, PRs or reviews.

   This is exactly the pattern the department's requirements describe as not demonstrating continuous development.
2. **Three components required for 24 October are missing**: 02 relevance evidence (SR1-06), the diagrams of 07 (SR1-11) and the prototype of 08 (SR1-12).
3. **The literature review cannot be verified (SR1-07).**
   - At least four entries cannot be found anywhere, including the paper cited as the "theoretical foundation" of the validator WRK-11.
   - Four more have wrong authors, years or titles.

   Under the Academic Policy (ДП-AITU-01 §50, §53), use of AI must be declared and the author is personally responsible for fact-checking. This is an integrity issue, not a formatting issue.
4. **Signs of undisclosed AI drafting (SR1-15).**
   - Nine of ten documents begin with an HTML comment `<!-- File: docs/… -->`.
   - `10-project-management.md` ends mid-sentence ("Use atomic").
   - The supervisor's module table (G-05) is reproduced without attribution.

**Readiness on 22 October:** not ready to tag.

You have about a day and a half. Do not try to perfect everything. Spend it on:

- an honest component 02;
- a cleaned, verified literature list;
- three real diagrams with sources;
- low-fidelity mock-ups;
- at least two reviewed PRs authored by each student;
- the submission note.

Everything else goes into the submission note as a known limitation with a date (SR1-16).

### 2.3 Supervisor decisions

| Ref | Decision |
| --- | --- |
| D-01 | **Task tracker.** Your own YouTrack project `LAM` is accepted instead of the `MTG` tasks in G-03. Conditions: <ul><li>every component and every R1 comment has a task;</li><li>each task states, **in its description**, the responsible student by name (guests see assignees anonymised), the expected outcome, the acceptance criteria, a deadline and a meaningful priority;</li><li>each task links to its branch and PR;</li><li>a task is moved to Done only when its criteria are met.</li></ul> |
| D-02 | **Repository.** Your own repository is accepted instead of importing the template wholesale. Copy from template v1.1 what is missing: `CONTRIBUTING.md`, `AI_USAGE.md`, `.github/pull_request_template.md`, `.gitignore`, `docs/02-relevance/` (interview guide, consent template), `docs/diagrams/{src,export}`, `docs/adr/`, `docs/checkpoints/`. Keep the existing file names. |
| D-03 | **Architecture baseline.** The supervisor's baseline (G-01, G-03 guide, G-05 module table, G-06 diagram) is accepted as your starting point. Conditions: <ul><li>the reuse is disclosed in `AI_USAGE.md` and in a "Sources" line of 01 and 07;</li><li>the three required diagrams and the architecture description are your own work;</li><li>the network topology is corrected: either the worker is attached to both `app` and `ai`, or you explain how it reaches PostgreSQL and the file storage.</li></ul> |
| D-04 | **Title.** Use the official topic in EN/RU/KZ on the README, the proposal and slide 1. "Local AI Meeting Assistant" may stay as the product name. |
| D-05 | **Requirement priorities.** *Must* = the end-to-end path you will demonstrate at pre-defense 2: <ul><li>upload with consent;</li><li>transcription with diarization;</li><li>transcript review and editing;</li><li>action items with evidence quotes and playback;</li><li>DOCX/Markdown export;</li><li>authentication and roles;</li><li>zero egress.</li></ul>Browser recording, search, retention automation and PDF export are *Should*, unless you justify otherwise. Your milestone plan puts summarisation in February. That is acceptable, but then say so in the priorities. |
| D-06 | **Evaluation data.** Use only: <ul><li>recordings made with the written consent of everyone audible (team role-play meetings, volunteers);</li><li>public corpora whose licence you have checked and recorded.</li></ul>No real organisation's meetings without a written agreement. Recordings and transcripts are never committed to Git; only manifests with checksums. |
| D-07 | **Model versions.** <ul><li>Evaluate the current pyannote.audio 4.x with `speaker-diarization-community-1`, not 3.1.</li><li>Keep `qwen2.5`/`llama3` only as baselines next to current candidates, chosen by measurement on your hardware.</li><li>Record every model's licence (the pyannote weights are gated; Llama and Gemma have custom licences).</li></ul> |

### 2.4 Summary of R1 comments

Severity: **B** = blocker for the 24 October tag; **M** = major, fix by 24 October or list it as a known limitation with a date; **m** = minor, by pre-defense 2. Owners follow your own RACI in `10-project-management.md`; the use-case diagram was reassigned in R2 (D-08). The *Status* column was updated after R2 (23 October) and confirmed by the re-check on 24 October at 00:47; "D-08" marks the items required for the final check on 24 October.

| ID | Topic | Sev. | Owner | Team decision | PR | Status |
| --- | --- | --- | --- | --- | --- | --- |
| SR1-01 | Progressive and individual contribution, reviews | B | All; Yerassyl coordinates | | | Open, no change in R2 · D-08 |
| SR1-02 | Git hygiene: identity, `.gitignore`, `LICENSE`, messages, rendering | M | Yerassyl | | | Open, no change in R2 · D-08 (a, b) |
| SR1-03 | YouTrack tasks: fields, ownership, coverage, states | M | Yerassyl | | | Open, no change in R2 · D-08 (partly) |
| SR1-04 | README as the entry point; official title | M | Yerassyl | | | Open, no change in R2 · D-08 (title) |
| SR1-05 | Proposal: measurable objectives, roles, legal context | M | Yerassyl (Assanali reviews) | | | Open, no change in R2 |
| SR1-06 | Relevance evidence (component 02) | B | Assanali (all support) | | | Open, no change in R2 · D-08 |
| SR1-07 | Literature review: verifiability and coverage | B | Zhanassyl (Yerassyl reviews) | | | Open, no change in R2 · D-08 |
| SR1-08 | Existing systems: evidence and comparators | M | Assanali | | | Open, no change in R2 |
| SR1-09 | Technology decisions: versions, sources, missing ADRs | M | Yerassyl; Zhanassyl for decision 3 | | | Open, no change in R2 |
| SR1-10 | Requirements: priorities, sources, missing requirements | M | Assanali (all contribute) | | | Open, no change in R2 |
| SR1-11 | Architecture and the three diagrams | B | Yerassyl (context, component); Zhanassyl (use case, reassigned in D-08) | | | Open, no change in R2 · D-08 |
| SR1-12 | UX prototype (component 08) | B | Assanali | | | Open, no change in R2 · D-08 |
| SR1-13 | Verification and evaluation plan | M | Zhanassyl | | | Open, no change in R2 |
| SR1-14 | Project management: truncation, dependencies, risks | M | Yerassyl | | | Open, no change in R2 · D-08 (truncation) |
| SR1-15 | Disclosure of AI assistance and of reused supervisor material | M | All | | | Open, no change in R2 · D-08 |
| SR1-16 | Submission note, `pre-defense-1` tag, this record | B | Yerassyl (tag after the final check); Assanali merges this record | | | Open, no change in R2 · D-08 |
| SR1-17 | Presentation | M | All | | | Open, no change in R2 |
| SR1-18 | Hardware inventory and feasibility spike | M | Zhanassyl (all report hardware) | | | Open, no change in R2 |
| SR1-19 | Every member explains every component | M | All | | | Not held in R2 |

### 2.5 R1 comments

#### SR1-01 · Progressive and individual contribution · B · Owner: all (Yerassyl coordinates)

**Finding.**
- **History** (all branches, 22 October):
  - `135842f`, 15.10 21:26: README, YouTrack link;
  - `ba9e361`, 15.10 22:01: README;
  - `c81d54d`, 22.10 13:38: all of components 01, 03–10, 11 files, +551 lines.
- **Authorship.** All three commits come from Yerassyl: two through the GitHub web editor as `iloveeroha`, one as `erasyl <erasyl@example.com>`. That address is not linked to any GitHub account, so GitHub cannot attribute the commit.
- **Assanali and Zhanassyl: zero commits.** YouTrack names them in LAM-2, LAM-3, LAM-4, LAM-6 and LAM-7, and your RACI makes them *A/R* for 02, 03, 04, 06, 08 and 09.
- **No PRs or reviews.** No branch other than `main`, no pull request, no review, no tag.
- **README ahead of the files.** The README listed the documentation files on 15.10, a week before any of them existed in the repository.

**Why it matters.**
- Git requirements, Step 2: each student commits from their own, identifiable account.
- Step 5: "Uploading the entire project immediately before a pre-defense does not demonstrate continuous development."
- Step 7: changes come through PRs reviewed by another member.
- Minimum requirement: "evidence of progressive contributions from each team member".

The committee grades each student individually and asks each of you to show your own changes.

**Required change.**
- **Protect `main` today:**
  - a ruleset requiring a PR with 1 approval;
  - block force-push and deletion;
  - a tag ruleset so that `pre-defense-1` cannot be moved.
- **From now on, every change is a PR** from its author's own account, reviewed formally by a member of another track. Before R2, each student authors **at least two PRs on their own components** (the fixes requested here) and formally reviews at least one PR of another track.
- **Make the remaining work visibly incremental:** one PR per section or step, not one upload.
- **Submission note, honest statement:** the repository was created on 15 October; the documents were drafted outside Git and uploaded by Yerassyl in one commit on 22 October. If drafts exist elsewhere (Google Docs version history, shared drives, chat with me), link them as evidence of who wrote what and when. **Do not rewrite history.**

**Done when.**
- A screenshot of the branch and tag rulesets is in `docs/10-…`.
- Each student has at least two merged PRs with an approval from another track and a content comment.
- The submission note contains the statement.

*Team response:* Decision ☐ Accept ☐ Accept with change ☐ Disagree — reason: … · PR: … · Date: …

#### SR1-02 · Git hygiene · M · Owner: Yerassyl

**Finding.**
- **(a) Identity.** The author is `erasyl <erasyl@example.com>`, not a real full name and not a verified address.
- **(b) Files missing.** There is no `.gitignore`, which Step 4 requires (and which keeps recordings, `.env` and model weights out of Git), and no `LICENSE`.
- **(c) Commit message.** "Добавил docs, prototype и src" has no task ID and says nothing about the content.
- **(d) LLM artefact.** Nine of ten documents start with `<!-- File: docs/… -->`.
- **(e) Broken rendering.** The ASCII figures in `07` §1.1, `08-ux` §2 and `10` §2 are not inside code fences, so GitHub collapses them into unreadable paragraphs.

**Required change.**
- Each student sets `git config user.name "<Full Name>"` and `user.email` to an address verified on GitHub (`git log` must show real names).
- Add the account mapping (GitHub login → name → track) to the README.
- Add `.gitignore`: Python, Node, `.env`, `*.wav *.mp3 *.m4a *.ogg *.opus *.webm *.mp4`, model weights, `eval/data/private/`, IDE files.
- Add a `LICENSE` placeholder ("All rights reserved" until you decide).
- Use `LAM-n: <what changed>` in every message.
- Remove the HTML comments.
- Put the remaining ASCII figures in ```` ```text ```` blocks, or replace them with real diagrams (SR1-11).

**Done when.** All items are merged through reviewed PRs.

*Team response:* … · PR: … · Date: …

#### SR1-03 · YouTrack · M · Owner: Yerassyl

**Finding** (guest API, 22 October 2026):
- **Coverage.** There are 7 tasks, LAM-1 to LAM-7, all created on 15.10 between 21:19 and 21:20. None is resolved; six are in *Backlog* and one in *Develop*, although the documents were uploaded on 22.10. There are no tasks for components 02, 08, 10, 11, the presentation or the submission.
- **Empty descriptions.** Every description is empty: no expected outcome, acceptance criteria or deadline, as Step 6 requires. Three documentation tasks have the priority *Show-stopper*.
- **Ownership conflicts.** Ownership is recorded as a comment containing a name. Take LAM-1 to LAM-3 as the key: there the comment and the (anonymised) *Assignee* identify the same person. On that basis, **in LAM-4, LAM-5 and LAM-6 the comment names a different student from the *Assignee*.** Your RACI agrees with the *Assignee*, not with the comment.
- **Anonymised assignees.** Guests see assignees as "Анонимизированный-…", so the committee cannot see who is responsible.
- **No links.** No task links to a commit or a PR.

**Required change.**
- Apply D-01.
- Fix LAM-4/5/6 so that the comment, the *Assignee* and the RACI agree.
- Create tasks for 02, 08, 10, 11, the presentation, the submission note, and one per SR1 item.
- Set real states.
- Link each task to its PR.
- Check access in a private browser window.

**Done when.** Every task has the D-01 fields, the conflicts are resolved and the SR1 tasks exist.

*Team response:* … · PR: … · Date: …

#### SR1-04 · README · M · Owner: Yerassyl

**Finding.**
- The official topic does not appear anywhere.
- The documentation list is plain text, not links. It omits components 02, 08 and 10, and it lists `docs/11-supervisor-feedback.md`, which did not exist until this record.
- "Frontend: Web Application UI" says nothing; `01` says React 19 + TypeScript.
- The team table has no GitHub handles or groups.

**Required change.**
- Apply D-04.
- Make the component list a table of the 11 components with links and status.
- Add the handles, groups and account mapping (SR1-02).
- State the front-end stack.
- Add a short "How we work" section: branches, PR review by another track, task IDs, tags.

**Done when.** A reader reaches every component from the README in one click.

*Team response:* … · PR: … · Date: …

#### SR1-05 · Proposal · M · Owner: Yerassyl (Assanali reviews)

**Finding.**
- **(a) Objectives.** The five objectives have no targets and no dates.
- **(b) Roles.** §5 has three roles (Admin, Member, Viewer). `06` §1 has four (adding Compliance Auditor). §3 lists compliance officers as stakeholders.
- **(c) Legal context.** §2 cites GDPR but not the law that applies to recordings of employees' voices in Kazakhstan, the Law of the Republic of Kazakhstan No. 94-V "On personal data and their protection". It also omits the Law "On Artificial Intelligence" (labelling of AI output). Participants' consent to recording is not mentioned at all.
- **(d) Unsupported claims.** "Inconsistent support for … Kazakh" and "hallucinated action items" have no evidence; link them to 02, 03 and 04 or mark them as assumptions.
- **(e) Expected outcomes.** There are no expected outcomes in the proposal itself; they appear only in the README.
- **(f) Complexity.** The complexity section copies the 49-module count from G-05 instead of explaining the difficulty in your own words. The three hard problems are:
  - Kazakh–Russian code-switched ASR;
  - attributing tasks to speakers with evidence;
  - verifiable zero egress.

**Required change.**
- Add a target and a date to each objective, taken from `09` and the milestones (provisional is fine).
- Fix one role model, used everywhere.
- Add the legal context and consent as a constraint.
- Add expected outcomes.
- Rewrite §6 in your own words, with a "Sources" line (D-03).

**Done when.** §4–§6 are measurable and consistent with 06 and 07.

*Team response:* … · PR: … · Date: …

#### SR1-06 · Relevance evidence (component 02) · B · Owner: Assanali (all support)

**Finding.** The component is missing and the README does not mention it. The department requires 3–5 discussions with user representatives (or an agreement with a client), and asks whether verified findings are separated from assumptions.

**Required change.**
- **If interviews took place,** add one record per interview with:
  - date, format and duration;
  - interviewer;
  - respondent role, and the organisation type and size (anonymised);
  - language;
  - whether the text is verbatim or a summary;
  - where the consent is kept (privately, not in Git).

  Add a findings table (F-nn, verified or assumption, the FR/NFR it supports).
- **If no interviews have taken place, do not invent any.** State that honestly.
  - Add the interview guide and consent template from template v1.1 (`docs/02-relevance/`).
  - Add a dated plan for at least 3 interviews before pre-defense 2.
  - Easy respondents: people who write minutes (secretaries of AITU departments or the dean's office), an IT or security officer of a bank or state body, a team lead in a company.
- **Even two 15-minute calls before Saturday are better than none.** One observation also counts: with permission, measure how long it takes to produce the minutes of one real department meeting.

**Done when.** Component 02 exists with either real records or an honest dated plan, and 06 links each requirement to a finding or marks it as an assumption.

*Team response:* … · PR: … · Date: …

#### SR1-07 · Literature review · B · Owner: Zhanassyl (Yerassyl reviews)

**Finding** (checked in Crossref and by web search on 22 October 2026):

| Row | As written | What I found |
| --- | --- | --- |
| 3 | Cui et al. (2020), *Slide-Window and Graph Attention for Long Document & Dialogue Summarization*, TACL; and "GATSum by Cui et al., 2020" in §2.3 | No such paper found. **GATSum** is Jiang, Zou, Xu & Zhang (2022), *Information Technology and Control* 51(2), doi 10.5755/j01.itc.51.2.30796 (from G-04). |
| 4 | Zhang et al. (2024), *Benchmarking Large Language Models for Meeting Summarization*, ACL Findings | Not found. The closest real paper is Zhang et al. (2024), *Benchmarking Large Language Models for **News** Summarization*, TACL, doi 10.1162/tacl_a_00632. |
| 5 | Kim et al. (2023), *CTranslate2: Fast Inference Engine for Transformer Models* | No such publication found. CTranslate2 is OpenNMT software: cite the repository, version and access date. It is not a scientific source. |
| 7 | Wang et al. (2023), *Mitigating Hallucination in Abstractive Summarization with Verifiable Quotes*, EMNLP | **Not found.** Your table calls it the "theoretical foundation for our WRK-11". |
| 2 | Bredin et al. (2023), *PyAnnote.audio 2.1 / 3.0: Neural building blocks…*, ICASSP | Mixes two papers: Bredin et al. (2020), ICASSP, doi 10.1109/icassp40776.2020.9052974, and Bredin (2023), Interspeech, doi 10.21437/interspeech.2023-105. |
| 6 | Medennikov et al. (2022), Interspeech | The paper is from 2020, titled *Target-Speaker Voice Activity Detection: A Novel Approach for Multi-Speaker Diarization in a Dinner Party Scenario*, doi 10.21437/interspeech.2020-1602. It needs speaker enrolment, so it does not support "pre-filtering silence". |
| 8 | Touvron et al. (2023), *Llama 2 / Llama 3* | These are two different papers; choose one and cite it correctly. |
| 11 | Wu et al. (2023), Chain-of-Density | The authors are Adams et al. (2023), NewSum workshop, doi 10.18653/v1/2023.newsum-1.7. |

- **Resolvable entries.** Rows 1 (Whisper, ICML 2023), 9 (Qwen2.5 report), 10 (AMI) and 12 (RAG, NeurIPS 2020) can be identified.
- **References.** There is no reference list, no DOI or URL, and no access date. Quantitative claims ("DER below 12 % on AMI", "up to 4×") have no source.
- **Coverage.** No source on Kazakh or Russian ASR, although code-switching is the main technical risk (RSK-04). None of the ten verified sources in G-04 is used.

**Why it matters.**
- The requirement is ≥ 12 *meaningfully used* sources, ≥ 8 of them scientific. With four entries untraceable, the requirement is not met in substance.
- ДП-AITU-01 §53 makes each author personally responsible for fact-checking anything produced with AI. A committee member or the anti-plagiarism check finding a non-existent reference is an academic-honesty problem.

**Required change (by 24 October).**
- **Remove every entry you have not opened and read.**
- **Replace them with verified sources.** G-04 gives ten with DOIs and open access; include at least five, among them at least two on Kazakh ASR (e.g. 10.37943/24AHNP6638, 10.37943/20DZGH8448, 10.3390/info14020074).
- **For each kept source**, write in your own words: the method, the result, the limitation and the decision it informs in this project.
- **Add a reference list** with a DOI or URL and an access date for every entry.
- **Add a short search log:** databases, queries, date.
- **Plan the path** to ≥ 20 references with ≤ 30 % internet sources for the final report (ДП-AITU-19 п. 28).
- **Reviewer:** Yerassyl opens every DOI before approving.

**Done when.** Every row resolves, rows 3, 4, 5 and 7 are replaced or corrected, and the G-04 sources are included.

*Team response:* … · PR: … · Date: …

#### SR1-08 · Existing systems · M · Owner: Assanali

**Finding.**
- **(a) Your own solution is a column of the matrix.** It is not an existing system. There are four comparators; 3–5 are required, so this is acceptable once the column is removed or set apart.
- **(b) No evidence per cell.** No cell has a source, an access date or a screenshot. Several cells are unsupported or overstated, for example the KK support levels or "Fatal flaws … explicitly violates … state secret regulations".
- **(c) The gap statement is contradicted by existing tools.** "There is no turnkey, self-hosted … meeting assistant" ignores open-source self-hosted tools, for example:
  - [Meetily](https://github.com/Zackriya-Solutions/meetily): local Whisper transcription and Ollama summaries;
  - [Scriberr](https://github.com/rishikanthc/Scriberr): self-hosted transcription with diarization and a web UI.

  Commercial ASR vendors with on-premises licensing also exist.

**Required change.**
- Remove or separate the own-solution column.
- Add at least one self-hosted comparator.
- Give every cell an evidence label (Documented / Observed / Vendor claim / Not specified), a link and an access date.
- Do one 30-minute hands-on check of Meetily or WhisperX on a 2-minute consented kk/ru clip, with screenshots.
- Narrow the gap statement to what you can show:
  - kk/ru code-switching quality;
  - action items with verifiable evidence;
  - a multi-user workspace with audit and retention;
  - verified zero egress.

**Done when.** The matrix has per-cell evidence, a self-hosted comparator and a supported gap statement.

*Team response:* … · PR: … · Date: …

#### SR1-09 · Technology decisions · M · Owner: Yerassyl (Zhanassyl for decision 3)

**Finding.**
- **(a) Criteria.** They are not derived from the requirements (no FR/NFR IDs), and the numbers have no source ("<12 % DER", "up to 4×", "~6–8 GB VRAM").
- **(b) Versions.** Decision 3 uses pyannote 3.1 and `qwen2.5`/`llama3`. The guide (G-03) names pyannote.audio 4.0 with `community-1`; on 18 October the current release was 4.0.7. No licences are recorded.
- **(c) Missing decisions.** The requirements depend on decisions that are not recorded: front-end framework, authentication and sessions (API-02 "JWT, refresh rotation"), and how egress is blocked **and verified** (NFR-01 is your central claim).
- **(d) No ADRs.** `docs/adr/` does not exist.

**Required change.**
- Apply D-07.
- Add FR/NFR IDs to the criteria.
- Add sources and access dates.
- Add two short ADRs with 2–3 alternatives each: "authentication and sessions"; "egress control and its verification" (internal networks, firewall rules, negative-control test).
- Add the front-end decision by pre-defense 2.

**Done when.** Decision 3 is updated and both ADRs are merged.

*Team response:* … · PR: … · Date: …

#### SR1-10 · Requirements · M · Owner: Assanali (all contribute)

**Finding.**
- **(a) No priorities.** No requirement has a priority, although the component explicitly asks for priorities. No requirement has a source or a verification method.
- **(b) Missing requirements.** These are central to the topic:
  - consent capture before upload or recording;
  - authentication and role enforcement (roles are defined, but no FR);
  - retention and deletion (in the proposal's scope);
  - cancel and retry of processing;
  - the audit-log viewer;
  - capacity (my guidance: about 1 000 users per day; derive your request rate from it);
  - upload limits and logging without content;
  - a usability target.
- **(c) Contradiction.** FR-02 produces **WebM** recordings, but FR-01 accepts only WAV/MP3/M4A/OGG and rejects other types with 415, so browser recordings would be rejected.
- **(d) Criteria that cannot be verified as written.** FR-09 "open cleanly"; NFR-05 has no criterion and no WCAG level. NFR-02 (RTF ≤ 0.35 on an RTX 3060/4060) assumes hardware nobody has reported (SR1-18).
- **(e) Stack traces.** NFR-03 stores stack traces in PostgreSQL. They can contain transcript content; store machine error codes instead.

**Required change.**
- For every FR/NFR add: priority (MoSCoW per D-05), source (finding F-nn, literature or assumption), acceptance criterion and verification method (unit / integration / e2e / evaluation).
- Add the missing SEC/NFR items.
- Resolve the WebM contradiction.
- Use one role model, the same as in 01 (SR1-05).

**Done when.** Every *Must* has a priority, a source, a measurable criterion and a verification method.

*Team response:* … · PR: … · Date: …

#### SR1-11 · Architecture and diagrams · B · Owner: Yerassyl (context, component); Assanali (use case)

**Finding.**
- **(a) The three diagrams are missing.** The department requires a system context diagram, a use-case diagram and a draft component diagram, with **editable source files** and readable exports. None exists.
- **(b) The ASCII sketch is wrong.**
  - It does not render (SR1-02e).
  - It places the worker only on the `ai` network, yet draws it reading storage and writing to PostgreSQL on the `app` network. With `internal: true` networks the worker must be attached to both (G-06).
  - The "Claim (SKIP LOCKED)" arrow connects the API to the DB, but claiming is done by the worker (your own §2 step 4).
  - §1.1 says Caddy does rate limiting; core Caddy has no rate limiter (it needs a plugin, or the API does it).
- **(c) Copied, not traced.** §3 reproduces G-05 without attribution. There is no data model (ER), and no traceability from requirements to components.

**Required change (by 24 October).**
- Add the three diagrams as PlantUML or Mermaid sources in `docs/diagrams/src/`, with SVG **and PDF/EPS** exports in `docs/diagrams/export/`. The LaTeX report needs vector figures (ДП-AITU-19 п. 42–47).
- Correct the topology.
- Add a table FR/NFR → module → planned test.
- Disclose the baseline (D-03).
- The ER diagram may follow by pre-defense 2.

**Done when.** The sources and exports exist, `07` embeds them, and the traceability table exists.

*Team response:* … · PR: … · Date: …

#### SR1-12 · UX prototype (component 08) · B · Owner: Assanali

**Finding.**
- There are no mock-ups.
- The "Figma Interactive Prototype" link is empty (only two backticks), and `prototype/` contains only `.gitkeep`.
- The minimum requirement is "prototype materials or a link to the prototype".
- The journeys text is a good start, but:
  - "Download Signed Minutes" promises signing, which is not in scope;
  - "WCAG 2.1 AA" disagrees with NFR-05.

**Required change (by 24 October).**
- Produce low-fidelity mock-ups (Figma or Penpot, with a public view link and PNG exports in `docs/08-ux/`) for:
  - upload with a **visible consent step**;
  - processing progress;
  - transcript review with the player;
  - action-item review with the evidence quote and playback;
  - export.
- Remove "signed".
- Align the WCAG level (2.2 AA).
- After 24 October, run two short walkthroughs with people outside the team and record the observations.

**Done when.** The screens and the link are in the repository and the README.

*Team response:* … · PR: … · Date: …

#### SR1-13 · Verification and evaluation plan · M · Owner: Zhanassyl

**Finding.**
- **(a) Unsourced baselines.** "~18–20 % (Whisper-base)", ROUGE 0.35/0.28, F1 0.65/0.60/0.62 and "~15 % (unconstrained LLM)" have no source.
- **(b) No baseline solution.** The component asks for a baseline solution for comparison, and none is defined.
- **(c) Datasets.**
  - AMI is English.
  - The "Kazakh Speech Corpus" is read speech, not meetings, and its licence is not checked.
  - There is no Russian or code-switched meeting data and no plan to record consented meetings.
  - There are no sample sizes, no annotation procedure and no statistics.
- **(d) Measurement conditions.** The hardware is not stated.
- **(e) Load test.** It is not derived from a workload; `07` INF-05 says "1,000 requests/day", which should be users per day.
- **(f) Usability.** There is no usability (SUS) evaluation, although INF-08 plans it.

**Required change.**
- Cite each baseline number or label it "assumption, to be replaced by our measurement".
- Define the comparison baselines:
  - B0: a plain faster-whisper or WhisperX pipeline;
  - B1: a single-prompt LLM extraction without the validator;
  - B2: your map-reduce extraction with the validator.
- Plan a consented gold set (kk, ru, en, mixed; size; two annotators on ≥ 20 %).
- Report 95 % bootstrap confidence intervals.
- State the reference hardware.
- Derive the k6 load from 1 000 users per day.
- Add the SUS test.
- Add a negative control to the egress test (it must *fail* when a container is on a non-internal network).
- Mark the WER/DER targets provisional until SR1-18 gives first numbers.

**Done when.** Each metric has a baseline, a dataset, a sample size and a condition.

*Team response:* … · PR: … · Date: …

#### SR1-14 · Project management · M · Owner: Yerassyl

**Finding.**
- `10-project-management.md` is **cut off mid-row** ("RSK-05 … Use atomic").
- There is no dependencies section, which the component requires.
- The milestones are not in a code block and render as one paragraph; the pre-defense dates are not marked provisional.
- There is no YouTrack link in the document.
- The RACI conflicts with YouTrack (SR1-03).
- Missing risks:
  - process and contribution evidence (SR1-01);
  - literature integrity (SR1-07);
  - no GPU available;
  - consented data for evaluation;
  - model licences;
  - availability of a team member.
- There is no log of meetings with the supervisor.

**Required change.**
- Complete the register.
- Add dependencies: GPU hardware, Hugging Face access to the gated pyannote weights, consented recordings, the AITU schedule.
- Fix the rendering, mark dates provisional, link YouTrack.
- Add a dated supervisor meeting log, linked to this record.

**Done when.** The file is complete and consistent with YouTrack.

*Team response:* … · PR: … · Date: …

#### SR1-15 · Disclosure of AI assistance and of reused material · M · Owner: all

**Finding.**
- The HTML file-name headers, the truncated file, the untraceable references and the uniform style indicate AI-generated drafts.
- Content from my materials (G-03, G-05) is reused without attribution, although the guide says the submitted documents must be your own work.
- Using AI tools and supervisor material is allowed (ДП-AITU-01 §50), but it must be declared. Each author is personally responsible for checking the result (§53).

**Required change.**
- Add `AI_USAGE.md` (the template from G-03) with one row per document: date, tool and model, purpose, what the author verified or changed.
- Add a "Sources" line to 01, 05 and 07 naming the supervisor materials used.
- Each student confirms their rows in the PR.

**Done when.** The file exists and each student has confirmed their part.

*Team response:* … · PR: … · Date: …

#### SR1-16 · Submission note, tag and this record · B · Owner: Yerassyl (tag after R2); Assanali merges this record

**Finding.** There is no tag, no submission note and no component 11.

**Required change.**
- Commit this record as `docs/11-supervisor-feedback.md` through a PR authored by Assanali and reviewed by Yerassyl.
- Write `docs/checkpoints/pre-defense-1.md` containing:
  - the repository link and tag;
  - the completed work per student;
  - known limitations, including every SR1 item carried over, with its date;
  - outstanding tasks with owners and dates.
- After R2, create the annotated tag `pre-defense-1` on the commit I accept, and never move it.

**Done when.** The record and the note are on `main`, and the tag points to the accepted commit.

*Team response:* … · PR: … · Date: …

#### SR1-17 · Presentation · M · Owner: all

**Finding.** There is no presentation in the repository.

**Required change.**
- About 10–12 slides for 8–10 minutes (ДП-AITU-08 cl. 65).
- Slide 1: the official topic in EN/RU/KZ and the supervisor.
- Content:
  - the problem;
  - relevance evidence, or the honest plan;
  - requirements with priorities;
  - the three diagrams;
  - two prototype screens;
  - the evaluation plan with baselines;
  - one slide on R1 and the changes it caused;
  - the next steps.
- Each student presents their own part.
- Rehearse with a timer and record the duration.

**Done when.** The deck is in the repository and the rehearsal time is recorded.

*Team response:* … · PR: … · Date: …

#### SR1-18 · Hardware inventory and feasibility spike · M · Owner: Zhanassyl (all report hardware)

**Finding.**
- Nothing shows that anyone has run faster-whisper, pyannote or Ollama yet.
- NFR-02 (RTF ≤ 0.35 on an RTX 3060/4060) and decision 3 (~6–8 GB VRAM) therefore have no basis.
- RSK-01 (out-of-memory) is rated *High*, but no hardware is listed.

**Required change.**
- A table with CPU, RAM, GPU/VRAM and OS for each student.
- A short spike in `eval/spike/README.md`, with the exact commands and versions:
  - faster-whisper `small` and `large-v3-turbo` on a 2–3-minute consented kk/ru clip, with a rough WER and the RTF;
  - whether pyannote `community-1` runs (Hugging Face account with the accepted model conditions).
- A fuller run follows by pre-defense 2.

**Done when.** The table and the first measured numbers are in the repository.

*Team response:* … · PR: … · Date: …

#### SR1-19 · Every member explains every component · M · Owner: all

**Finding.** The tracks are clear, but the committee will ask any of you about anything, and so far only one of you has committed.

**Required change.** Study the parts you did not write. In R2 I will ask each of you two questions outside your own track, for example:
- **Yerassyl:**
  - "Why does the validator store the original slice of the segment rather than the model's quote, and what can the database check?"
  - "Why is the AMI corpus not enough to evaluate this system?"
- **Assanali:**
  - "Why must the worker be attached to both internal networks, and how do you prove that it cannot reach the internet?"
  - "What happens when two workers claim jobs at the same moment?"
- **Zhanassyl:**
  - "Which requirements does each of the three diagrams trace to?"
  - "Why can a viewer read a meeting but not edit it, and where is that enforced?"

**Done when.** Each student answers both questions in R2.

*Team response:* … · Date: …

## 3. Supervisor review R2 — 23 October 2026

| | |
| --- | --- |
| Date and time | 23 October 2026, 21:10 (UTC+5) |
| Commit reviewed | `main` at [`c81d54d`](https://github.com/iloveeroha/Diploma-Project-by-Jetibay-Sherkenov-Yessenbekov/commit/c81d54d), the same commit as in R1 |
| Form | Written only: repository and YouTrack checked remotely. The demo drill and the cold questions were not held (see below). |
| Re-check | 24 October 2026, 00:47 (UTC+5), same method. `main` is still at `c81d54d`, and there are still no other branches, pull requests or tags. The YouTrack instance still has only the project `LAM` and no knowledge-base articles, and no task has changed since 21 October, 20:33. The R2 result, the verdict and D-08 stand unchanged. |

**What I checked.**
- **Repository.** I fetched all branches and tags and listed every remote ref. There is still one branch, `main`, at `c81d54d` (22 October, 13:38). There are no new commits, branches, pull requests or tags.
- **YouTrack.** I read every task in the only project, `LAM`, through the guest API. There are still 7 tasks, LAM-1 to LAM-7. The latest change to any task was on 21 October at 20:33 (UTC+5), before R1. The descriptions are still empty, the LAM-4/5/6 ownership conflicts are unchanged, and there is no task for any SR1 item.
- **This record.** It is not in the repository yet, and no *Team response* field has been filled in.

**Result.** No R1 comment has been addressed. R2 adds a fourth status to the three in the template: **Open, no change** means that nothing was submitted for the item.

| Item | Result | Supervisor note |
| --- | --- | --- |
| SR1-01 | Open, no change | Still 3 commits, all by Yerassyl; Assanali and Zhanassyl have none. No PR, no review. There is no screenshot of the rulesets; branch protection cannot be seen from outside the repository. In D-08. |
| SR1-02 | Open, no change | The author is still `erasyl@example.com`; there is no `.gitignore` or `LICENSE`; the HTML headers are still in 9 files. Identity and `.gitignore` are in D-08; the rest is carried over. |
| SR1-03 | Open, no change | 7 tasks with empty descriptions, the LAM-4/5/6 conflicts, no SR1 tasks. Tasks for the D-08 PRs and the conflicts are in D-08; the full D-01 fields are carried over. |
| SR1-04 | Open, no change | The official title is still missing. The title is in D-08; the rest is carried over. |
| SR1-05 | Open, no change | Carried over (§4). |
| SR1-06 | Open, no change | Component 02 is still missing. In D-08. |
| SR1-07 | Open, no change | Rows 3, 4, 5 and 7 are still untraceable, and there is no reference list. In D-08. |
| SR1-08 | Open, no change | Carried over (§4). |
| SR1-09 | Open, no change | Carried over (§4). |
| SR1-10 | Open, no change | The WebM contradiction between FR-01 and FR-02 is still there. Carried over (§4). |
| SR1-11 | Open, no change | No diagrams; the topology is still wrong. In D-08. |
| SR1-12 | Open, no change | The Figma link is still empty, and `prototype/` holds only `.gitkeep`. In D-08. |
| SR1-13 | Open, no change | Carried over (§4). |
| SR1-14 | Open, no change | `10-project-management.md` still ends at "Use atomic". The truncation is in D-08; the rest is carried over. |
| SR1-15 | Open, no change | No `AI_USAGE.md`. In D-08. |
| SR1-16 | Open, no change | No record in the repository, no submission note, no tag. In D-08. |
| SR1-17 | Open, no change | No deck. Required before the pre-defense session (§4). |
| SR1-18 | Open, no change | Carried over (§4). |
| SR1-19 | Not held | Moved to the final check (§3.2). |

**Demo drill and cold questions.** Not held: there is no PR or review to trace. Both move to the final check.

**Verdict:** ☐ Ready to tag ☐ Ready to tag with the limitations listed in the submission note ☒ **Not ready.** Reason: no R1 comment was addressed, and the 24 October minimum is still not met. Components 02 and 11, the three diagrams, the prototype, a verifiable literature review and evidence of each student's contribution are all missing.

**Accepted commit for `pre-defense-1`:** none · Confirmation: Almas Ospanov · Date: 23.10.2026

### 3.1 Decision after R2

| Ref | Decision |
| --- | --- |
| D-08 | **Minimum for the final check on 24 October.** <ul><li>**Scope.** The scope is cut to the seven PRs below. Every other R1 item goes into the submission note as a known limitation, with the date in §4.</li><li>**Authorship.** The R1 rule stands: each student authors at least two of these PRs, and a member of another track approves each one formally.</li><li>**Load.** The use-case diagram moves from Assanali to Zhanassyl. Because of this, Zhanassyl's first SR1-19 question becomes: "How does the upload endpoint verify a file, and what does it return for an unsupported type?"</li><li>**Before the first PR:**<ul><li>Yerassyl creates one `LAM` task per PR and resolves the LAM-4/5/6 conflicts (SR1-03).</li><li>Each student sets their real name and a verified e-mail in Git (SR1-02a).</li><li>Yerassyl protects `main` and adds `.gitignore` (SR1-01, SR1-02b).</li></ul></li><li>**Order.** Merge PR 1 first and PR 6 last, because the submission note refers to the others.</li><li>**Final check.** When the PRs are merged, post their links in the team chat. I then do the final check (§3.2) and confirm the commit for the tag.</li><li>**If nothing is merged by the submission deadline,** the R2 verdict stands. You still tag and submit the commit you have, and this record goes to the committee as it is.</li></ul> |

| PR | Content | Comments | Author | Reviewer (another track) |
| --- | --- | --- | --- | --- |
| 1 | This record as `docs/11-supervisor-feedback.md`, unchanged except for the *Team response* fields | SR1-16 | Assanali | Yerassyl |
| 2 | `docs/02-relevance/`. If interviews took place: the records. If not: an honest status, the interview guide and consent template from template v1.1, and a dated plan for at least 3 interviews before pre-defense 2. | SR1-06 | Assanali | Zhanassyl |
| 3 | `03-literature-review.md`: <ul><li>remove or replace rows 3, 4, 5 and 7;</li><li>correct rows 2, 6, 8 and 11;</li><li>add at least 5 G-04 sources, at least 2 of them on Kazakh ASR;</li><li>add a reference list with a DOI or URL and an access date for every entry.</li></ul> | SR1-07 | Zhanassyl | Yerassyl (opens every DOI) |
| 4a | Context and component diagrams: <ul><li>Mermaid or PlantUML sources in `docs/diagrams/src/`;</li><li>SVG and PDF exports in `docs/diagrams/export/`;</li><li>the worker attached to both `app` and `ai`;</li><li>both diagrams embedded in `07`.</li></ul> | SR1-11 | Yerassyl | Assanali |
| 4b | Use-case diagram in the same format, embedded in `07` | SR1-11 | Zhanassyl | Yerassyl |
| 5 | Low-fidelity mock-ups of the five screens listed in SR1-12 (a public Figma or Penpot link and PNG exports in `docs/08-ux/`); "Signed" removed | SR1-12 | Assanali | Zhanassyl |
| 6 | <ul><li>`AI_USAGE.md`;</li><li>a "Sources" line in 01, 05 and 07;</li><li>the HTML headers removed;</li><li>RSK-05 in `10` completed;</li><li>the official title in the README;</li><li>`docs/checkpoints/pre-defense-1.md` with the SR1-01 statement, the work done by each student, and §4 as the known limitations.</li></ul> | SR1-01, SR1-04, SR1-14, SR1-15, SR1-16 | Yerassyl. Assanali and Zhanassyl each confirm their own `AI_USAGE.md` rows in a review comment. | Assanali |

### 3.2 Final check before the tag — 24 October 2026 (to be completed by the supervisor)

**State at the re-check (24 October, 00:47):** none of the seven D-08 PRs has been opened, and no link has been posted, so the final check has not started.

| | |
| --- | --- |
| Date and time | … |
| Commit reviewed | … |
| Form | ☐ In person ☐ Online ☐ Written only |

| D-08 PR | Merged PR link | Formal approval by another track | Result (Accepted / Not accepted) | Supervisor note |
| --- | --- | --- | --- | --- |
| 1 · this record | | | | |
| 2 · component 02 | | | | |
| 3 · literature | | | | |
| 4a · context and component diagrams | | | | |
| 4b · use-case diagram | | | | |
| 5 · mock-ups | | | | |
| 6 · disclosure and submission note | | | | |
| Demo drill: each student traces one task in under two minutes (YouTrack task → branch → PR → review comment → revision → merge commit → files) | — | — | | |
| Cold questions: two per student (SR1-19, as changed in D-08) | — | — | | |

After the check I update the *Status* column in §2.4. An accepted PR closes its items; anything not accepted moves to §4.

**Verdict:** ☐ Ready to tag ☐ Ready to tag with the limitations listed in the submission note ☐ Not ready — reason: …

**Accepted commit for `pre-defense-1`:** … · Confirmation: Almas Ospanov · Date: …

## 4. Items carried over to pre-defense 2

The dates were proposed by the supervisor in R2. Confirm each date in the submission note, or propose another with a reason; I confirm them in the final check. Any D-08 PR that is not accepted in the final check is added here.

| Item | What remains | Owner | New date |
| --- | --- | --- | --- |
| SR1-02 | `LICENSE`; `LAM-n:` commit messages; ASCII figures in code blocks | Yerassyl | 06.11.2026 |
| SR1-03 | All D-01 fields on every task; tasks for every component; links to PRs | Yerassyl | 06.11.2026 |
| SR1-04 | Component table with links and status; handles and groups; front-end stack; "How we work" | Yerassyl | 06.11.2026 |
| SR1-05 | Measurable objectives; one role model; legal context and consent; expected outcomes; §6 in your own words | Yerassyl (Assanali reviews) | 06.11.2026 |
| SR1-10 | MoSCoW per D-05, with sources, criteria and verification methods; the missing requirements; the WebM fix | Assanali (all contribute) | 06.11.2026 |
| SR1-14 | Dependencies; the missing risks; the supervisor meeting log | Yerassyl | 06.11.2026 |
| SR1-08 | Evidence per cell; a self-hosted comparator; the hands-on check; a narrower gap statement | Assanali | 13.11.2026 |
| SR1-09 | Decision 3 per D-07; FR/NFR IDs and sources; ADRs on authentication and on egress control | Yerassyl; Zhanassyl for decision 3 | 13.11.2026 |
| SR1-11 | Requirements → module → test table (13.11.2026); ER diagram (pre-defense 2) | Yerassyl | 13.11.2026 / pre-defense 2 |
| SR1-18 | Hardware table and the first spike numbers | Zhanassyl (all report hardware) | 13.11.2026 |
| SR1-12 | Two walkthroughs with people outside the team | Assanali | 20.11.2026 |
| SR1-13 | Sourced baselines; B0–B2; gold-set plan; confidence intervals; hardware; k6 load from 1 000 users per day; SUS; negative control for the egress test | Zhanassyl | 20.11.2026 |
| SR1-17 | Presentation and a timed rehearsal | All | Before the pre-defense session |
| SR1-19 | Cold questions, if they are not held in the final check | All | Before the pre-defense session |

## 5. Consultation log

| Date | Form | Participants | Topic / deliverable | Resulting decision or comment |
| --- | --- | --- | --- | --- |
| 05.10.2026 | Written | Supervisor → team | Student guidance (G-01) | — |
| 08–09.10.2026 | Written | Supervisor → team | Checkpoint package, template and guide v1.1 (G-03) | — |
| 10.10.2026 | Written | Supervisor → team | Verified literature list (G-04) | — |
| 13.10.2026 | Written | Supervisor → team | Module table (G-05) | D-03 |
| 16.10.2026 | Written | Supervisor → team | Architecture diagram (G-06) | D-03 |
| 22.10.2026 | Written review | Supervisor → team | R1 (this record) | D-01 … D-07, SR1-01 … SR1-19 |
| 23.10.2026 | Written verification | Supervisor | R2: repository and YouTrack unchanged since R1 | Not ready; D-08 |
| 24.10.2026, 00:47 | Written re-check | Supervisor | Repository and YouTrack still unchanged; no D-08 PR opened | R2 verdict and D-08 stand |
| 24.10.2026 | … | … | Final check before the tag (§3.2) | … |
| *(team adds every meeting or call with the supervisor: date, form, who attended, what was decided)* | | | | |
