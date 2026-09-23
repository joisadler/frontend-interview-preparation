# Content Conventions

## Language and terminology

Use clear Russian explanations while retaining canonical English technical terms. Avoid beginner-course tone and unexplained specification trivia.

## Chapter contract

Where relevant, a completed chapter contains:

1. Mental Model
2. Core Concepts
3. Detailed Explanation
4. Examples
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

