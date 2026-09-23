# Stage 3 Calibration Review — 1.1 Execution Model, Declarations & Scope

> Status: `awaiting user calibration review`
>
> Authored and locally verified: `2026-09-23`
>
> Gate: do not start section 1.2 or Stage 4 without explicit user approval.

## Authorized Scope

This calibration covers exactly **1.1. Execution Model, Declarations & Scope**.

Primary inventory groups:

- `JS-01`
- `JS-02`
- `JS-03`
- `JS-04`
- `JS-22`

Limited cross-references (`JS-12`, `JS-15`, `BR-05`, `JS-41–42`) are used only where function timing, lexical capture, the call stack or module scope is necessary to explain 1.1. They are not marked complete.

## Calibration Artifacts

- [Handbook chapter](../../handbook/01-javascript-and-async-programming/01-execution-model-declarations-and-scope.md)
- [Question prompts](../../question-bank/by-domain/01-javascript-and-async-programming.md)
- [Separate question answers](../../question-bank/answers/by-domain/01-javascript-and-async-programming.md)
- [Exercise prompts](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md)
- [Separate exercise solutions](../../exercises/solutions/by-domain/01-javascript-and-async-programming.md)

## Size and Mix

| Artifact | Count / size |
|---|---:|
| Handbook chapter | 907 lines |
| Interview questions | 20 |
| Junior / Mid / Senior questions | 7 / 8 / 5 |
| Active-recall exercises | 9 |
| Exercise progression | recall → prediction → explanation → debugging → review → implementation → integrated challenge |
| Timed 30–60 second model answers | 4 |

Question formats include conceptual, compare/explain, output prediction, “why,” find-the-bug, debugging, code review/refactoring, practical scenario, interview communication and implementation.

## Curriculum Coverage Audit

| Curriculum requirement | Evidence |
|---|---|
| ECMAScript versus host environment | chapter §1; Q12, Q19; EX05, EX09 |
| Execution contexts, call stack, environments and scope chain | chapter §2–3; Q08–Q10; EX03–EX04 |
| Global, function, block, lexical and module scope | chapter §4 and §10; Q02, Q12, Q17–Q19; EX03, EX09 |
| `var` / `let` / `const` lifecycle and redeclaration | chapter §5 and §9; Q01, Q03, Q11; EX01–EX02, EX06 |
| Hoisting and TDZ without the moved-code myth | chapter §6–8; Q04–Q05, Q16; EX01–EX04 |
| Shadowing and illegal shadowing | chapter §9; Q06, Q11, Q14; EX02, EX06 |
| Strict mode, accidental globals and `delete` | chapter §11; Q07, Q17–Q20; EX05, EX07, EX09 |

Result: **7/7 curriculum bullets covered**.

## Inventory Evidence Crosswalk

| Inventory ID | Handbook | Question Bank | Practice |
|---|---|---|---|
| `JS-01` | declaration lifecycle, redeclaration, production choice | Q01, Q03, Q06, Q11, Q13, Q15 | EX01–EX02, EX06–EX09 |
| `JS-02` | environments, scopes, globals, loop bindings | Q02, Q08–Q10, Q12–Q13, Q17–Q20 | EX03–EX05, EX07–EX09 |
| `JS-03` | instantiation, hoisting, TDZ, function timing | Q03–Q05, Q16 | EX01–EX04, EX07, EX09 |
| `JS-04` | shadowing, declaration conflicts, early errors | Q06, Q11, Q14, Q18 | EX02, EX06, EX09 |
| `JS-22` | strict mode, accidental globals, property deletion | Q07, Q12, Q15, Q17–Q20 | EX05, EX07, EX09 |

Result: **5/5 mapped inventory groups have handbook, question and/or practice evidence**. The canonical rows in `coverage/coverage-map.tsv` remain unchanged and still map all five groups to 1.1.

## Active-Recall Separation

- 20 question IDs have 20 matching answer IDs.
- 9 exercise IDs have 9 matching solution IDs.
- Question prompts and answers live in separate files.
- Exercise prompts use process-oriented evaluation checklists; expected outputs and repairs remain in the solution file.
- The handbook links to prompts, not directly to revealed solutions.

## Local Verification

- `git diff --check`: passed.
- Code-fence audit: 100 relevant fences checked (97 JavaScript and 3 HTML); 86 valid JavaScript fences passed syntax validation and 11 intentionally invalid fences produced the expected `SyntaxError`.
- Script execution: 80 valid Script blocks ran in isolated `node:vm` contexts; 30 targeted behavior assertions also passed with Node.js `v26.4.0`.
- ES-module behavior: 5 standalone Module blocks and 1 importing module graph linked and evaluated successfully.
- Node.js CommonJS top-level behavior: checked through the Node module wrapper.
- Question/answer ID parity: 20/20.
- Exercise/solution ID parity: 9/9.
- Relative Markdown file and `JS-SCOPE-*` anchor links: passed.
- Canonical curriculum and coverage maps: unchanged.
- Chapter placeholders 1.2–1.12: unchanged.
- No content was added to neighboring curriculum topics.

## Calibration Review Prompts

Please evaluate:

1. Is the 907-line chapter too long, too short or appropriate for one canonical topic?
2. Is the split between interview shorthand and specification terminology clear?
3. Is the Russian/English terminology balance comfortable?
4. Are examples dense enough without turning the chapter into an output-trivia collection?
5. Are 20 questions and 9 exercises the right amount for one topic?
6. Do Junior/Mid/Senior labels feel realistic?
7. Does the exercise progression protect active recall and build toward review/debugging?
8. Are the four 30–60 second answers useful models rather than scripts to memorize?
9. Should future chapters use the same amount of answer detail and rubric depth?

## Feedback Record

No user calibration feedback has been recorded yet.

Stage 3 remains **in review**. The 1.1 checkbox in `PROGRESS.md` remains unchecked until this review is complete.
