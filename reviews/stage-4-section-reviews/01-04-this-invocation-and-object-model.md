# Stage 4 Section Review — 1.4 `this`, Invocation & Object Model

> Status: `ready for user review — not approved`
>
> Authored and locally verified: `2026-10-08`
>
> Gate: open. Section 1.5 remains a separate cycle requiring explicit authorization.

## Authorized Scope

This Stage 4 cycle covers exactly **1.4. `this`, Invocation & Object Model**.

Primary inventory groups:

- `JS-23`
- `JS-24`
- `JS-25`
- `JS-26`
- `JS-27`
- `JS-28`
- `JS-39`

The approved section 1.3 remains authoritative for the function-specific `JS-16–JS-18` treatment of regular and lexical `this`, detached methods, `call` / `apply` / `bind`, constructibility and the practical `new` model. Section 1.4 reconnects to that foundation briefly and then develops the object model. Those IDs were not moved or counted again.

Arrays, array methods, copying, cloning, `structuredClone` and iteration protocols remain in section 1.5 or later. Section 1.4 mentions shallow behavior only where object integrity and shared references require it. No curriculum, inventory or coverage-map row changed.

## Artifacts

- [Handbook chapter](../../handbook/01-javascript-and-async-programming/04-this-invocation-and-object-model.md)
- [Compact pre-interview summary](../../summaries/01-javascript-and-async-programming.md#14-this-invocation--object-model)
- [Print-ready English infographic](../../infographics/01-javascript-and-async-programming/04-this-invocation-and-object-model.pdf)
- [Editable infographic source](../../infographics/01-javascript-and-async-programming/04-this-invocation-and-object-model.svg)
- [Question prompts](../../question-bank/by-domain/01-javascript-and-async-programming.md#14-this-вызов-функции-и-объектная-модель)
- [Separate question answers](../../question-bank/answers/by-domain/01-javascript-and-async-programming.md#14-this-вызов-функции-и-объектная-модель)
- [Exercise prompts](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#14-this-вызов-функции-и-объектная-модель)
- [Separate exercise solutions](../../exercises/solutions/by-domain/01-javascript-and-async-programming.md#14-this-вызов-функции-и-объектная-модель)

## Size and Mix

| Artifact | Count / size |
|---|---:|
| Handbook chapter | 1,779 lines; 28 connected teaching questions |
| Compact summary | one dense section inside the existing domain summary |
| Interview questions | 30 |
| Junior / Mid / Senior | 8 / 14 / 8 |
| Question tags | 16 output / 8 debugging / 8 compare / 6 why / 6 conceptual / 5 practical scenario / 5 code review / 4 explain / 3 architecture / 3 API design / 2 implementation / 2 interview communication / 1 find-the-bug / 1 legacy |
| Active-recall exercises | 14 |
| Exercise progression | recall → prediction → explanation → debugging → code review → implementation → integrated challenge |
| Timed 30–60 second model answers | 6 |

Tags are intentionally multi-valued; one question can exercise several interview formats.

## Curriculum Coverage Audit

| Curriculum requirement | Evidence |
|---|---|
| Default, implicit, explicit and constructor binding | teaching questions 1–4; Q02–Q04, Q09, Q15, Q30; EX01–EX02, EX14 |
| Lost method context and lexical arrow `this` | teaching questions 1–3, 14; Q02–Q03, Q15; EX01–EX02, EX07, EX14 |
| `call`, `apply`, `bind` | teaching question 4; Q02, Q04, Q09; EX01–EX02 |
| Step-by-step `new` model | teaching questions 5–8; Q04–Q05, Q09, Q23; EX01–EX03, EX09 |
| Literals, factories, constructor functions and `Object.create` | teaching questions 5, 17, 27; Q01, Q10, Q24, Q30; EX01, EX03, EX08–EX09, EX13–EX14 |
| Prototype chain, lookup and shadowing | teaching questions 8–12; Q05, Q11–Q13, Q23; EX01, EX03–EX04, EX08–EX09, EX14 |
| `__proto__` as a legacy accessor | teaching question 12 and legacy guidance; Q13; EX01, EX03, EX14 |
| Classes, inheritance, `super`, static and private fields | teaching questions 13–17; Q07, Q14–Q16, Q24; EX01, EX07–EX09, EX13–EX14 |
| Own/inherited and enumerable/non-enumerable properties | teaching questions 18–19; Q06, Q12, Q17, Q22; EX01, EX05, EX13–EX14 |
| Descriptors, getters and setters | teaching questions 20–21; Q11, Q18–Q19, Q21, Q25; EX01, EX04, EX06, EX11, EX13–EX14 |
| `freeze`, `seal`, `preventExtensions` | teaching questions 22–23; Q08, Q20, Q25; EX01, EX10, EX13–EX14 |
| Proxy/Reflect survey depth | teaching questions 24–27; Q16, Q26–Q30; EX01, EX11–EX14 |

Result: **12/12 curriculum bullets covered**.

## Inventory Evidence Crosswalk

| Inventory ID | Handbook | Question Bank | Practice |
|---|---|---|---|
| `JS-23` | object creation strategies, `new`, placement and production choice | Q01, Q03–Q04, Q09–Q10, Q24, Q30 | EX01–EX03, EX08–EX09, EX13–EX14 |
| `JS-24` | `.prototype`, `[[Prototype]]`, lookup, writes, checks, `instanceof`, `__proto__`, `null` prototype | Q02–Q05, Q09, Q11–Q13, Q19, Q23, Q30 | EX01–EX04, EX08–EX09, EX13–EX14 |
| `JS-25` | classes, fields/methods, `extends`, `super`, static/private elements and composition | Q03, Q07, Q10, Q14–Q16, Q24 | EX01, EX07–EX08, EX13–EX14 |
| `JS-26` | ownership, enumerability, string/Symbol keys and enumeration APIs | Q06, Q12, Q17, Q22, Q25, Q30 | EX01, EX05, EX13–EX14 |
| `JS-27` | data/accessor descriptors, defaults, getter/setter receiver and API choice | Q11, Q17–Q19, Q21, Q25–Q27, Q30 | EX01, EX04, EX06, EX11, EX13–EX14 |
| `JS-28` | integrity levels, strict failures and shallow guarantees | Q08, Q20, Q25, Q30 | EX01, EX10, EX13–EX14 |
| `JS-39` | Proxy/Reflect, receiver, invariants, identity, revocation and API choice | Q16, Q26–Q30 | EX01, EX11–EX14 |

Result: **7/7 mapped inventory groups have explicit handbook, Question Bank and practice evidence**.

## Active-Recall Separation

- 30 question IDs have 30 matching answer IDs.
- 14 exercise IDs have 14 matching solution IDs.
- Questions and answers are in separate trees.
- Exercise conditions and solutions are in separate trees.
- The handbook links to prompts and Question Bank rather than revealing solutions inline.

## Local Verification

- 121 JavaScript fences across the 1.4 chapter/question/practice set passed syntax checking.
- Intentionally invalid calls are explicitly labeled and commented so their containing fences remain valid.
- 107 targeted runtime assertions passed for invocation forms, arrows, repeated binding, bound construction, `new` returns, prototype topology, lookup and writes, class fields and inheritance, private brands, enumeration, descriptors, integrity levels, Proxy receiver/invariants/identity and revocation.
- Question/answer ID parity: 30/30.
- Exercise/solution ID parity: 14/14.
- Repository-relative Markdown links and anchors: 1,093 checked, 0 broken.
- Complete Russian editorial audit: handbook, Question Bank, answers, prompts, solutions and summary checked; English remains for first-use canonical terms, exact APIs, code and standardized metadata.
- PDF/SVG: English-only A4 portrait; PDF is exactly one page; rendered output has a white background, printer-safe margins, diagrams, arrows, comparison tables, pale grayscale-safe accents and no visible clipping or overlap.
- The infographic was rendered and compared side by side with approved 1.1–1.3 pages; title hierarchy, bordered panel grid, spacing, typography, palette and footer treatment remain part of the same series.
- Approved 1.1–1.3 learning artifacts remain unchanged except shared navigation and status metadata.
- Section 1.5 and all later learning placeholders remain unchanged.
- Canonical curriculum, inventory and coverage-map changes: 0.
- `git diff --check`: passed.

## Review Prompts

Please evaluate:

1. Does the chapter rebuild the object model from invocation through Proxy without feeling like a reference catalogue?
2. Is the bridge from approved 1.3 brief enough while still restoring the required `this` and `bind` rules?
3. Are `.prototype`, `[[Prototype]]`, receiver and descriptor operations distinguished clearly?
4. Are classes explained as part of the prototype model without hiding their distinct semantics?
5. Is the balance between inheritance and composition practical rather than ideological?
6. Are enumeration, descriptor and integrity matrices memorable enough for interview recall?
7. Is Proxy/Reflect deep enough for Senior interviews without becoming a metaprogramming chapter?
8. Do the questions and exercises test explanation, prediction, implementation, debugging and review rather than trivia?
9. Does the Russian read naturally throughout all six learning artifacts?
10. Does the infographic work as a one-page visual recall sheet when printed?

## User Acceptance

Pending. Local completeness does not mark the progress checkbox or pass the review gate. After review, approval or requested corrections should be recorded here before section 1.5 is authorized.
