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

The first cycle covered **1.2. Values, Types, Equality & Coercion only** and was approved on 2026-10-06. The second cycle covered **1.3. Functions, Closures & Functional Patterns only** and was approved on 2026-10-07. The third cycle covered **1.4. `this`, Invocation & Object Model only** and was approved on 2026-10-08. The fourth cycle covered **1.5. Arrays, Transformations & Copying only** and was approved on 2026-11-04. The fifth cycle covered **1.6. Collections, Symbols & Iteration only** and was approved on 2026-11-04. The sixth cycle covered **1.7. Modules, Errors & Serialization only** and was approved on 2026-11-05. The seventh cycle covered **1.8. Memory Management** and was approved on 2026-11-06. The eighth cycle covered **1.9. Event Loop & Scheduling** and was approved on 2026-11-06. The ninth cycle covered **1.10. Promises & `async`/`await`** and was approved on 2026-11-06. The tenth cycle covered **1.11. Async Coordination Patterns** and was approved on 2026-11-06 after replacing unexplained time notation with explicit examples. The approved set was published in `252da35`. The eleventh cycle covered **1.12. JavaScript Implementation Practice** and was approved on 2026-11-07. This completes Domain 1. The user requested publication of the approved set. The next domain begins with 2.1 after separate authorization.

Work one major section at a time:

1. follow the required reading order in `AGENTS.md`, then reread current conventions, calibration feedback and approved reference artifacts;
2. research modern/time-sensitive details using primary sources;
3. author the authorized section;
4. add related question-bank entries;
5. add prompts and separately stored solutions;
6. add the compact domain-summary subsection and required English A4 portrait PDF/editable SVG infographic;
7. verify examples and executable exercises, Russian wording, artifact separation, consistency with approved references and the final rendered PDF;
8. record curriculum/inventory evidence and actual verification results without changing canonical mappings unless scope changes are explicitly authorized;
9. synchronize current status, navigation, progress, changelog and handoff, leaving the new section ready for user review and its checkbox unchecked;
10. complete commit/push if authorized, then stop for user review; publication does not approve the content or authorize the next section.

## Stage 5 — Final Coverage Audit — Not Started

- Recheck every original question group.
- Confirm handbook, question-bank and practice coverage.
- Repeat web research for changed or newly common interview topics.
- Add justified new groups without renumbering existing IDs.
- Audit Junior/Mid/Senior balance.
- Audit conceptual, output, coding, debugging, review, performance and system-design formats.
- Audit modern/legacy labels, stale claims and executable examples.
- Produce the final coverage report and identify remaining role-specific tracks.
