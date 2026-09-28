# Session Handoff

## Current state

- Last completed stage: Stage 2 — Repository Skeleton.
- Active stage: Stage 3 — Calibration Section.
- Authorized boundary: `1.1. Execution Model, Declarations & Scope` only.
- Three calibration feedback rounds have been applied; user review of the third version is pending.
- Stage 3 is not complete. Section 1.2 and Stage 4 are not authorized.

## Current learning format

The third feedback rejected the three-file route “theory → separate questions → separate answers” as too long and inconvenient.

The accepted design to evaluate now is:

1. one handbook chapter read from top to bottom;
2. each concept introduced as a realistic interview question;
3. a short 30–60 second answer directly below it;
4. only the explanation, example or trap needed to understand that answer;
5. separate prompts/solutions only for active-recall exercises;
6. a highly compressed, print-first summary for last-minute refresh.

## What exists for 1.1

- [One 731-line Q&A chapter](../handbook/01-javascript-and-async-programming/01-execution-model-declarations-and-scope.md): 20 stable interview-question IDs plus two supporting bridge/method questions.
- [One 43-line print summary](../summaries/01-javascript-and-async-programming.md), reduced from 154 lines and containing no code fences.
- A lightweight [stable question-ID index](../question-bank/by-domain/01-javascript-and-async-programming.md); no duplicate model-answer reading step.
- 9 progressive [exercise prompts](../exercises/prompts/by-domain/01-javascript-and-async-programming.md).
- 9 [separately stored exercise solutions](../exercises/solutions/by-domain/01-javascript-and-async-programming.md).
- Coverage evidence for `JS-01`, `JS-02`, `JS-03`, `JS-04`, `JS-22`.

## Scope and structure preserved

- All seven curriculum bullets for 1.1 remain covered.
- All 20 existing `JS-SCOPE-Q01–Q20` anchors remain present exactly once.
- All 9 exercise IDs and separate solutions remain unchanged.
- The canonical curriculum, Master Question Inventory and coverage map remain unchanged.
- Handbook chapters 1.2–1.12 and summary content for 1.2+ remain placeholders.
- The `question-bank/` placeholder tree remains only for stable indexes/Stage 2 compatibility; future teaching answers belong inline in handbook chapters.

## Next permitted action

Review the new section 1.1 from top to bottom and the compressed summary. Evaluate whether the route is now fast enough, conversational enough and still complete enough for real interviews. Do not author 1.2 or begin Stage 4 without explicit permission.

## Calibration questions still open

- Is 731 lines acceptable now that it replaces the former 2,378-line route across the chapter, question file and answer file?
- Does the repeated pattern “question → short answer → explanation/example” match the intended format?
- Are the short answers natural enough to say aloud on an interview?
- Is the 43-line summary dense enough for printing and last-minute repetition?
- Are any remaining optional Senior/legacy details still disproportionate?

## Required reading for the next session

`AGENTS.md` → `docs/PROJECT_CONTEXT.md` → `ROADMAP.md` → `CURRICULUM.md` section 1.1 → `JS-01–04,22` in the inventory/coverage map → `docs/CONTENT_CONVENTIONS.md` → `PROGRESS.md` → this handoff → `reviews/stage-3-calibration/README.md`.
