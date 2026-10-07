# Roadmap

Every stage has an approval gate. Do not start the next stage without explicit user authorization.

## Stage 0 — Research & Master Question Inventory — Complete

Deliverables completed:

- broad research across 94 artifacts and 63 independent source families;
- approximately 2,350 useful raw prompts/variants reviewed;
- normalization and deduplication into 510 question groups;
- domain, level, question-type, frequency and relevance classification;
- gap analysis, source list and research limitations.

Canonical artifact: `research/MASTER_QUESTION_INVENTORY.md`.

## Stage 1 — Curriculum & Coverage Audit — Complete

Deliverables completed:

- 19-domain `Domain → Section → Topic → Subtopic` curriculum;
- Fundamentals → Professional/Mid → Advanced/Senior progression;
- explicit modern, legacy and survey-depth distinctions;
- 510/510 coverage mapping with zero unmapped groups;
- interview-value audit.

Canonical artifact: `CURRICULUM.md`.

## Stage 2 — Repository Skeleton — Complete

Deliverables:

- Git repository and root documentation;
- complete Stage 0 and Stage 1 artifacts;
- project context, conventions, decisions and session handoff;
- `PROGRESS.md`;
- 19 domain TOCs and 147 chapter placeholders;
- per-ID coverage map for all 510 inventory groups;
- question-bank, exercise, solution, playground and review skeletons;
- chapter/question/exercise/system-design templates.

Restrictions honored:

- no textbook chapters filled;
- no generated bulk question bank;
- no solved exercises;
- no runtime dependencies or application infrastructure.

Exit gate: structural verification must pass, then stop for user review.

## Stage 3 — Calibration Section — Complete

Authorized calibration boundary: **1.1. Execution Model, Declarations & Scope only**.

The chapter, Question Bank, separate answers, exercise prompts and separate solutions are the approved artifact structure. A later experiment that merged theory, questions and answers was rejected and reverted. The accepted revision keeps the required technical depth, uses clear conversational Russian, adds several focused real-life analogies and moves specification-heavy detail into skippable blocks. The current summary and linear print infographic are also approved.

Calibrated:

- breadth and depth;
- chapter size and tone;
- examples and terminology;
- interview-core versus optional-depth labeling;
- compact pre-interview summaries;
- realistic interview questions;
- 30–60 second answers;
- exercises and challenges;
- code/debug/review balance.

Local coverage and quality audit: complete. The user approved the complete 1.1 learning set on 2026-10-01. Stage 3 is complete; do not continue into section 1.2 automatically.

## Stage 4 — Incremental Build — In Progress

The first cycle covered **1.2. Values, Types, Equality & Coercion only** and was approved on 2026-10-06. The second cycle covers **1.3. Functions, Closures & Functional Patterns only**. Its artifact set was rebuilt against the approved 1.1/1.2 structural and visual baseline, received a complete Russian editorial pass, was locally verified and was marked ready for user review on 2026-10-07. Work stops before section 1.4; the 1.3 gate remains pending.

Work one major section at a time:

1. reread current conventions and calibration feedback;
2. research modern/time-sensitive details using primary sources;
3. author the authorized section;
4. add related question-bank entries;
5. add prompts and separately stored solutions;
6. verify examples and executable exercises;
7. map covered inventory IDs;
8. update progress, changelog and handoff;
9. stop for review.

## Stage 5 — Final Coverage Audit — Not Started

- Recheck every original question group.
- Confirm handbook, question-bank and practice coverage.
- Repeat web research for changed or newly common interview topics.
- Add justified new groups without renumbering existing IDs.
- Audit Junior/Mid/Senior balance.
- Audit conceptual, output, coding, debugging, review, performance and system-design formats.
- Audit modern/legacy labels, stale claims and executable examples.
- Produce the final coverage report and identify remaining role-specific tracks.
