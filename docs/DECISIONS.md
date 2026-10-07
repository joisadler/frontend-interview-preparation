# Decision Log

Record only user-approved or consequential project decisions. Do not rewrite old entries; append a new dated entry when a decision changes.

## 2026-09-23 — Repository principles

- Keep the repository text-first and infrastructure-light.
- Preserve the complete Stage 0 inventory and Stage 1 curriculum as canonical artifacts.
- Use one chapter placeholder per numbered curriculum section.
- Keep exercise prompts and solutions separate.
- Use simple Markdown progress tracking.
- Continue future content work one reviewed major section at a time.

## 2026-09-23 — Stage 3 calibration boundary

- The sole Stage 3 calibration topic is `1.1. Execution Model, Declarations & Scope`.
- Keep the existing domain-level handbook, question, answer, prompt and solution structure; do not create a parallel per-topic system.
- Store question answers and exercise solutions separately from active-recall prompts.
- Treat `JS-01`, `JS-02`, `JS-03`, `JS-04` and `JS-22` as the primary coverage groups. Use `JS-12`, `JS-15`, `BR-05` and module topics only as limited cross-references.
- Leave the 1.1 progress checkbox unchecked until the user completes the calibration review.

## 2026-09-24 — Calibration format and language correction

- Treat the first 1.1 draft as rejected for pedagogy, despite complete technical coverage: it felt fragmented, began with specification vocabulary and used too much English.
- Use a connected Russian Q&A narrative that rebuilds fundamentals before precise internals.
- Introduce canonical English terms beside the Russian term on first use, then continue primarily in Russian.
- Apply the language choice to the handbook, Question Bank, model answers, exercise prompts and solutions.
- Preserve answer/solution separation for active recall and keep section 1.1 in review until the user evaluates the revised version.

## 2026-09-27 — Interview-first depth and summary layer

- Treat the second calibration feedback as a request to simplify presentation, not to reduce realistic topic coverage.
- Give each full chapter a clearly marked `🎯 Interview core`; move exact specification terminology and rare edge cases into skippable `🔬 Optional precision` or `🧓 Legacy` layers.
- Prefer plain spoken Russian and short sentences. Use accurate real-life analogies where they reduce cognitive load, while stating that an analogy is not the language implementation.
- Add `summaries/` beside `handbook/`: one compact file per domain, with numbered subsections inside each file.
- Summaries are pre-interview memory aids, not parallel teaching material. Fill only already-authorized sections; keep future sections as explicit navigation placeholders.
- Preserve canonical English terminology in summaries and prefer arrows, symbols, small tables and short bullets over prose or code blocks.

## 2026-09-28 — Restore separate artifacts and simplify without losing depth

- Reject and fully revert the experiment that merged handbook theory, active-recall questions and model answers into one file; it made the treatment feel shorter but too superficial.
- Keep handbook theory, Question Bank prompts, model answers, exercise prompts and exercise solutions as separate artifacts.
- Preserve the detailed 1.1 coverage from the pre-consolidation version. Simplify wording and sentence structure instead of deleting technical content.
- Use different focused analogies for different mechanisms. Do not reuse one broad metaphor when its parts do not map coherently to the concepts.
- Keep exact specification terminology available in skippable precision blocks after the practical explanation.
- Do not change the existing summary during this revision; review and redesign that artifact separately.

## 2026-09-28 — Add a print-first infographic layer

- Add `infographics/` beside `handbook/` and `summaries/` for one-page visual refreshers.
- Mirror the `handbook/<domain>/<section>` naming structure, but create files only for sections that already have authorized content; do not generate empty infographic placeholders.
- Keep the printable infographic itself in English so canonical interview terminology remains compact.
- Store a print-ready A4 PDF and an editable vector SVG for each finished infographic.
- Use a white background, sparse pale accents and a layout that remains readable in grayscale to minimize printer ink.
- Keep the accepted linear infographic for section 1.1; do not adopt the rejected mind-map experiment.

## 2026-10-01 — Approve the Stage 3 calibration baseline

- Accept the complete section 1.1 learning set: handbook, separate questions and answers, separate exercises and solutions, compact summary and linear print infographic.
- Use the final handbook style as the baseline for future sections: detailed and connected, but conversational rather than dry or academic.
- Continue rebuilding fundamentals explicitly; professional experience must not be used as a reason to skip basic concepts needed for active recall.
- Keep varied, coherent real-life analogies where they improve memory. The theater-props analogy is a positive reference example.
- Keep the current summary and English A4 infographic formats.
- Mark section 1.1 and Stage 3 complete.
- Do not start section 1.2 or Stage 4 until the user gives explicit authorization.

## 2026-10-07 — Treat approved artifacts as one project-wide system

- Treat the repository as one connected handbook, not a collection of independently styled articles.
- Use approved sections as the required reference for chapter hierarchy, heading grammar, explanatory rhythm, metadata, summary density and infographic visual language across every domain.
- Preserve the teaching-heading pattern `### 🎯 1. ...` / `### 🔬 1. ...`. Do not invent local labels such as `Interview core — 1`.
- Adapt length and grouping to the topic's real scope without changing the recognizable structure or voice.
- Require a side-by-side consistency check against approved chapter, summary and infographic artifacts before a new section is marked review-ready.
- Require a complete language pass across every Russian learning artifact. Russian sentence structure is primary; canonical English terms appear at first introduction or where an exact API name is required, not as untranslated sentence scaffolding.
- Treat a new structural or visual language as an explicit project decision, not a per-section authoring choice.
