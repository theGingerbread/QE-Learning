# Agent Team Symmetry / K-Path Report

## Scope

This PR is the Batch B topic-pack for Issue #4. It refines only the reciprocal-space, crystal-symmetry and k-point / k-path theory pages:

- `theory-minimum/reciprocal-space-and-brillouin-zone.md`
- `theory-minimum/crystal-symmetry-space-group-point-group.md`
- `theory-minimum/kpoints-symmetry-kpath.md`

Preflight found `main` and `origin/main` at the same commit when this branch was created. Before final QA, PR #5 for band-structure / band-gap interpretation was merged into `main`, and this branch was updated from `origin/main` without conflicts. This PR still does not edit the two PR #5 target pages.

## Subagents Used

| Subagent | Role | Target pages | Output |
|---|---|---|---|
| R-B1 Reciprocal-space Research | Research | `reciprocal-space-and-brillouin-zone.md`, `kpoints-symmetry-kpath.md` | Brief on lattice / reciprocal lattice / Bloch theorem / BZ integration / mesh vs path |
| R-B2 Crystal-symmetry Research | Research | `crystal-symmetry-space-group-point-group.md`, `kpoints-symmetry-kpath.md` | Brief on space group / point group / little group / irreducible k-points / degeneracy |
| W-B1 Reciprocal-space Writer | Writer | `reciprocal-space-and-brillouin-zone.md` | Added mesh/path evidence and PASS / WARN / BLOCK table |
| W-B2 Symmetry Writer | Writer | `crystal-symmetry-space-group-point-group.md` | Clarified space group / point group / little group and label-validity evidence |
| W-B3 K-path Integration Writer | Writer | `kpoints-symmetry-kpath.md` | Integrated links and separated NSCF mesh from bands path |
| Q-B1 Physics QA | QA | all three pages | Found one required wording fix around structural space group vs calculation symmetry branch |
| Q-B2 Style QA | QA | all three pages | Found heading and PASS strictness consistency improvements |
| Q-B3 Source / Link QA | QA | all three pages | Found no source-boundary blockers |

## Research Summary

The team converged on two technical boundaries:

- Uniform k meshes are Brillouin-zone integration objects; high-symmetry paths are dispersion-visualization objects.
- Symmetry labels, irreducible k-points and degeneracy statements are conditional on the current cell, standardized convention, active symmetry branch and data chain.

The research briefs recommended making `full mesh + shift + irreducible count` the minimum k-point evidence, and treating `bands.x lsym` / `filband.rap` as classification evidence rather than proof of topology, experiment-facing assignment or path validity.

## Writing Changes

- Strengthened the reciprocal-space page with the relation between real-space cell changes and reciprocal spacing, and with explicit output evidence for full mesh, shift, weights and irreducible k-points.
- Added a `PASS / WARN / BLOCK` table to the reciprocal-space page.
- Clarified the space group / point group / little group distinction in the symmetry page.
- Added a label-validity checklist: current cell, standardized convention, path source, symmetry branch and post-relax review.
- Clarified that `filband.rap` and `bands.x lsym` support small-group classification only.
- Updated the kpoints page to separate `calculation='nscf'` dense uniform mesh from `calculation='bands'` path calculations.
- Tightened WARN / BLOCK conditions for old paths after relax / vc-relax, SOC, magnetism, noncollinear settings or symmetry changes.

## Physics QA Findings

Physics QA found one required fix: the first writer version implied that structural space group depends on magnetic / SOC model. This was corrected to distinguish structural crystallographic symmetry from the QE-usable symmetry branch of the active Hamiltonian.

Physics QA accepted the treatment of:

- high-symmetry path as non-integration evidence;
- irreducible k-points as symmetry-reduced representatives, not the original full mesh;
- little group as specific to a `k` / `q` point;
- SOC / magnetism / relax as triggers for renewed symmetry and path review.

## Style QA Findings

Style QA found no blockers. Two consistency suggestions were applied:

- the reciprocal-space page now uses an explicit `PASS / WARN / BLOCK` heading;
- the kpoints page `PASS` row now includes current cell convention and post-relax / SOC / magnetism review evidence.

## Source QA Findings

Source QA found no source-boundary blocker. The pages still rely on:

- QE `INPUT_PW`, `INPUT_BANDS` and related official documentation for field and program behavior;
- Monkhorst-Pack for the integration-mesh concept;
- SeeK-path only as a path-provenance helper, not as a substitute for structure / symmetry review.

No new DOI, BibTeX, private path, tutorial-as-authority or material-specific source was added.

## Validation Results

Validation commands were run after integration:

- `git diff --check`
- full Markdown local-link check
- private-path and document-residue scan
- project-scope drift scan
- fixed material case and universal-parameter scan
- high-risk overclaim scan for path / mesh / symmetry / degeneracy wording
- PASS / WARN / BLOCK preservation check

## Remaining Gaps

- This PR does not add a full group-theory derivation; the pages remain theory-minimum references for QE input/output review.
- External QE and SeeK-path pages were not live-revalidated in this PR; the existing source spine remains the authority for source maintenance.
- PR #5 has already merged the band-structure and band-gap pages, so this branch intentionally remains scoped to reciprocal-space, symmetry and k-path pages.

## Merge Recommendation

Ready for draft PR review after final command validation. The diff is scoped to three theory-minimum pages plus this report.

## Final QA Gate

| Gate | Result | Evidence |
|---|---|---|
| Physics accuracy | PASS | The pages distinguish full mesh, shift flags, irreducible representatives and weights; separate space group, point group and little group; and keep little-group labels tied to the current k/q point and Hamiltonian branch. |
| Style consistency | PASS | The three pages use positive definitions, physical-picture prose and compact review tables without turning into a broad group-theory derivation. |
| Source boundary | PASS | Source use remains within QE official INPUT/program docs, Monkhorst-Pack for integration meshes and SeeK-path only as a path-provenance helper. No new DOI or BibTeX metadata was added. |
| Output-review framing | PASS | The pages specify output evidence for full mesh, shift, weights, irreducible k-points, symmetry summaries, bands path sequence and `filband.rap` classification. |
| PASS/WARN/BLOCK preservation | PASS | All three target pages contain explicit PASS/WARN/BLOCK or equivalent judgement gates. |
| Local links | PASS | Full local Markdown link check passed after updating from `origin/main`. |
| Private path / document residue | PASS | Target-file scan found no private machine paths or external document residues. |
| Project-scope drift | PASS | Target-file scan found no unrelated tooling drift; content stays within QE-Learning theory-minimum scope. |
| Fixed material case scan | PASS | No material-specific case examples were introduced. |
| Universal parameter scan | PASS | No fixed k-mesh, shift, cutoff, smearing or other universal parameter recipe was introduced. |
| High-risk overclaim scan | PASS | Path-as-DOS/BZ-integration, irreducible-points-as-full-mesh, and `filband.rap`-as-proof overclaims are explicitly blocked or framed as misconceptions. |
| Merge recommendation | READY | No BLOCK gate remains; PR #6 is suitable to mark ready and merge after final GitHub mergeability check. |
