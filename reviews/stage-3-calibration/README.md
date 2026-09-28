# Stage 3 Calibration Review — 1.1 Execution Model, Declarations & Scope

> Status: `third feedback applied — awaiting user calibration review`
>
> Gate: do not start section 1.2 or Stage 4 without explicit user approval.

## Authorized scope

Exactly **1.1. Execution Model, Declarations & Scope**.

Primary inventory groups: `JS-01`, `JS-02`, `JS-03`, `JS-04`, `JS-22`.

Limited cross-references: `JS-12` for function timing, `JS-15` for loop bindings, `BR-05` for the synchronous call stack and `JS-41–42` for module scope/automatic strict mode. They are not marked complete.

## Current artifacts

- [Single Q&A handbook chapter](../../handbook/01-javascript-and-async-programming/01-execution-model-declarations-and-scope.md)
- [Print-dense summary](../../summaries/01-javascript-and-async-programming.md)
- [Stable question-ID index](../../question-bank/by-domain/01-javascript-and-async-programming.md)
- [Exercise prompts](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md)
- [Separate exercise solutions](../../exercises/solutions/by-domain/01-javascript-and-async-programming.md)

## Third-version size and format

| Artifact | Current result |
|---|---:|
| Required learning route | 1 file / 731 lines |
| Previous route | 3 files / 2,378 lines |
| Reduction | 1,647 lines / about 69% |
| Q&A blocks | 20 stable question IDs + 2 supporting bridge/method questions |
| Separate conceptual answer files | 0 required |
| Summary | 43 total lines; 19 nonblank lines for 1.1 |
| Active-recall exercises | 9 prompts / 9 separate solutions |

Each handbook block now follows:

`interview question → short spoken answer → necessary explanation/example → next question`

Question formats remain varied: conceptual, compare/explain, output prediction, why, find-the-bug, debugging, code review, practical scenario and small implementation.

## Curriculum coverage

| Requirement | Evidence in integrated chapter |
|---|---|
| ECMAScript versus host environment | Q14–16, Q19 |
| Execution contexts, call stack, environments, scope chain | Q3–6 and nested block/stack question |
| Global, function, block, lexical, module scope | Q2–4, Q14–16 |
| `var` / `let` / `const`; declaration / initialization / assignment / redeclaration | Q1–2, Q10–11 |
| Hoisting and TDZ without moved-code myth | Q1, Q5, Q7–9 |
| Shadowing and illegal shadowing | Q4, Q10–12 |
| Strict mode, accidental globals and `delete` | Q13–16, Q18–20 |

Result: **7/7 curriculum bullets retained**.

## Inventory crosswalk

| Inventory ID | Handbook Q&A | Practice |
|---|---|---|
| `JS-01` | Q1–2, Q10–11, Q18 | EX01–02, EX06–09 |
| `JS-02` | Q3–6, Q14–19 | EX03–05, EX07–09 |
| `JS-03` | Q1, Q5, Q7–9 | EX01–04, EX07, EX09 |
| `JS-04` | Q10–12, Q19 | EX02, EX06, EX09 |
| `JS-22` | Q13–16, Q18, Q20 | EX05, EX07, EX09 |

Result: **5/5 primary inventory groups retained**. Canonical curriculum and coverage rows are unchanged.

## Separation rule after third feedback

- Teaching questions and answers are intentionally together in the handbook.
- `question-bank/` preserves stable IDs and links only; it is not a reading step.
- Only active-recall exercise prompts hide their solutions.
- 9 exercise IDs still match 9 solution IDs.

## Local verification — 2026-09-28

- 20/20 `JS-SCOPE-Q01–Q20` anchors occur exactly once in the chapter and index.
- 28 JavaScript fences passed syntax parsing; no syntax failures.
- 13 targeted runtime assertions passed for `var`, TDZ, `typeof`, function timing, lexical lookup, loop bindings, strict/sloppy globals, classic-script global properties and cross-script conflicts.
- 308 Markdown files checked; zero broken relative file links.
- 19/19 summary domain files and 147/147 subsection headings still match `PROGRESS.md`.
- Summary 1.1 has no fenced code blocks.
- 9/9 exercise prompt/solution IDs match; exercise content did not change.
- `CURRICULUM.md`, Master Question Inventory and coverage map did not change.
- Chapters 1.2–1.12 did not change.
- `git diff --check` passed.

## Feedback history

### 2026-09-24 — First feedback

Rejected the fragmented, specification-first, English-heavy draft. Requested a connected Russian explanation from fundamentals in Q&A form.

### 2026-09-27 — Second feedback

The connected version was better but still too academic and deep. Requested simpler language, real-life analogies and very short domain summaries.

### 2026-09-28 — Third feedback

The total route was still far too long and split between theory, questions and answers. Requested:

- one ordered Q&A document with answers directly under questions;
- no navigation between theory, prompts and model answers;
- separate files only for real exercises/solutions;
- a substantially shorter, ink-conscious printable summary;
- TDZ embedded directly into the lifecycle scheme.

Applied:

- merged all 20 stable interview questions into the main chapter;
- removed duplicated prompt/answer content from the required learning route;
- cut the route by about 69% while retaining 7/7 curriculum bullets and 5/5 inventory groups;
- reduced summary 1.1 from 154 to 43 total lines and integrated TDZ into the lifecycle arrow;
- updated repository conventions and templates so future chapters follow the same design.

## What to evaluate now

1. Can the chapter be read once, top to bottom, without opening another theory/question/answer file?
2. Is the balance “short spoken answer first, detail second” now right?
3. Is 731 lines acceptable for this broad subsection now that it replaces a 2,378-line route?
4. Is the 43-line summary dense enough for printing and repeated last-minute reading?
5. Which remaining question, if any, still feels too academic or too rare for interview preparation?

Stage 3 remains **in review**. The 1.1 checkbox remains unchecked.
