# Frontend Interview Preparation

Personal **Frontend Interview Handbook + Question Bank + Coding Practice Repository** for Mid → Senior Frontend Engineer interviews.

This is not a beginner course. The project is designed to restore active recall and the ability to independently explain, implement, debug, review and design frontend systems.

## Current status

- Stage 0 — Research & Master Question Inventory: complete.
- Stage 1 — Curriculum & Coverage Audit: complete.
- Stage 2 — Repository Skeleton: complete after structural verification.
- Stage 3 — Calibration Section: complete; section 1.1 and its supporting artifacts were approved on 2026-10-01.
- Stage 4 — Incremental Build: in progress; sections 1.2–1.12 are approved.
- Stage 5 — Final Coverage Audit: not started.

Section **1.1. Execution Model, Declarations & Scope** is the approved calibration baseline. Sections **1.2. Values, Types, Equality & Coercion**, **1.3. Functions, Closures & Functional Patterns**, **1.4. `this`, Invocation & Object Model** and **1.5. Arrays, Transformations & Copying** completed their Stage 4 review gates on 2026-10-06, 2026-10-07, 2026-10-08 and 2026-11-04 respectively. The [1.6. Collections, Symbols & Iteration review record](reviews/stage-4-section-reviews/01-06-collections-symbols-and-iteration.md) records user approval on 2026-11-04.

## How to use the learning material

- **Learn or restore a topic:** read the relevant file in [`handbook/`](handbook/), then answer the linked Question Bank prompts and complete the exercises without opening their separate answers/solutions.
- **Refresh before an interview:** open [`summaries/`](summaries/) for compact text cheat sheets or [`infographics/`](infographics/) for printable one-page visual refreshers. Both contain reminders, not full explanations.
- **Track progress:** use [`PROGRESS.md`](PROGRESS.md). A file existing on disk does not mean that its topic is complete.

Sections 1.1–1.12 have approved learning content, summaries, practice and printable infographics. The [1.7 review record](reviews/stage-4-section-reviews/01-07-modules-errors-and-serialization.md) records user approval on 2026-11-05. The [1.8 review record](reviews/stage-4-section-reviews/01-08-memory-management.md) records user approval on 2026-11-06. The [1.9 review record](reviews/stage-4-section-reviews/01-09-event-loop-and-scheduling.md) records user approval on 2026-11-06. The [1.10 review record](reviews/stage-4-section-reviews/01-10-promises-and-async-await.md) records user approval on 2026-11-06. The [1.11 review record](reviews/stage-4-section-reviews/01-11-async-coordination-patterns.md) records user approval on 2026-11-06 after the time-example corrections. The user approved the complete section 1.12 learning set on 2026-11-07. [Review record](reviews/stage-4-section-reviews/01-12-javascript-implementation-practice.md).

## Start here

Read these files in order before continuing the project in a new session:

1. [AGENTS.md](AGENTS.md)
2. [Project Context](docs/PROJECT_CONTEXT.md)
3. [Roadmap](ROADMAP.md)
4. [Curriculum](CURRICULUM.md)
5. [Master Question Inventory](research/MASTER_QUESTION_INVENTORY.md)
6. [Coverage Map](coverage/INVENTORY_TO_CURRICULUM.md)
7. [Progress](PROGRESS.md)
8. [Session Handoff](docs/SESSION_HANDOFF.md)

## Repository map

- `CURRICULUM.md` — canonical, complete Stage 1 curriculum.
- `research/` — Stage 0 methodology, sources, gaps and all 510 normalized question groups.
- `coverage/` — per-ID mapping from the inventory to curriculum sections.
- `handbook/` — 19 domain TOCs and 147 chapter files: sections 1.1–1.12 are approved, and 135 remain placeholders.
- `summaries/` — one compact pre-interview cheat sheet per domain; only already-authored sections are filled.
- `infographics/` — print-ready A4 PDFs and editable SVG sources, mirroring authored handbook sections.
- `question-bank/` — 312 approved questions for sections 1.1–1.12, with separate model answers; other domains remain placeholders.
- `exercises/` — separate prompt and solution trees.
- `playground/` — future executable practice areas; intentionally dependency-free for now.
- `templates/` — chapter, question, exercise, solution, system-design and handoff contracts.
- `reviews/` — Stage 3 calibration, Stage 4 reviews and Stage 5 audit records.
- `PROGRESS.md` — simple checkbox tracking; placeholders do not count as progress.

## Guiding sequence

`Research → Coverage → Learn → Recall → Understand → Explain → Code → Debug → Review → Design → Interview`

The project optimizes for realistic interview coverage and high-quality learning material, not infrastructure.
