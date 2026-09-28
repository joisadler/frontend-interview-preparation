# Frontend Interview Preparation

Personal **Q&A Frontend Interview Handbook + Coding Practice Repository** for Mid → Senior Frontend Engineer interviews.

This is not a beginner course. The project is designed to restore active recall and the ability to independently explain, implement, debug, review and design frontend systems.

## Current status

- Stage 0 — Research & Master Question Inventory: complete.
- Stage 1 — Curriculum & Coverage Audit: complete.
- Stage 2 — Repository Skeleton: complete after structural verification.
- Stage 3 — Calibration Section: section 1.1 consolidated into one shorter Q&A chapter after the third calibration feedback; awaiting review.
- Stage 4 — Incremental Build: not started.
- Stage 5 — Final Coverage Audit: not started.

Only the authorized calibration topic—**1.1. Execution Model, Declarations & Scope**—has been authored. Sections 1.2+ remain placeholders and Stage 4 has not started.

## How to use the learning material

- **Learn or restore a topic:** read one relevant file in [`handbook/`](handbook/) from top to bottom. The theory, interview questions and model answers are one Q&A narrative.
- **Practice active recall:** complete the separate exercises without opening their solutions.
- **Refresh before an interview:** open [`summaries/`](summaries/) and use the compact domain cheat sheets. They contain reminders, not full explanations.
- **Track progress:** use [`PROGRESS.md`](PROGRESS.md). A file existing on disk does not mean that its topic is complete.

At the current calibration stage, only section 1.1 has real learning content and a filled summary. The remaining summary sections are navigation placeholders, not generated material.

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
- `handbook/` — 19 domain TOCs and 147 chapter placeholders.
- `summaries/` — one compact pre-interview cheat sheet per domain; only already-authored sections are filled.
- `question-bank/` — stable-ID index retained for coverage audits; it is not a separate learning route.
- `exercises/` — separate prompt and solution trees.
- `playground/` — future executable practice areas; intentionally dependency-free for now.
- `templates/` — chapter, question, exercise, solution, system-design and handoff contracts.
- `reviews/` — Stage 3 calibration, Stage 4 reviews and Stage 5 audit records.
- `PROGRESS.md` — simple checkbox tracking; placeholders do not count as progress.

## Guiding sequence

`Research → Coverage → Q&A learning → Recall → Code → Debug → Review → Design → Interview`

The project optimizes for realistic interview coverage and high-quality learning material, not infrastructure.
