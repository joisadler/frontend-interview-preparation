# Stage 4 Section Review — 1.6 Collections, Symbols & Iteration

> Status: `ready for user review — not approved`
>
> Authored and locally verified: `2026-11-04`
>
> User approval: pending. Gate: open.

## Authorized Scope

This cycle covers 1.6 only. Canonical placement is `JS-35–JS-38 → 1.6`. Arrays, transformations and copying stay in 1.5. The chapter uses JSON only at the collection boundary. Full serialization remains in 1.7, general memory management in 1.8, and Promise coordination and streaming internals in their later sections. The 1.6 checkbox is unchecked.

## Artifacts

- [Handbook chapter](../../handbook/01-javascript-and-async-programming/06-collections-symbols-and-iteration.md)
- [Question Bank](../../question-bank/by-domain/01-javascript-and-async-programming.md#16-collections-symbols--iteration) and [model answers](../../question-bank/answers/by-domain/01-javascript-and-async-programming.md#16-collections-symbols--iteration)
- [Exercise prompts](../../exercises/prompts/by-domain/01-javascript-and-async-programming.md#16-collections-symbols--iteration) and [solutions](../../exercises/solutions/by-domain/01-javascript-and-async-programming.md#16-collections-symbols--iteration)
- [Compact summary](../../summaries/01-javascript-and-async-programming.md#16-collections-symbols--iteration)
- [A4 infographic PDF](../../infographics/01-javascript-and-async-programming/06-collections-symbols-and-iteration.pdf) and [editable SVG](../../infographics/01-javascript-and-async-programming/06-collections-symbols-and-iteration.svg)

## Size and Mix

| Artifact | Count |
|---|---:|
| Connected teaching questions | 22 |
| 30–60 second interview explanations | 4 |
| Question/answer pairs | 24 |
| Junior / Mid / Senior | 7 / 11 / 6 |
| Exercise/solution pairs | 10 |

Questions include comparison, conceptual explanation, output prediction, debugging, review, implementation, performance and design. Practice moves from recall through prediction, explanation, debugging and code review to implementation and an integrated challenge.

## Curriculum Coverage Audit

| Canonical requirement | Chapter | Question Bank | Practice |
|---|---|---|---|
| `Map` and object keys, iteration, size, serialization | 1–5 | Q01–Q03, Q06, Q08–Q09, Q19 | EX01–EX02, EX05, EX10 |
| `Set` and deduplication | 6–7 | Q04, Q10, Q20, Q24 | EX01–EX02, EX05, EX10 |
| `WeakMap`, `WeakSet`, `WeakRef`, weak reachability | 8–11 | Q11–Q12, Q21, Q24 | EX01, EX03, EX06, EX10 |
| Symbols and well-known symbols | 12–13 | Q05, Q13–Q14, Q24 | EX01, EX03–EX04, EX10 |
| Iterable and iterator protocols | 14–15, 19 | Q06–Q07, Q14, Q16, Q22 | EX01, EX04, EX07–EX08 |
| Custom iterables and generators | 16–20 | Q15–Q17, Q22–Q23 | EX04, EX07–EX08 |
| Async iterables as a bridge to streaming | 21–22 | Q18, Q24 | EX09–EX10 |

| Inventory group | Evidence |
|---|---|
| `JS-35` | Chapter 1–5, Q01–Q03/Q08–Q09, EX02/EX05 |
| `JS-36` | Chapter 6–11, Q04/Q10–Q12/Q20–Q21, EX03/EX06 |
| `JS-37` | Chapter 12–13, Q05/Q13–Q14, EX04 |
| `JS-38` | Chapter 14–22, Q15–Q18/Q22–Q24, EX07–EX10 |

## Research and compatibility

Semantics were checked against [published ECMAScript 2026](https://262.ecma-international.org/17.0/index.html), the [TC39 living draft](https://tc39.es/ecma262/) and [finished proposals](https://github.com/tc39/proposals/blob/main/finished-proposals.md). Browser support comes from MDN Baseline entries for [Set intersection](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set/intersection), [Map grouping](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map/groupBy), [iterator helpers](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Iterator/map), [map insertion](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map/getOrInsert) and [iterator sequencing](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Iterator/concat). These are documentation checks, with runtime probes on the exact Node.js builds listed below.

[GreatFrontEnd](https://www.greatfrontend.com/questions/quiz/javascript-interview-questions) calibrated the collection trade-offs and iteration discussion. [Sudheer Jonna's question bank](https://github.com/sudheerj/javascript-interview-questions) provided weak collection comparison prompts. [Lydia Hallie's question bank](https://github.com/lydiahallie/javascript-questions) provided generator output-prediction formats. Their prompt styles guided original exercises. Edition, browser support and semantics were taken from the primary sources.

The [sync iterator close fix](https://github.com/tc39/ecma262/pull/2600) matters for a rejected yielded promise. The probe observed no cleanup in Node.js 20.18.2 and 22.13.1, and cleanup in 24.21.0 and 26.4.0. The chapter documents this distinction. No checks depend on when a weak target is collected.

## Verification

See [verification log](../../docs/VERIFICATION.md#stage-4-local-audit--section-16--2026-11-04) for measured results. All six Russian learning artifacts received an editorial pass. The chapter hierarchy and prompt/solution separation follow 1.1–1.5. The draft was compared with approved 1.5 chapter and summary structure and with a fresh render of the approved 1.5 infographic for page geometry, panel spacing, typography and palette.

The original checkout was clean on `main` at `2d9cb43`. GitHub confirmed that `main` still pointed at that base when checked. The original checkout is read-only in this session and shell Git HTTPS failed to resolve GitHub. GitHub read access confirmed the base, but write access returned HTTP 403. Authoring and verification therefore ran in an isolated copy.
