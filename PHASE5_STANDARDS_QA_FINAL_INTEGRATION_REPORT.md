# Phase 5 Standards QA Final Integration Report

## Scope

本轮只处理 `standards/`、一致性 QA 和最终整合报告。目标是把 Phase 1-4 的入口修正、workflow 回填、theory-minimum 回填、physics-judgement 回填和 reference spine 整理收束成可提交 PR review 的状态。

本轮没有大规模改写 `workflows/`、`theory-minimum/`、`physics-judgement/` 正文，没有新增工具教程、具体材料案例或文献清单。

## Files changed

- `standards/README.md`
- `standards/pass-warn-block.md`
- `standards/calculation-record-template.md`
- `standards/input-file-naming.md`
- `standards/project-layout.md`
- `standards/citation-and-source-policy.md`
- `PHASE5_STANDARDS_QA_FINAL_INTEGRATION_REPORT.md`

`standards/output-review-checklist.md` 已在 Phase 2-A/2-B/2-C 覆盖 ground-state、electronic、phonon 和 advanced review。本轮审计确认其表格结构与 `PASS / WARN / BLOCK` 语义一致，未做重复扩写。

## Standards changes

### `standards/README.md`

- 强化 `standards/` 的职责：文件命名、calculation record、project layout、output review、`PASS / WARN / BLOCK`、source policy 和 final QA。
- 新增 `Final QA checklist`，把合并前检查收束为目录职责、workflow 结构、theory-minimum 映射、physics-judgement 判断、references source spine、standards 术语和全仓库 QA。

### `standards/pass-warn-block.md`

- 将状态定义统一为：
  - `PASS`：证据足以支撑当前目标允许的下游或当前层级结论。
  - `WARN`：可用于学习、趋势判断、参数摸底或排错，但不能写成最终结论。
  - `BLOCK`：关键证据缺失、数据链不一致、收敛失败、模型边界未说明或存在不可接受风险。
- 明确 `JOB DONE`、单项 SCF convergence 或后处理文件生成都不能单独决定 `PASS`。
- 新增最小审阅句式，要求每个 record 写清 `Status`、`Reason`、`Evidence`、`Downstream allowed`、`Downstream blocked` 和 `Uncertainty statement`。

### `standards/output-review-checklist.md`

- 本轮未改正文。
- 审计确认已覆盖 SCF、convergence scan、NSCF、relax、vc-relax、final static SCF、bands、DOS、PDOS、pp.x、electrostatic potential、ELF、work function、Fermi surface、phonon 和 advanced workflow。
- 各主线 workflow review 均包含“检查项 / 从哪里看 / 能证明什么 / 不能证明什么 / WARN/BLOCK 触发”或等价结构。

### `standards/calculation-record-template.md`

- 增加 `Workflow stage`，避免只写目标不写所处 workflow 阶段。
- 增加 `Key numerical settings`，显式记录 cutoff、k-point、occupation/smearing、SCF threshold、force/stress threshold 和 q-grid/q-path。
- 在 `Review status` 中增加 `Source boundary`，让来源边界与 uncertainty statement 同步记录。
- 强化 `prefix/outdir` 与人类可读文件名的区别。

### `standards/input-file-naming.md`

- 明确文件名服务人类复查，`prefix/outdir` 服务 QE 程序文件链；二者不能互相替代。
- 补充 `pp.potential`、`pp.elf` 等后处理命名。
- 强化不同结构状态、functional、pseudopotential、SOC、U、vdW 或 boundary 设置不得模糊混用。
- 增加 relax/vc-relax 后 final static SCF、NSCF、DOS/PDOS、q2r/matdyn/dynmat 等下游文件链命名边界。

### `standards/project-layout.md`

- 增加个人项目级 `references/` 目录说明，用于保存具体项目使用过的公开来源、赝势来源、工具文档入口或教程备注。
- 明确项目级 `references/` 不替代本仓库的公共 source spine。
- 在 record 映射表中加入 `Source boundary`。

### `standards/citation-and-source-policy.md`

- 与 Phase 4 的 source spine 保持一致：参数定义优先官方 `INPUT_*`；程序链优先官方 docs / package docs；物理判断优先 canonical literature；工具文档只说明工具边界；教程只作 workflow 辅助。
- 修正页面结构，把 `input 模板来源标注` 放在来源写法小节下，避免重复章节。
- 保留 version-sensitive、tutorial boundary、tool boundary 和 canonical literature 规则。

## Cross-repository QA

### Workflow 页面结构检查

检查范围：

- `workflows/ground-state/*.md`
- `workflows/electronic/*.md`
- `workflows/phonon/*.md`

结果：

- 所有检查页均包含 `Output review`。
- 所有检查页均包含 `PASS / WARN / BLOCK`。
- `standards/output-review-checklist.md` 已覆盖 ground-state、electronic、phonon 和 advanced 的最小 review gate。

### Theory-minimum 页面结构检查

检查范围：`theory-minimum/*.md`，不含 README。

结果：

- 所有理论页均包含 QE input/output 映射或等价结构。
- 所有理论页均包含 workflow 回链或 workflow 影响说明。

### Physics-judgement 页面结构检查

检查范围：`physics-judgement/*.md`，不含 README。

结果：

- 所有 judgement 页均包含 `PASS / WARN / BLOCK`。
- 所有 judgement 页均包含来源、来源边界或结论强度说明。

### References source spine 检查

结果：

- `references/source-index.md` 中外部链接均有用途说明。
- `references/canonical-literature.md` 中主题表均包含等级、支持的判断和对应仓库页面。
- `references/canonical.bib` 未发现重复 key。

