# Stage 4 Section Review — 1.3 Functions, Closures & Functional Patterns

> Status: `ready for user review — not approved`
>
> Rebuilt and locally verified: `2026-10-07`
>
> Gate: pending. Stop before section 1.4.

## Authorized Scope

This Stage 4 cycle covers exactly **1.3. Functions, Closures & Functional Patterns**.

Primary inventory groups:

- `JS-12`
- `JS-13`
- `JS-14`
- `JS-15`
- `JS-16`
- `JS-17`
- `JS-18`
- `JS-19`
- `JS-20`
- `JS-21`

The canonical map places `JS-16–JS-18` in 1.3 even though section 1.4 has overlapping curriculum bullets. This cycle therefore covers function-specific invocation behavior: regular/lexical `this`, detached methods, context preservation, `call` / `apply` / `bind`, constructibility and the practical `new` model.

Section 1.4 retains the full object model: object creation strategies, `Object.create`, prototype chains, constructor/prototype relationships, classes/inheritance, property descriptors, getters/setters and object-model trade-offs. No curriculum, inventory or coverage-map row was changed.

## Consistency Correction

The first rejected 1.3 implementation was removed completely before this rebuild. The repository was returned to commit `7b50a0d2382c181c0baa24120c68a26d000efd4f` and rebuilt from the approved 1.1/1.2 artifacts.

This revision:

- uses the established `### 🎯 1. ...` / `### 🔬 1. ...` heading grammar;
- follows the same chapter hierarchy and connected Q&A rhythm;
- matches the existing Question Bank, answer, exercise and solution metadata;
- keeps the summary dense rather than chapter-like;
- uses the approved infographic grid, palette, panels, arrows, tables and print margins;
- records the project-wide consistency rule in `AGENTS.md`, project context and content conventions.

After the first rebuild pass, all Russian learning artifacts received a complete editorial rewrite. Russian sentence structure is now primary; English remains at the first useful introduction of a canonical term, in exact API names, code and standardized metadata. The pass covered the handbook, Question Bank, separate answers, exercise prompts, separate solutions and compact summary rather than correcting only isolated quotations.

A follow-up user review found the same older code-switching pattern in the 1.1/1.2 portions of the shared summary file. The complete filled summary set, 1.1–1.3, was then edited in one pass without changing technical coverage or filling future placeholders.

## Artifacts

