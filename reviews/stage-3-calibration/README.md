# Stage 3 Calibration Review — 1.1 Execution Model, Declarations & Scope

> Status: `revised after first feedback — awaiting repeat user calibration review`
>
> Initial draft: `2026-09-23`; full Q&A rewrite and repeat verification: `2026-09-24`
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
| Handbook chapter | 1,416 lines; 15 connected teaching questions |
| Interview questions | 20 |
| Junior / Mid / Senior questions | 7 / 8 / 5 |
| Active-recall exercises | 9 |
| Exercise progression | recall → prediction → explanation → debugging → review → implementation → integrated challenge |
| Timed 30–60 second model answers | 4 |

Question formats include conceptual, compare/explain, output prediction, “why,” find-the-bug, debugging, code review/refactoring, practical scenario, interview communication and implementation.

## Curriculum Coverage Audit

| Curriculum requirement | Evidence |
|---|---|
| ECMAScript versus host environment | teaching question 12; Q12, Q19; EX05, EX09 |
| Execution contexts, call stack, environments and scope chain | teaching questions 5–7; Q08–Q10; EX03–EX04 |
| Global, function, block, lexical and module scope | teaching questions 4–5 and 12; Q02, Q12, Q17–Q19; EX03, EX09 |
| `var` / `let` / `const` lifecycle and redeclaration | teaching questions 1–3 and 11; Q01, Q03, Q11; EX01–EX02, EX06 |
| Hoisting and TDZ without the moved-code myth | teaching questions 6 and 8–10; Q04–Q05, Q16; EX01–EX04 |
| Shadowing and illegal shadowing | teaching questions 5 and 11; Q06, Q11, Q14; EX02, EX06 |
| Strict mode, accidental globals and `delete` | teaching questions 12–14; Q07, Q17–Q20; EX05, EX07, EX09 |

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
- Code-fence audit after rewrite: 128 fences checked (110 JavaScript, 4 HTML and 14 text/diagram fences); 98 valid JavaScript fences passed Script/Module syntax validation and 12 intentionally invalid examples produced the expected `SyntaxError`.
- Runtime behavior: 36 targeted Script/Module assertions passed with Node.js `v26.4.0`, including TDZ, function timing, loop bindings, classic-script globals, cross-script declaration conflicts, CommonJS-like wrapping and module/global lookup.
- Node.js CommonJS top-level behavior: checked through the Node module wrapper.
- Question/answer ID parity: 20/20.
- Exercise/solution ID parity: 9/9.
- Relative Markdown file and `JS-SCOPE-*` anchor links: passed.
- Canonical curriculum and coverage maps: unchanged.
- Chapter placeholders 1.2–1.12: unchanged.
- No content was added to neighboring curriculum topics.

## Calibration Review Prompts

Please evaluate:

1. Does the 15-question narrative now feel like one connected explanation from variables to interview analysis?
2. Are the foundations restored before specification-level terminology appears?
3. Is the predominantly Russian language clear, with enough English terminology for real interviews?
4. Is the 1,416-line size appropriate, or should later chapters split long topics differently?
5. Do the short answers, detailed explanations, examples and bridges have the right rhythm?
6. Are 20 active-recall questions and 9 exercises the right amount for one topic?
7. Do Junior/Mid/Senior labels feel realistic?
8. Does the exercise progression protect active recall and build toward review/debugging?
9. Should future chapters use the same Q&A structure and answer/rubric depth?

## Feedback Record

### 2026-09-24 — First calibration feedback

The first technically complete draft was rejected as a learning format: it felt like disconnected fragments, started too far inside the specification model, did not restore basic concepts and used language that was too difficult for a non-native English reader.

Requested correction:

- provide a detailed, connected explanation from beginning to end;
- use a question-and-answer format, beginning with fundamentals such as variables and scope;
- treat professional experience as context, not as permission to skip forgotten basics;
- write primarily in Russian and introduce English terms beside their Russian equivalent.

Applied revision:

- replaced the handbook's structure with 15 prerequisite-ordered teaching questions;
- moved precise internals after the basic variable/scope model;
- rewrote the Question Bank, answers, exercises and solutions in Russian;
- added the language and explanatory-flow rules to `docs/CONTENT_CONVENTIONS.md`;
- preserved 7/7 curriculum coverage, all five primary inventory groups and prompt/solution separation.

Stage 3 remains **in review**. The 1.1 checkbox in `PROGRESS.md` remains unchecked until the revised version receives user review.
