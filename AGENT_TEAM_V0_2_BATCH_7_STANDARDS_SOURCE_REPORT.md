# Agent Team v0.2 Batch 7 Standards / Source Report

## Scope

Batch 7 completes the v0.2 standards, records and source-policy pass. The batch does not add new bibliography metadata or rewrite content pages. It focuses on making the existing standards/source spine more directly usable for `PASS / WARN / BLOCK`, output review, calculation records, file naming, project layout and source-boundary decisions.

## Subagents used

| Subagent | Role | Target pages | Output |
|---|---|---|---|
| Standards QA auditor | Read-only standards review | `standards/*.md` | Checked P/W/B, output review, records, naming and project layout consistency |
| Source metadata QA auditor | Read-only source review | `references/source-index.md`, `canonical-literature.md`, `canonical.bib`, tool/tutorial cards | Checked source-use boundaries, official-doc priority and duplicate BibTeX keys |
| Main agent | Writer / integrator / final QA | `standards/pass-warn-block.md`, `standards/input-file-naming.md`, `standards/project-layout.md`, `references/source-index.md` | Applied targeted additions and validation gate |

## Research summary

The existing standards/source pages were already structurally sound. The main gap was that some pages described good practice but did not explicitly connect that practice to downstream gate decisions. Batch 7 therefore added the missing bridge between source/use/provenance and `PASS / WARN / BLOCK` without turning standards pages into bureaucracy.

## Writing changes

- [standards/pass-warn-block.md](standards/pass-warn-block.md): added a source/version-boundary section explaining what official docs, QE output, canonical literature, tool docs, tutorials and internal judgement can support.
- [standards/input-file-naming.md](standards/input-file-naming.md): added naming/file-chain consequences for `PASS / WARN / BLOCK`, reconciled naming grammar with post-processing examples, and mapped workflow subdirectories to project-level layout.
- [standards/project-layout.md](standards/project-layout.md): added how project layout affects reproducibility gates, scratch-retention boundaries, and workflow subdirectory nesting.
- [standards/output-review-checklist.md](standards/output-review-checklist.md): tightened relax/vc-relax downstream admission so final static SCF is required before electronic/phonon downstream, scoped phonon PASS by chain type, and added page-end sources with usage notes.
- [standards/calculation-record-template.md](standards/calculation-record-template.md): clarified that the review-status uncertainty field is a one-line summary pointing to the detailed uncertainty section.
- [references/source-index.md](references/source-index.md): added a source-to-output-review / source-to-PWB mapping table.

## Standards QA findings

- `PASS / WARN / BLOCK` is now clearly tied to source type, output evidence, version-sensitive fields and downstream admission.
- Standards QA found three Must Fix issues: relax/vc-relax downstream permission was too broad, naming grammar did not match post-processing examples, and output/project-layout source sections were incomplete. All were fixed.
- Naming and project layout now state when weak provenance is `WARN` and when broken file chains become `BLOCK`.
- Calculation record and output review templates received targeted consistency fixes without broad rewriting.

## Source QA findings

- `source-index.md` now explains how source categories support output review and claim strength.
- `canonical.bib` duplicate-key scan passed.
- No DOI, BibTeX metadata, tool version, or source metadata was invented.
- Tool/tutorial pages remain bounded as references, not basic-path replacements.

## Validation results

- `git diff --check`: passed.
- Markdown local links: passed, 156 files checked.
- `canonical.bib` duplicate-key scan: passed, 27 keys checked.
- Batch 7 touched-file private path / document residue / project-scope drift / material-case / universal-parameter / high-risk overclaim scans: passed.
- Relax/vc-relax/final-static-SCF downstream admission consistency scan: passed by inspection and report linkage.
- Source-section compliance for touched standards pages: passed after adding usage notes to source lists.

## Remaining gaps

- Batch 8 will decide whether diagrams should link to standards/source pages.
- Batch 9 will refresh navigation and release notes after all content batches are merged.
- External source live-link checking remains a future maintenance task; this batch only checked local links and source-boundary wording.

## Final QA Gate

| Gate | Result | Evidence |
|---|---|---|
| Physics accuracy | PASS | No physics claims were expanded beyond existing source boundaries. |
| QE workflow correctness | PASS | Standards now route file/source evidence back to output review and downstream admission. |
| Output-review framing | PASS | Source and naming rules explicitly support output evidence, not just prose guidance. |
| PASS/WARN/BLOCK preservation | PASS | P/W/B consequences added to naming, project layout and source-use rules. |
| Style consistency | PASS | Additions are compact standards text, not broad checklist sprawl. |
| Source boundary | PASS | Source classes now state what they support and what they cannot replace. |
| Diagram validity, if applicable | NA | No new diagrams in this batch. |
| Local links | PASS | 156 Markdown files checked; no missing local links. |
| Private path / document residue | PASS | Touched-file scan passed. |
| Project-scope drift | PASS | No platform/runtime/system content added. |
| Fixed material case scan | PASS | No material-specific case added; `<system>` remains a placeholder convention. |
| Universal parameter scan | PASS | No universal parameter recommendation added. |
| High-risk overclaim scan | PASS | No method, source, tutorial, or tool is written as sufficient evidence by itself. |
| Merge recommendation | READY | Final validation commands passed. |
