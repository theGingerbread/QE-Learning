# Agent Team v0.2 Batch 5 Theory-Minimum Report

## Scope

Batch 5 completes the theory-minimum handbook slice. The pass focuses on the theory pages as QE input/output review layers rather than textbook chapters. Most theory pages already had sufficient v0.2 depth from earlier PRs, so this batch makes a targeted final upgrade to the older-format exchange-correlation functional page and records a full theory-page structure audit.

## Subagents used

| Subagent | Role | Target pages | Output |
|---|---|---|---|
| Theory structure auditor | Gap audit | all `theory-minimum/*.md` | Identified `functional-choice.md` as the only older-format topic page |
| Functional-choice writer | Page writer | `theory-minimum/functional-choice.md` | Rewrote as a full QE review-layer theory page |
| Main agent | Integration and QA | `theory-minimum/README.md`, report, validation | Final gate and PR integration |

## Research summary

The theory-minimum directory now covers DFT/KS/SCF, plane-wave cutoff, pseudopotentials, reciprocal space, symmetry, k-points, bands/DOS, smearing, force/stress, DFPT phonons, dielectric/Born response, magnetism/SOC/DFT+U, and functional choice. The common role is to explain why specific QE input/output evidence matters for workflow admission and downstream reliability.

## Writing changes

- Reworked [theory-minimum/functional-choice.md](theory-minimum/functional-choice.md) from an older checklist page into the v0.2 theory-minimum structure:
  - positive problem statement;
  - physical picture;
  - minimum theory structure;
  - QE input/output mapping;
  - output-review evidence;
  - workflow downstream impact;
  - common misconceptions;
  - `PASS / WARN / BLOCK` gate;
  - physics-judgement boundary;
  - source boundary.
- Updated [theory-minimum/README.md](theory-minimum/README.md) to state the v0.2 reading contract for theory pages.

## Theory-page QA findings

- Existing pages use equivalent headings such as `最低数学结构`, `对 output review 的影响`, and `PASS / WARN / BLOCK 关联`; these satisfy the v0.2 page definition of done without mechanical heading churn.
- `functional-choice.md` was the only topic page lacking explicit physical picture, QE mapping, output review, workflow impact, and PASS/WARN/BLOCK in the current style.
- The functional-choice page now distinguishes model error from numerical convergence and routes detailed credibility judgement to `physics-judgement/`.

## Source QA findings

No new source metadata, DOI, BibTeX entry, or external tutorial dependency was added. The functional-choice page points parameter definitions to QE official `INPUT_PW` and uses repository source spine / physics-judgement pages for model-boundary context.

## Validation results

- `git status --short --branch`: branch `docs/v0.2-theory-minimum-final`; only Batch 5 target files are changed.
- `git diff --check`: passed.
- Markdown local links: passed, 155 Markdown files checked.
- Theory-minimum core section scan: passed, 13 topic files checked for problem statement, QE object mapping, PASS/WARN/BLOCK, and source boundary.
- Private path / document residue scan: passed on touched Batch 5 files.
- Scope drift, fixed material, universal parameter and high-risk overclaim scans: passed on touched Batch 5 content files.

## Remaining gaps

- Batch 6 will perform the final depth and duplicate-route pass for `physics-judgement/`.
- Batch 7 will finish standards/source policy consistency and record templates.
- Batch 8 will decide whether additional theory diagrams are still necessary beyond the diagrams already added in Batches 2-4.

## Final QA Gate

| Gate | Result | Evidence |
|---|---|---|
| Physics accuracy | PASS | Functional choice is framed as a model choice, not a universal accuracy ladder. |
| QE workflow correctness | PASS | `input_dft`, UPF metadata, `vdw_corr`, hybrid/Hubbard branches, and `prefix/outdir` consistency are mapped to QE workflow evidence. |
| Output-review framing | PASS | The page states what SCF output, PP loading, warnings, and downstream file chains can and cannot prove. |
| PASS/WARN/BLOCK preservation | PASS | The rewritten page includes explicit `PASS / WARN / BLOCK` gate logic. |
| Style consistency | PASS | Page now matches the reference-handbook theory style without turning into a long textbook derivation. |
| Source boundary | PASS | Official field definitions are routed to QE `INPUT_PW`; model-boundary judgements route to physics-judgement pages. |
| Diagram validity, if applicable | NA | No new diagrams in this batch. |
| Local links | PASS | 155 Markdown files checked; no missing local links. |
| Private path / document residue | PASS | No private path or research-document residue found in touched Batch 5 files. |
| Project-scope drift | PASS | No off-scope platform or automation-system content added. |
| Fixed material case scan | PASS | No concrete material examples added. |
| Universal parameter scan | PASS | No universal cutoff, k mesh, smearing, U, or functional recommendation added. |
| High-risk overclaim scan | PASS | No functional, hybrid, vdW, or DFT+U method is written as a universal improvement. |
| Merge recommendation | READY | Final validation commands passed. |