### Standards 一致性检查

结果：

- `PASS / WARN / BLOCK` 定义已收束到 `standards/pass-warn-block.md`。
- calculation record、output review、file naming、project layout 和 source policy 均链接到对应 standards 页面。
- standards 不要求保存具体 input/output、scratch、wavefunction 或 restart 文件。

## Validation results

实际运行检查：

```bash
git status --short --branch
git diff --check
python3 <markdown local link checker>
rg -n <private path and research-document residue patterns> ...
rg -n <forbidden wording and overclaim patterns> ...
python3 <canonical.bib duplicate key checker>
python3 <workflow Output review / PASS-WARN-BLOCK checker>
python3 <theory-minimum QE mapping checker>
python3 <physics-judgement source and PASS-WARN-BLOCK checker>
python3 <source-index link usage checker>
python3 <canonical-literature row checker>
python3 <forbidden top-level directory checker>
```

结果摘要：

- Markdown 本地链接：通过。
- `git diff --check`：通过。
- `canonical.bib` duplicate key：通过，27 entries。
- workflow `Output review` / `PASS / WARN / BLOCK`：通过。
- theory-minimum QE 映射 / workflow 回链：通过。
- physics-judgement `PASS / WARN / BLOCK` / 来源节：通过。
- source-index 裸链接用途说明：通过。
- canonical-literature 等级 / 用途 / 页面映射：通过。
- 禁止目录 `cases/`、`archive/`、`structure-learning/`、`examples/`、`tutorial-cases/`：不存在。

扫描备注：

- Deep Research 参考文档名称仍出现在规划文件 `PROJECT_REFERENCE_INTAKE.md`、`PROJECT_BACKFILL_PRIORITY_ROADMAP.md`、`SUBAGENT_BACKFILL_TASK_PLAN.md` 和 `DEEP_RESEARCH_BACKFILL_MATRIX.md` 中。这些是 intake 的文件名记录，不是正文引用，也不是本地私有路径。
- 自动化/runtime 偏移相关词只出现在审计/报告中的边界说明和禁止项中，未进入 QE workflow、theory 或 judgement 正文作为项目方向。
- 过度结论扫描中出现的 “完全一致” 等词位于“避免写……”或“不完全一致”的负向边界语境中。

## Remaining risks

- `physics-judgement/` 仍同时保留编号 canonical pages 和快速判断页。当前可用，但长期维护建议逐步合并重复主题，避免双轨漂移。
- `canonical.bib` 已通过 duplicate key 检查，但未做全文级 metadata 校订。Phase 4 已记录 Timrov / DFPT-U 与 QHA / thermodynamics 条目的后续 metadata TODO。
- 本轮链接检查覆盖本地 Markdown 链接；外部链接只在 Phase 4 做了关键官方/工具 URL 抽查，仍建议在 PR review 前或 release 前做一次外部链接抽样。
- standards 已给出 final QA gate，但不替代逐页人工科学审稿。复杂主题如 DFT+U、SOC、Wannier、EPC、GW/BSE 仍建议按具体科研问题单页深审。

## Merge readiness

Ready for PR review。

理由：

- 目录职责、入口层、主线 workflow、theory-minimum、physics-judgement、references 和 standards 已形成稳定分层。
- 主线 workflow 已有 output review 和 `PASS / WARN / BLOCK`。
- theory-minimum 能回到 QE input/output 和 workflow。
- physics-judgement 能支撑模型边界和结果可信度判断。
- reference spine 和 source policy 已能支撑关键断言回查。
- standards 已统一记录、命名、审阅、来源和 final QA。
- 自动检查没有发现 blocking issue；剩余问题属于人工审稿和长期维护风险。

## Recommended PR description

Title:

```text
Build QE-Learning reference-handbook foundation
```

Summary:

- Realigned QE-Learning as a Quantum ESPRESSO reference handbook and DFT knowledge system.
- Upgraded entry pages and learn path around output review, verifiable learning evidence and downstream gates.
- Upgraded ground-state, electronic and phonon workflow references with QE program chains, input fields, output review and `PASS / WARN / BLOCK`.
- Upgraded theory-minimum pages so DFT/DFPT concepts map to QE input, output and workflow decisions.
- Upgraded physics-judgement pages for high-risk model-boundary interpretation: KS eigenvalues, band gaps, DFT+U, SOC, vdW, work function, Wannier, EPC, excited-state boundaries, free energy and uncertainty statements.
- Consolidated `references/` into a source spine with QE official docs, tool docs and canonical literature.
- Integrated `standards/` for file naming, calculation records, output review, source policy and final QA.

Validation:

- Markdown local links checked.
- `git diff --check` passed.
- Forbidden directory scan passed.
- `canonical.bib` duplicate key check passed.
- workflow/theory/physics judgement structural checks passed.

Known follow-up:

- Gradual readability pass.
- Selected page deep review for DFT+U/SOC/Wannier/EPC/GW/BSE.
- External source link audit.
- Release tag and handbook index preparation.

## Follow-up after merge

- Phase 6：readability pass，统一长页面的语言密度、表格节奏和读者入口。
- Phase 7：selected page deep review，针对 DFT+U、SOC、Wannier、EPC、GW/BSE、work function 和 uncertainty statement 做单页专家审稿。
- Phase 8：external source verification，抽查官方文档、工具文档和 canonical literature 链接可用性与 metadata。
- Phase 9：release tag / handbook index，为当前 reference-handbook foundation 打 tag，并生成更短的读者手册索引。
