# Session Handoff

## Current state

- Last completed stage: Stage 2 — Repository Skeleton.
- Active stage: Stage 3 — Calibration Section.
- Authorized boundary: `1.1. Execution Model, Declarations & Scope` only.
- Section 1.1 is authored and locally verified; user calibration review is pending.
- Stage 3 is not complete. Section 1.2 and Stage 4 are not authorized.

## What exists

- A full [1.1 handbook chapter](../handbook/01-javascript-and-async-programming/01-execution-model-declarations-and-scope.md).
- 20 [interview questions](../question-bank/by-domain/01-javascript-and-async-programming.md) across Junior, Mid and Senior levels.
- 20 [separately stored model answers](../question-bank/answers/by-domain/01-javascript-and-async-programming.md).
- 9 progressive [exercise prompts](../exercises/prompts/by-domain/01-javascript-and-async-programming.md).
- 9 [separately stored solutions](../exercises/solutions/by-domain/01-javascript-and-async-programming.md).
- A [Stage 3 calibration and coverage audit](../reviews/stage-3-calibration/README.md).
- Coverage evidence for all primary groups: `JS-01`, `JS-02`, `JS-03`, `JS-04`, `JS-22`.
- Unchanged canonical curriculum and mapping files.

## Verification state

- 7/7 curriculum bullets and 5/5 primary inventory groups covered.
- 20/20 question/answer IDs and 9/9 exercise/solution IDs matched.
- 100 relevant code fences were audited: 86 valid JavaScript fences passed syntax checks, 11 intentionally invalid fences failed as expected, and 3 HTML fences were inspected in their browser context.
- 80 Script blocks, 5 standalone Modules and 1 importing module graph were executed; 30 targeted behavior assertions passed with Node.js `v26.4.0`.
- Relative Markdown links, code outputs, early-error/declaration-instantiation distinctions and prompt/solution separation checked.
- Chapters 1.2–1.12 remain unchanged placeholders.

## Next permitted action

Review or revise section 1.1 using user calibration feedback. Do not author section 1.2, fill the rest of JavaScript or begin Stage 4 without explicit permission.

## Open decisions for calibration

- Accept or adjust the current chapter size and detail level.
- Accept or adjust the balance of interview shorthand and specification terminology.
- Accept or adjust the count/difficulty mix of 20 questions and 9 exercises.
- Decide whether future chapters should use the same depth for model answers and solution rubrics.
- Decide later, outside this microstage, whether role-specific React Native coverage becomes a separate track.

## Required reading for the next session

`AGENTS.md` → `docs/PROJECT_CONTEXT.md` → `ROADMAP.md` → `CURRICULUM.md` section 1.1 → `JS-01–04,22` in the inventory/coverage map → `docs/CONTENT_CONVENTIONS.md` → `PROGRESS.md` → this handoff → `reviews/stage-3-calibration/README.md`.
