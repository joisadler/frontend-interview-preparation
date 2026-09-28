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

## Stage 3 — Calibration Section — Revising After Third Feedback

Authorized calibration boundary: **1.1. Execution Model, Declarations & Scope only**.

The first two revisions still produced an overly long learning route split between theory, questions and answers. The third feedback requires one shorter, ordered Q&A chapter with inline teaching answers, separate exercises only, and a much denser print-oriented summary. These changes are applied to section 1.1; another user review is required, so Stage 3 is not complete and section 1.2 is not authorized.

Calibrate:

- breadth and depth;
- chapter size and tone;
- examples and terminology;
- interview-core versus optional-depth labeling;
- compact pre-interview summaries;
- one-file Q&A learning flow without duplicated Question Bank answers;
- realistic interview questions;
- 30–60 second answers;
- exercises and challenges;
- code/debug/review balance.

Local coverage and quality audit: complete. Record user feedback and stop. Do not continue into another section automatically.

## Stage 4 — Incremental Build — Not Started

Work one major section at a time:

1. reread current conventions and calibration feedback;
2. research modern/time-sensitive details using primary sources;
3. author the authorized section as an ordered Q&A narrative with inline teaching answers;
4. update the stable question index without duplicating the learning content;
5. add exercise prompts and separately stored exercise solutions;
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
