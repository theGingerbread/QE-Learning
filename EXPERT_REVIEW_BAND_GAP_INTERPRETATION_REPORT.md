# Expert Review: Band Structure and Band Gap Interpretation

## Scope

This review addresses the first Issue #4 expert-review slice. The scope was limited to:

- `theory-minimum/band-structure-and-dos.md`
- `physics-judgement/04-band-gap-problem-and-derivative-discontinuity.md`

No directory structure, workflow pages, broad theory sections, material examples, or universal parameter recommendations were added.

## Files changed

- `theory-minimum/band-structure-and-dos.md`
- `physics-judgement/04-band-gap-problem-and-derivative-discontinuity.md`
- `EXPERT_REVIEW_BAND_GAP_INTERPRETATION_REPORT.md`

## Physics accuracy fixes

- Clarified that ordinary QE bands/DOS support a DFT-level or Kohn-Sham-level electronic-structure statement, not an unqualified quasiparticle, optical or experimental gap.
- Added a compact distinction among Kohn-Sham gap, fundamental gap, quasiparticle addition/removal energy and optical gap.
- Tightened derivative-discontinuity wording by linking the missing exchange-correlation discontinuity and delocalization/self-interaction boundary to model error rather than k-mesh error.
- Clarified that semilocal gap limitations are common model boundaries, not a universal rule for every spin/SOC/functional setting.
- Added explicit checks for path-only VBM/CBM searches, uniform-mesh DOS evidence, `nbnd` coverage, smearing and energy-zero consistency.

## Readability fixes

- Added a short energy-reference explanation covering Fermi level, VBM, CBM and energy zero at first use in the theory page.
- Reduced ambiguity around “gap” by naming the evidence level: KS-level bands, DFT-level gap, total DOS, projected DOS, quasiparticle gap and optical gap.
- Kept the pages as concise reference entries rather than turning them into a textbook derivation.

## QE mapping fixes

- Strengthened the mapping to `K_POINTS crystal_b/tpiba_b` for bands paths and `K_POINTS automatic` for NSCF/DOS uniform meshes.
- Added `nbnd` as a required review item for target valence/conduction energy-window coverage.
- Added Fermi level, VBM/CBM and energy-zero review as explicit output/plot-script evidence.
- Preserved and strengthened the output-review and `PASS / WARN / BLOCK` framing.

## Source boundary

- No new bibliography spine was introduced.
- Parameter and program behavior remain grounded in existing QE official input references: `INPUT_PW`, `INPUT_BANDS`, `INPUT_DOS` and `INPUT_PROJWFC`.
- Band-gap and derivative-discontinuity boundaries remain grounded in the existing canonical literature spine: Kohn-Sham foundations, Perdew-Parr-Levy-Balduz, Mori-Sanchez-Cohen-Yang, and Onida-Reining-Rubio.
- No DOI, BibTeX or metadata was invented.

## Validation

Validation commands were run before commit:

- `git status --short --branch`
- `git diff --check`
- Markdown local link check
- modified/new-file scan for private paths, Word-reference residues and automation/tool drift terms
- fixed material case scan
- universal-parameter wording scan
- high-risk overclaim scan for KS eigenvalue / DFT gap misuse
- checks that both target pages retain output-review framing and `PASS / WARN / BLOCK`
