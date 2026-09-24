# Content Conventions

## Language and terminology

Use clear Russian as the main language of explanations. Introduce a canonical English technical term in parentheses at its first meaningful use inside a chapter—for example, «область видимости (scope)»—then continue primarily with the stable Russian term. Keep API names, code, specification fields and algorithm names unchanged.

Assume professional experience, but do not assume active recall of fundamentals. Rebuild the basic model before using specification terminology. Avoid both a beginner-course tone and unexplained specification trivia.

## Explanatory flow

For conceptual handbook chapters, prefer a connected question-led narrative:

1. begin with the basic question a candidate must answer;
2. give a short direct answer;
3. expand it with one small example and causal reasoning;
4. add an explicitly labeled precision or legacy note only when useful;
5. bridge to the next prerequisite question.

Order material from familiar concepts to precise internals. Do not open a chapter with a glossary or specification model whose terms depend on concepts not yet explained. A Q&A chapter may show teaching answers inline; active-recall question prompts and exercise solutions must remain separate.

Give each concept one canonical explanation. Use Common Mistakes, Interview Traps and summaries for recall, not to teach the same material again at full length.

## Chapter contract

Where relevant, a completed chapter contains:

1. Mental Model
2. Connected Core Explanation, often in Q&A form
3. Examples integrated where each concept is introduced
4. Compact terminology/reference summary
5. Common Mistakes
6. Interview Traps
7. Common Interview Questions
8. How to Explain It in an Interview
9. Exercises
10. Interview Challenge
11. Checklist
12. Related Inventory IDs
13. Sources / Last Verified

## Depth labels

- `Core` — explain, implement and debug confidently.
- `Professional` — production scenarios and trade-offs.
- `Advanced` — architecture, diagnostics and Senior judgment.
- `Survey` — explain purpose and trade-offs without disproportionate internals.
- `Legacy` — interview/maintenance knowledge, not the current default.
- `Experimental` — clearly identify non-stable APIs.

## Stable identifiers

Preserve inventory IDs. Questions, exercises and chapters should have stable IDs and reference the inventory items they cover. New inventory groups receive new IDs; existing IDs are not renumbered for aesthetics.

## Question metadata

Every future question should record:

- stable ID;
- domain and topic;
- Junior/Mid/Senior level;
- question type;
- priority/frequency;
- related inventory IDs;
- modern/legacy status;
- answer location;
- verification/source status.

## Exercise separation

Prompts live under `exercises/prompts/`; solutions live under `exercises/solutions/`. Do not place a direct solution beneath a task intended for active recall.

## Completion semantics

A section is complete only when its authorized content, questions, practice, verification and review obligations are satisfied. A placeholder or prose-only draft is not complete.
