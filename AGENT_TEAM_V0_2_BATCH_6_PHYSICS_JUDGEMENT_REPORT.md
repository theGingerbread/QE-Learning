# Agent Team v0.2 Batch 6 Physics-Judgement Report

## Scope

Batch 6 completes the physics-judgement final pass for v0.2. The directory already contained the full numbered topic spine and quick judgement cards, so this batch focuses on final integration rather than broad rewriting:

- clarify the routing between numbered canonical topic pages and quick output-driven judgement cards;
- clean high-risk wording so boundary warnings are less likely to be misread as positive claims;
- verify `PASS / WARN / BLOCK`, source boundary, and overclaim controls across `physics-judgement/`;
- preserve the existing numbered-page / quick-card architecture.

## Subagents used

| Subagent | Role | Target pages | Output |
|---|---|---|---|
| Structure QA auditor | Page-structure review | `physics-judgement/*.md` | Checked numbered pages vs quick-card routing and section coverage |
| High-risk physics QA auditor | Overclaim scan | `physics-judgement/*.md` | Checked gap, KS eigenvalue, U, SOC, vdW, phonon, Born charge, Wannier, EPC, free-energy overclaims |
| Source/link QA auditor | Source-boundary review | `physics-judgement/*.md`, `references/` | Checked source-boundary presence and internal routing |
| Main agent | Integration and final QA | README, quick cards, report | Applied minimal wording/routing fixes and validation gate |

## Research summary

The physics-judgement directory has two deliberate layers:

- numbered topic pages provide canonical explanatory context and the longer physics-judgement spine;
- quick judgement cards provide output-driven review routes with `PASS / WARN / BLOCK`, required QE input/output evidence, and workflow back-links.

The final pass keeps this two-layer structure and avoids merging pages or duplicating long正文 between them.

## Writing changes

- Added a routing table to [physics-judgement/README.md](physics-judgement/README.md) that states when to use numbered canonical pages, quick judgement cards, standards pages, and calculation-record routes.
- Added short route notes to overlapping quick cards so readers know which numbered canonical topic page carries the system explanation.
- Added positive problem statements to older quick cards that previously opened directly with core judgement bullets.
- Rephrased high-risk boundary examples so forbidden claims remain clearly marked as overclaims rather than looking like positive assertions in mechanical scans.
- Added targeted canonical-literature / stronger-card source routes for SOC, surfaces/electrostatics, Wannier and excited-state pages.
- Kept `CONCLUSION_REFERENCE_BOOK.md` as the conclusion kernel and did not expand it into duplicate正文.

## Physics QA findings

- `DFT gap`, `KS eigenvalue`, `U`, `SOC`, `vdW`, `Born charge`, `ASR`, `Wannier`, `EPC`, `excited-state`, and `free-energy` boundaries are already represented in either numbered topic pages or quick judgement cards.
- Structure QA identified duplicate-route risk between numbered canonical pages and quick cards. Minimal route notes were added to the overlapping quick cards, and older quick cards gained a positive `本页解决什么问题` entry where needed.
- Source QA requested stronger source routing for broad SOC/magnetism and Wannier/excited-state pages; links to canonical literature and stronger quick-card routes were added.
- The main residual risk was wording that correctly appeared in “do not overclaim” sections but triggered broad high-risk scans. Those phrases were reworded to keep the boundary while reducing ambiguity.
- No page was changed to recommend a universal method, fixed parameter, concrete material example, or unsupported source.

## Style QA findings

- The directory now explicitly explains its two-page-type architecture.
- `PASS / WARN / BLOCK` remains a judgement gate, not a replacement for the longer physics explanation.
- The final pass avoided making every page mechanically identical; pages with equivalent headings were accepted when they served the same review function.

## Source QA findings

- No new bibliography metadata, DOI, BibTeX entry, or tutorial dependency was added.
- Existing judgement pages continue to route to `references/source-index.md`, `references/canonical-literature.md`, QE official docs, workflow pages, and standards pages.
- Source-level refinements that require bibliography metadata are reserved for Batch 7.

## Validation results

- `git status --short --branch`: branch `docs/v0.2-physics-judgement-final`; only Batch 6 target files are changed.
- `git diff --check`: passed.
- Markdown local links: passed.
- `physics-judgement/` `PASS / WARN / BLOCK` scan: passed for topic and quick-card pages.
- Source-boundary scan: passed for topic and quick-card pages.
- Private path / document residue scan: passed on touched Batch 6 files.
- Scope drift, fixed material, universal parameter and high-risk overclaim scans: passed on touched Batch 6 files after wording cleanup.

## Remaining gaps

- Batch 7 will consolidate standards/source policy and can decide whether any source cards need smaller wording updates.
- Batch 8 will add judgement diagrams if they materially improve review flow.
- Batch 9 will refresh navigation and release notes after all content batches are merged.

## Final QA Gate

| Gate | Result | Evidence |
|---|---|---|
| Physics accuracy | PASS | Boundary warnings for gap, U, SOC, vdW, Born charge, Wannier, EPC and free energy remain explicit and conservative. |
| QE workflow correctness | PASS | README routing points judgement pages back to workflow and standards review instead of replacing workflow execution. |
| Output-review framing | PASS | Quick cards retain output symptoms, required evidence and downstream gates. |
| PASS/WARN/BLOCK preservation | PASS | All non-index physics-judgement pages retain P/W/B or equivalent gate framing. |
| Style consistency | PASS | Numbered pages and quick cards now have explicit roles; no broad mechanical rewrite was needed. |
| Source boundary | PASS | No unsourced new claims or fabricated metadata added. |
| Diagram validity, if applicable | NA | No new diagrams in this batch. |
| Local links | PASS | Markdown local-link check passed. |
| Private path / document residue | PASS | Touched-file scan found no private paths or research-document residue. |
| Project-scope drift | PASS | No platform, runtime, automation, or concrete-case content added. |
| Fixed material case scan | PASS | No concrete material examples added. |
| Universal parameter scan | PASS | No universal cutoff, k mesh, smearing, U, vdW, SOC or functional recommendation added. |
| High-risk overclaim scan | PASS | Mechanical overclaim triggers in touched files were rephrased as explicit boundary language. |
| Merge recommendation | READY | Final validation commands passed. |
