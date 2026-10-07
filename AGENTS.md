# Repository Instructions

This repository is the source of truth for the Frontend Interview Preparation project.

## Required reading order

Before making changes, read:

1. `docs/PROJECT_CONTEXT.md`
2. `ROADMAP.md`
3. `CURRICULUM.md`
4. `research/MASTER_QUESTION_INVENTORY.md`
5. `coverage/INVENTORY_TO_CURRICULUM.md`
6. `PROGRESS.md`
7. `docs/SESSION_HANDOFF.md`
8. the README and placeholders for the authorized domain.

## Stage gates

- Determine the active roadmap stage before editing.
- Perform only the stage or major section explicitly authorized by the user.
- Never advance through a review gate automatically.
- Stage 3 creates exactly one complete calibration section and then stops.
- Stage 4 proceeds one major section → review → next section.
- Do not generate the entire handbook in one batch.

## Content rules

- Treat approved sections as one project-wide editorial and visual system. Before authoring a new section, compare its chapter hierarchy, heading grammar, narrative rhythm, metadata, summary density and infographic design with the approved references. Adapt the amount of material to the topic, but do not invent a new structure or visual language without an explicit project decision.
- In Russian learning material, make the Russian sentence primary. Introduce a useful canonical English term once, then use Russian wording except for API names, code and terms that would become less precise in translation. Do not assemble Russian prose from untranslated English nouns and adjectives.
- Preserve all stable inventory IDs such as `JS-01`, `RE-01` and `SD-01`.
- Do not silently remove, merge or renumber inventory or curriculum items.
- If scope changes, update the curriculum, coverage map, progress, decision log and handoff together.
- Distinguish current production recommendations from legacy/interoperability interview knowledge.
- Mark experimental/canary and survey-depth material explicitly.
- Revalidate unstable ecosystem claims with current primary documentation before authoring them.
- Keep solutions separate from prompts; do not expose an answer directly below an active-recall exercise.
- A placeholder is never `complete`.
- Verify executable examples and record the verification status.

## Scope and infrastructure

Prefer Markdown and small executable exercises. Do not introduce a web app, dashboard, backend, database, agent infrastructure, elaborate automation or separate progress-tracking system without explicit approval.

Do not overwrite unrelated user changes. End each authorized major section with its audit and stop for review.

## End-of-session handoff

Update, where applicable:

- `PROGRESS.md`;
- affected coverage mappings;
- `ROADMAP.md` stage/domain status;
- `CHANGELOG.md`;
- `docs/DECISIONS.md`;
- `docs/SESSION_HANDOFF.md`;
- verification and unresolved questions.
