# Agent Team Polar Response / Electrostatics Report

## Scope

This PR is the Batch D topic-pack for Issue #4. It refines only polar-response and surface-electrostatics boundary pages:

- `theory-minimum/dielectric-born-charge.md`
- `physics-judgement/10-dfpt-response-and-polar-materials.md`
- `physics-judgement/work-function-and-electrostatic-boundary.md`
- `workflows/electronic/work-function.md`

No slab-construction tutorial, fixed vacuum/slab parameter recommendation, concrete material case or broad workflow rewrite was added.

## Subagents Used

| Subagent | Role | Target pages | Output |
|---|---|---|---|
| R-D1 Polar-response Research | Research | `dielectric-born-charge.md`, `10-dfpt-response-and-polar-materials.md` | Brief on dielectric tensor, Born effective charge, LO-TO splitting, non-analytic correction, tensor symmetry and convergence evidence |
| R-D2 Surface-electrostatics Research | Research | `work-function-and-electrostatic-boundary.md`, `workflows/electronic/work-function.md` | Brief on electrostatic potential reference, planar/macroscopic average, vacuum plateau, Fermi level, dipole correction and slab boundary |
| W-D1 Born-charge Theory Writer | Writer | `theory-minimum/dielectric-born-charge.md` | Added insulator-response boundary and tensor / sum-rule review evidence |
| W-D2 Polar-material Judgement Writer | Writer | `physics-judgement/10-dfpt-response-and-polar-materials.md` | Added real-response vs numerical/model/file-chain classification |
| W-D3 Work-function Boundary Writer | Writer | `physics-judgement/work-function-and-electrostatic-boundary.md` | Added potential-zero, plateau, two-side slab and dipole-boundary language |
| W-D4 Work-function Workflow Writer | Writer | `workflows/electronic/work-function.md` | Added fixed output-review order and two-side plateau check |
| Q-D1 Physics QA | QA | all four pages | Checked Born charge, tensor, LO-TO and work-function overclaim risks |
| Q-D2 Style / Source QA | QA | all four pages | Checked handbook style, scope and source boundary |

## Research Summary

The team converged on two evidence chains:

- Polar response requires an insulating-response context, converged DFPT perturbations, tensor symmetry / sum-rule review, and consistent Born/dielectric/IFC/non-analytic files.
- Work function requires a same-chain Fermi reference and vacuum level, stable planar or macroscopic average plateau, clear slab normal and boundary-condition record.

Both areas are high-risk because apparently valid output files can still be physically uninterpretable when the response condition, energy reference or boundary condition is wrong.

## Writing Changes

- Strengthened `dielectric-born-charge.md` by stating that Born effective charge is a dynamic polarization response and by adding tensor constraint / charge-neutrality evidence.
- Expanded `10-dfpt-response-and-polar-materials.md` with a layered cause model: real polar response, numerical error, model error, file-chain error and invalid response condition.
- Refined `work-function-and-electrostatic-boundary.md` to clarify potential zero, planar/macroscopic average, vacuum plateau, slab asymmetry and dipole-boundary handling.
- Updated `workflows/electronic/work-function.md` with a stable output-review order: SCF chain -> `pp.x` source -> potential type / average direction -> plateau -> `E_vac - E_F`.

## Physics QA Findings

No BLOCK-level physics issue remains after integration.

Accepted boundaries:

- Born effective charge is not described as static ionic valence.
- Tensor abnormalities are treated as ambiguous until symmetry, convergence, structure and file chain are reviewed.
- LO-TO / non-analytic correction requires consistent Born/dielectric/IFC data and recorded direction / ASR boundary.
- Work function requires a stable vacuum plateau and same-chain Fermi reference.
- Dipole correction and low-dimensional boundary settings are not presented as universal fixes.

## Style QA Findings

The pages remain concise reference-handbook entries. The workflow page stays procedural and does not become a slab-construction tutorial; the judgement page handles interpretation boundary; the theory page handles response concepts.

## Source QA Findings

No new DOI, BibTeX, tutorial-as-authority or material-specific source was introduced. QE program behavior remains tied to official INPUT and PostProc documentation; DFPT polar-response theory remains tied to the existing canonical literature spine.

## Validation Results

Validation commands were run after integration:

- `git diff --check`
- full Markdown local-link check
- private-path and document-residue scan
- project-scope drift scan
- fixed material case and universal-parameter scan
- high-risk overclaim scan for Born charge, dielectric tensor, LO-TO, work function, vacuum plateau, Fermi reference and dipole correction
- PASS / WARN / BLOCK preservation check

## Remaining Gaps

- This PR does not live-verify external QE documentation links; source maintenance remains centralized in the source spine.
- This PR does not add slab construction, charged-slab correction, ESM or surface thermodynamics tutorials.
- Work-function convergence thresholds remain target-observable dependent and are not reduced to fixed parameter recipes.

## Merge Recommendation

Ready for draft PR review after final command validation. The diff is scoped to four polar-response / electrostatics pages plus this report.

## Final QA Gate

| Gate | Result | Evidence |
|---|---|---|
| Physics accuracy | PASS | Born charge is framed as dynamic polarization response, tensor anomalies require symmetry/convergence/file-chain review, LO-TO correction requires consistent Born/dielectric/IFC data, and work function requires stable vacuum plateau plus same-chain Fermi reference. |
| Style consistency | PASS | Theory, judgement and workflow pages keep separate roles; added content is explanatory and locally scoped. |
| Source boundary | PASS | No new DOI, BibTeX or tutorial-as-authority was added; QE behavior remains tied to official INPUT/PostProc docs and canonical DFPT literature. |
| Output-review framing | PASS | Output evidence now includes tensor symmetry / sum-rule consistency, non-analytic file chain, planar/macroscopic average, two-side plateau and boundary-setting records. |
| PASS/WARN/BLOCK preservation | PASS | All four target pages retain explicit PASS/WARN/BLOCK sections or workflow decision framing. |
| Local links | PASS | Full local Markdown link check reported `OK local markdown links checked: 142 files`. |
| Private path / document residue | PASS | Target-file scan found no private machine paths or external document residues. |
| Project-scope drift | PASS | Target-file scan found no unrelated tooling drift; content stays within QE-Learning polar-response and electrostatics scope. |
| Fixed material case scan | PASS | No material-specific case examples were introduced. |
| Universal parameter scan | PASS | No fixed vacuum thickness, slab thickness, dipole, cutoff, k-mesh or response-threshold recipe was introduced. |
| High-risk overclaim scan | PASS | Keyword hits for Born charge, work function, vacuum plateau and fixed slab/vacuum language occur in misconception or boundary contexts; no positive overclaim was found. |
| Merge recommendation | READY | No BLOCK gate remains; suitable for draft PR creation and ready/merge after GitHub mergeability check. |
