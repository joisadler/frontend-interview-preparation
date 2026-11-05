# Working Workflow

## Starting a new session

1. Read [AGENTS.md](../AGENTS.md) and follow its required order: project context → roadmap → curriculum → inventory → coverage → progress → handoff → the authorized domain's README and chapter placeholder.
2. Determine the active stage and the scope already authorized by the user. A planned next section is not authorization to start it. Routine decisions inside the authorized scope do not require another approval.
3. Read the current [content conventions](CONTENT_CONVENTIONS.md), applicable decisions/verification and artifact templates. Compare the calibration baseline and the nearest approved chapter, summary, questions/practice, infographic SVG and rendered PDF.
4. Before section research or authoring, check the main checkout, `main`, `origin` and working tree; fetch `origin` and verify that `HEAD` matches the actual remote `main`. Preserve unrelated changes and identify any unfinished work from this cycle before resuming it.
5. If a command fails on a sandbox boundary, use the available authorized execution mechanism before concluding that the project folder is wrong. Permissions and environment observations from an older session must be checked again. Do not substitute a mirror, temporary clone or patch for work in the main checkout. Temporary test fixtures and renders are allowed outside the repository.

The installed `frontend-handbook-section-cycle` skill supplies the repeatable Stage 4 procedure when available. Repository rules, current files and explicit user authorization remain authoritative; the skill does not authorize another section or a push by itself.

## Authoring cycle for Stages 3–4

Stage 3 is complete. Preserve its single-section calibration boundary as history. For each explicitly authorized Stage 4 section:

1. Resolve every curriculum requirement, primary inventory ID, prerequisite and boundary with neighboring topics. Preserve stable IDs and canonical placements.
2. Revalidate time-sensitive claims using current primary sources and calibrate interview depth/formats against independent interview sources. Record dates and exact environments where behavior depends on them.
3. Write the connected Russian chapter using the current contract and approved references. Integrate examples with the explanation, preserve numbered `🎯`/`🔬` teaching headings and make the two reading routes clear.
4. Create questions with separate model answers and exercise prompts with separate solutions. Add only this section's compact domain-summary subsection, English one-page A4 portrait PDF/editable SVG infographic and review/coverage record.
5. Verify the actual executable examples and their expected behavior in the appropriate environment. Check ID parity, metadata, links, answer separation, Russian wording and structural/visual consistency. Render the final PDF and inspect it beside an approved reference. Record measured results and limitations rather than copying old counts.
6. Record concrete curriculum/inventory → chapter → questions → practice evidence. Update applicable navigation, progress, roadmap, changelog and handoff; append a decision only when the policy or scope actually changes.
7. Leave the authored section `ready for user review — not approved`, its checkbox unchecked and its review gate open. The next action in the handoff is review of this section.
8. If commit/push is authorized, check diff scope, commit only this cycle's files and push without force. Verify the actual remote commit, artifact delivery and clean working tree. A permitted publication can precede content approval; it does not close the review gate.
9. Stop for user review. After explicit acceptance, synchronize approval records and the handoff. Starting the next section still requires separate authorization.

For an audit, wording correction or documentation-only task, follow the user-approved scope and use proportionate checks. Do not run a new authoring cycle or repeat runtime/PDF checks merely to update prose or record acceptance when the underlying examples/artifacts are unchanged.

## Status vocabulary

| State | Meaning |
|---|---|
| `placeholder` | Navigation/scaffold only; no completed learning content. |
| `draft` | Authoring or required checks are still incomplete. |
| `ready for user review — not approved` | The full authorized set is prepared and verified with stated limits; user acceptance is pending and progress remains unchecked. |
| `approved` / `approved by user` / `одобрено` | The user explicitly accepted the artifact set. |
| `complete` | Required artifacts, verification and user review are satisfied; the section may be checked in progress. |
| `needs-refresh` | Material needs a stated update; this label does not erase its approval history. |

Use the existing status/metadata format of the relevant artifact. `reviewed` in an older record does not establish user approval unless acceptance is explicitly recorded. `Core`, `Professional`, `Advanced`, `Survey`, `Legacy` and `Experimental` describe depth or compatibility, not completion.

A file existing on disk, successful tests, a commit or a push do not by themselves mean that a topic is approved or personally mastered. Track authored, verified, committed, pushed and user-approved states separately in the existing records.