- [Handbook chapter](../../handbook/01-javascript-and-async-programming/03-functions-closures-and-functional-patterns.md)
- [Compact pre-interview summary](../../summaries/01-javascript-and-async-programming.md#13-functions-closures--functional-patterns)
- [Print-ready English infographic](../../infographics/01-javascript-and-async-programming/03-functions-closures-and-functional-patterns.pdf)
- [Editable infographic source](../../infographics/01-javascript-and-async-programming/03-functions-closures-and-functional-patterns.svg)
- [Question prompts](../../question-bank/by-domain/01-javascript-and-async-programming.md#13-функции-замыкания-и-функциональные-паттерны)
- [Separate question answers](../../question-bank/answers/by-domain/01-javascript-and-async-programming.md#13-функции-замыкания-и-функциональные-паттерны)
- [Exercise prompts](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#13-функции-замыкания-и-функциональные-паттерны)
- [Separate exercise solutions](../../exercises/solutions/by-domain/01-javascript-and-async-programming.md#13-функции-замыкания-и-функциональные-паттерны)

## Size and Mix

| Artifact | Count / size |
|---|---:|
| Handbook chapter | 1,998 lines; 26 connected teaching questions |
| Compact summary | one dense section inside the existing domain summary |
| Interview questions | 28 |
| Junior / Mid / Senior | 9 / 13 / 6 |
| Primary formats | 4 conceptual / 4 compare / 12 output / 1 find-the-bug / 2 debugging / 2 code-review / 2 implementation / 1 performance-diagnosis |
| Active-recall exercises | 12 |
| Exercise progression | recall → prediction → explanation → debugging → code review → implementation → integrated challenge |
| Timed 30–60 second model answers | 6 |

Secondary question tags also cover `why`, practical scenario, refactoring, performance, architecture and interview communication.

## Curriculum Coverage Audit

| Curriculum requirement | Evidence |
|---|---|
| Declarations, expressions, named expressions and arrows | teaching questions 1–4; Q01–Q03, Q07, Q16–Q17, Q28; EX01–EX02, EX11–EX12 |
| First-class/HOF functions and callbacks | teaching questions 9–10; Q06, Q12, Q20, Q23, Q26, Q28; EX01, EX06, EX08, EX11–EX12 |
| Defaults, rest, destructuring, `arguments` and arity | teaching questions 5–8; Q04–Q05, Q10–Q12, Q15, Q28; EX01–EX02, EX08, EX12 |
| Closures, factories, encapsulation and memoization | teaching questions 17–20; Q08, Q18, Q20, Q24, Q27–Q28; EX03, EX08–EX09, EX11–EX12 |
| Loop closure and retained memory | teaching questions 21–22; Q19, Q25–Q28; EX04, EX07, EX09, EX11–EX12 |
| Pure functions, side effects and practical immutability | teaching question 23; Q09, Q18, Q23, Q27–Q28; EX03, EX06, EX09–EX12 |
| Currying, partial application, composition and pipelines | teaching questions 24–25; Q21–Q22, Q28; EX10, EX12 |

Result: **7/7 curriculum bullets covered**.

## Inventory Evidence Crosswalk

| Inventory ID | Handbook | Question Bank | Practice |
|---|---|---|---|
| `JS-12` | forms, creation timing, named-expression scope | Q01–Q03, Q28 | EX01–EX02, EX12 |
| `JS-13` | arrow/regular semantics, lexical context | Q01, Q05, Q07, Q16, Q28 | EX01, EX05, EX11–EX12 |
| `JS-14` | first-class functions, callback contracts, HOF | Q06, Q12, Q20, Q23, Q26, Q28 | EX01, EX06, EX08, EX11–EX12 |
| `JS-15` | lexical capture, factories, loops, memoization, memory | Q08, Q18–Q20, Q24–Q28 | EX03–EX04, EX07–EX09, EX11–EX12 |
| `JS-16` | regular invocation `this`, lexical arrow `this` | Q07, Q13–Q14, Q16, Q26, Q28 | EX05, EX11–EX12 |
| `JS-17` | `call`, `apply`, `bind`, context preservation | Q13–Q16, Q26, Q28 | EX05, EX11–EX12 |
| `JS-18` | practical `new` model, arrow non-constructibility | Q01, Q07, Q17, Q28 | EX01, EX11–EX12 |
| `JS-19` | parameters/default/rest/destructuring/`arguments`/arity | Q04–Q05, Q10–Q12, Q15, Q28 | EX01–EX02, EX08, EX12 |
| `JS-20` | currying, partial application, compose/pipe order | Q21–Q22, Q28 | EX10, EX12 |
| `JS-21` | purity, effects, ownership and immutability | Q09, Q18, Q23, Q27–Q28 | EX03, EX06, EX09–EX12 |

Result: **10/10 mapped inventory groups have explicit handbook, Question Bank and practice evidence**.

## `call` / `apply` / `bind` Depth

The rebuild treats this as a recurring interview topic rather than a short API comparison:

- invocation form and detached-method context loss;
- immediate `call`/`apply` versus deferred `bind`;
- argument list, array-like and iterable distinctions;
- strict/sloppy receiver normalization;
- arrow lexical `this` with arguments still passed/bound;
- method borrowing and the modern `Object.hasOwn` alternative;
- bound leading arguments and partial application;
- repeated `bind` receiver/argument behavior;
- new function identity and listener cleanup;
- bound `name`/`length`;
- bound functions used with `new`;
- production choice among one-off call, stored bound callback and arrow adapter.

## Active-Recall Separation

- 28 question IDs have 28 matching answer IDs.
- 12 exercise IDs have 12 matching solution IDs.
- Questions and answers are in separate trees.
- Exercise conditions and solutions are in separate trees.
- The handbook links to prompts and Question Bank rather than revealing solutions inline.

## Local Verification

- 158 JavaScript fences across the 1.3 chapter/question/practice set passed syntax checking.
- Three intentionally invalid constructor examples are explicitly labeled and commented, so the surrounding runnable fences remain valid.
- 69 targeted runtime assertions passed for declaration timing, named-expression scope, defaults, rest/`arguments`, `length`, callback signatures, context loss, `call`/`apply`/`bind`, arrow lexical `this`, `new`, closures, loop bindings, memoization, immutability and composition order.
- Question/answer ID parity: 28/28.
- Exercise/solution ID parity: 12/12.
- Repository-relative Markdown links and anchors: 907 checked, 0 broken.
- Complete Russian editorial audit: handbook, Question Bank, answers, prompts and solutions for 1.3 plus all filled summary subsections 1.1–1.3 checked; unintended sentence-level code switching removed.
- PDF/SVG: English-only A4 portrait; PDF is exactly one page; rendered output has white background, printer-safe margins, color-coded panels, tables, arrow flows and no visible clipping or overlap.
- Approved 1.1/1.2 handbook, Question Bank, practice and infographic content remains unchanged; only their shared summary wording received the explicit user-requested editorial correction.
- Sections 1.4–1.12 remain placeholders.
- Canonical curriculum, inventory and coverage-map changes: 0.

## Review Prompts

Please evaluate:

1. Does the chapter now read as the same project as 1.1/1.2?
2. Is the path `function value → call → callback → capture → lifecycle → functional patterns` connected?
3. Is `call` / `apply` / `bind` deep enough for repeated real interviews?
4. Are defaults, `arguments`, rest and `length` explained without losing the main flow?
5. Does the closure section clearly separate binding, snapshot, mutation and reassignment?
6. Are retained-memory and cache risks practical rather than alarmist?
7. Are pure functions and immutability connected to identity/ownership from 1.2?
8. Are currying/partial/composition presented with realistic limits?
9. Is the 1.3/1.4 boundary explicit and credible?
10. Does the infographic now function as a visual recall sheet when printed?

## Review Gate

Section 1.3 is **ready for user review, not approved**. Its progress checkbox remains unchecked. Do not begin section 1.4 or fill any later placeholder without explicit user authorization.
