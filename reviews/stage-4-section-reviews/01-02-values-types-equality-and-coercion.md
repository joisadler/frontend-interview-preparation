# Stage 4 Section Review — 1.2 Values, Types, Equality & Coercion

> Status: `approved by user on 2026-10-06`
>
> Authored and locally verified: `2026-10-01`
>
> Gate: passed. Section 1.2 is complete; section 1.3 is the next separate Stage 4 cycle.

## Authorized Scope

This Stage 4 cycle covers exactly **1.2. Values, Types, Equality & Coercion**.

Primary inventory groups:

- `JS-05`
- `JS-06`
- `JS-07`
- `JS-08`
- `JS-09`
- `JS-10`
- `JS-11`
- `JS-40`

Limited cross-references (`JS-01`, `JS-21`, `JS-34`, `JS-37`) are used only where `const`, practical immutability, shallow copy or `Symbol.toPrimitive` is required to explain 1.2. They are not marked complete here.

## Artifacts

- [Handbook chapter](../../handbook/01-javascript-and-async-programming/02-values-types-equality-and-coercion.md)
- [Compact pre-interview summary](../../summaries/01-javascript-and-async-programming.md#12-values-types-equality--coercion)
- [Print-ready English infographic](../../infographics/01-javascript-and-async-programming/02-values-types-equality-and-coercion.pdf)
- [Editable infographic source](../../infographics/01-javascript-and-async-programming/02-values-types-equality-and-coercion.svg)
- [Question prompts](../../question-bank/by-domain/01-javascript-and-async-programming.md#12-значения-типы-равенство-и-преобразование-типов)
- [Separate question answers](../../question-bank/answers/by-domain/01-javascript-and-async-programming.md#12-значения-типы-равенство-и-преобразование-типов)
- [Exercise prompts](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#12-значения-типы-равенство-и-преобразование-типов)
- [Separate exercise solutions](../../exercises/solutions/by-domain/01-javascript-and-async-programming.md#12-значения-типы-равенство-и-преобразование-типов)

## Size and Mix

| Artifact | Count / size |
|---|---:|
| Handbook chapter | 1,524 lines; 18 connected teaching questions; 3 collapsed precision blocks |
| Compact summary | one dense section inside the existing domain summary |
| Interview questions | 24 |
| Junior / Mid / Senior questions | 8 / 10 / 6 |
| Primary question formats | 5 conceptual / 3 compare / 8 output / 1 recall / 2 debugging / 1 find-the-bug / 2 code-review / 1 practical-scenario / 1 implementation |
| Active-recall exercises | 10 |
| Exercise progression | recall → prediction → explanation → debugging → code review → implementation → integrated challenge |
| Timed 30–60 second model answers | 5 |

Question formats include conceptual/explain, compare, output prediction, why, recall, find-the-bug, debugging, production scenario, code review/refactoring, practical architecture, implementation/testing, trade-off and interview communication.

## Curriculum Coverage Audit

| Curriculum requirement | Evidence |
|---|---|
| Primitive/object values; identity, mutation and shared references | teaching questions 1–3; Q01–Q03, Q12, Q21, Q24; EX01, EX03, EX06, EX10 |
| Pass-by-value and object reference as value | teaching question 4; Q03, Q24; EX03, EX10 |
| `typeof`, `null`, `undefined`, `Symbol`, `BigInt` | teaching questions 5–6; Q04–Q05; EX01–EX02, EX08 |
| `NaN`, infinities, `-0`, floating-point precision | teaching questions 7–8; Q06, Q13–Q14, Q20, Q22–Q23; EX02, EX05, EX09–EX10 |
| Truthy/falsy and nullish values | teaching question 9; Q07–Q08; EX01, EX04, EX08, EX10 |
| `||`, `??`, optional chaining and short-circuit | teaching questions 10–11; Q08–Q10, Q24; EX04, EX08, EX10 |
| `==`, `===`, `Object.is`, SameValueZero | teaching questions 12–13; Q11, Q17, Q19–Q20, Q24; EX01–EX02, EX07, EX09–EX10 |
| Explicit/implicit coercion; `ToPrimitive`, `valueOf`, `toString` | teaching questions 14–17; Q15–Q19, Q22, Q24; EX02, EX05, EX07–EX08, EX10 |
| Output prediction for conversion and equality | teaching question 18; Q02–Q04, Q06–Q10, Q12–Q18, Q24; EX02–EX04, EX07, EX10 |

Result: **9/9 curriculum bullets covered**.

## Inventory Evidence Crosswalk

| Inventory ID | Handbook | Question Bank | Practice |
|---|---|---|---|
| `JS-05` | primitives/objects, identity, mutation, shared references, shallow-copy boundary | Q01–Q03, Q12, Q21, Q24 | EX01, EX03, EX06, EX10 |
| `JS-06` | `typeof`, null/undefined, Symbol/BigInt and historical oddities | Q01, Q04–Q06, Q22 | EX01–EX02, EX08, EX10 |
| `JS-07` | special numbers, precision, comparison and money guidance | Q06, Q13–Q14, Q20, Q22–Q24 | EX02, EX05, EX09–EX10 |
| `JS-08` | boolean contexts, falsy/nullish and defaults | Q07–Q09, Q15, Q24 | EX01–EX02, EX04, EX08, EX10 |
| `JS-09` | four equality semantics and object identity | Q11–Q12, Q17, Q19–Q20, Q24 | EX01–EX02, EX07, EX09–EX10 |
| `JS-10` | conversion pipeline, `+`, comparisons and `ToPrimitive` | Q13, Q15–Q19, Q22, Q24 | EX02, EX05, EX07–EX08, EX10 |
| `JS-11` | pass-by-value and copied object reference value | Q03, Q21, Q24 | EX03, EX06, EX10 |
| `JS-40` | short-circuit, nullish coalescing and optional chaining | Q08–Q10, Q24 | EX04, EX08, EX10 |

Result: **8/8 mapped inventory groups have explicit handbook, Question Bank and practice evidence**. Canonical curriculum and coverage-map rows remain unchanged.

## Active-Recall Separation

- 24 question IDs have 24 matching answer IDs.
- 10 exercise IDs have 10 matching solution IDs.
- Question prompts and answers remain in separate files.
- Exercise prompts progress from recall to integrated production review; expected outputs and repairs remain only in the solution file.
- The handbook links to prompts, not directly to revealed solutions.

## Local Verification

- 135 JavaScript fences in the 1.2 artifact set were audited: 132 valid fences passed syntax checking and 3 explicitly labeled invalid optional/nullish examples failed with the expected `SyntaxError`.
- 108 targeted runtime assertions passed for identity, pass-by-value, numeric edges, defaulting, optional chaining, equality, coercion, `ToPrimitive`, Question Bank outputs and representative implementations.
- Question/answer ID parity: 24/24.
- Exercise/solution ID parity: 10/10.
- Relative Markdown links and anchors: 397 checked, 0 broken.
- PDF/SVG: English-only A4 portrait source and one-page print PDF; rendered output checked for clipping, overlap, legibility, white background and printer-safe margins.
- Canonical curriculum, inventory and coverage-map changes: 0.
- Section 1.1 learning artifacts: unchanged; its summary subsection remains byte-for-byte unchanged.
- Sections 1.3–1.12: unchanged placeholders.
- `git diff --check`: passed.

## Review Prompts

Please evaluate:

1. Does the path from values/identity to equality and coercion feel connected rather than encyclopedic?
2. Is the distinction between primitive immutability, binding reassignment and object mutation clear enough?
3. Does pass-by-value avoid both the “objects are copied” and “JavaScript is pass-by-reference” misconceptions?
4. Are numeric edge cases and money guidance practical without taking over the chapter?
5. Are `||`/`??` and optional-chaining traps explained at the right depth?
6. Does the equality matrix make `===`, SameValue and SameValueZero easy to recall?
7. Is `ToPrimitive` precise enough for Senior follow-ups but still skippable on a first pass?
8. Are 24 questions and 10 exercises proportionate to this section's breadth?
9. Is the summary genuinely useful for last-minute recall rather than a second chapter?
10. Does the one-page infographic remain readable when printed at 100% on A4?

## Review Gate

The user completed the review and approved the complete section 1.2 artifact set on 2026-10-06 with no requested corrections. The section 1.2 progress checkbox is checked. Section 1.3 remains an untouched placeholder and must be handled as a new, separately bounded Stage 4 cycle; stop before section 1.4.
