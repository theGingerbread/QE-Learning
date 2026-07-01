# Phase 2-C Phonon Workflow Report

## Scope

本轮只处理 `workflows/phonon/` 中的 phonon / DFPT workflow 页面，并同步补强 `standards/output-review-checklist.md` 的 phonon review 条目。修改范围集中在 `ph.x`、`dynmat.x`、`q2r.x`、`matdyn.x`、phonon DOS、Born effective charge、dielectric tensor、IR/Raman 和 imaginary frequency triage。

## Files changed

- `workflows/phonon/gamma-phonon.md`
- `workflows/phonon/phonon-dispersion-dfpt.md`
- `workflows/phonon/phonon-dos.md`
- `workflows/phonon/dielectric-born-effective-charge.md`
- `workflows/phonon/ir-raman.md`
- `workflows/phonon/phonon-debugging.md`
- `standards/output-review-checklist.md`
- `PHASE2C_PHONON_WORKFLOW_REPORT.md`

## Workflow pages upgraded

### `workflows/phonon/gamma-phonon.md`

- 补强 Gamma phonon 的定位：zone-center modes；全 Brillouin zone 稳定性需要 q-grid dispersion 审阅。
- 补充 `ph.x` 与 `dynmat.x` 的关键 input 字段：`prefix/outdir`、`tr2_ph`、`trans`、`epsil`、`fildyn`、`asr`。
- 增加 output review 表，覆盖上游 SCF、q 点、perturbation convergence、acoustic modes、imaginary frequency、dielectric/Born 分支和文件链。
- 增加 PASS / WARN / BLOCK，明确 `JOB DONE` 或频率表不能替代 perturbation 和文件链审阅。

### `workflows/phonon/phonon-dispersion-dfpt.md`

- 重构 DFPT dispersion 数据链：final static SCF -> `ph.x` q-grid -> `q2r.x` IFC -> `matdyn.x` q-path。
- 补充 `ldisp`、`nq1/nq2/nq3`、`start_q/last_q`、`fildyn`、`flfrc`、`zasr`、`asr`、`q_in_band_form` 的审阅意义。
- 强化 `q2r.x` 和 `matdyn.x` 文件边界，防止不同结构、q-grid 或 ASR 设置混用。
- 补充 q-grid、ASR、polar correction 和 imaginary frequency triage 的 WARN/BLOCK 判断。

### `workflows/phonon/phonon-dos.md`

- 明确 phonon DOS 来自 IFC 和 DOS q mesh，不是单条 q-path。
- 补充 `matdyn.x` DOS mode 中 `dos`、`nk1/nk2/nk3`、`deltaE`、`fldos`、`flfrq`、`asr` 的字段审阅。
- 增加 output review，强调 frequency range、negative frequencies、broadening/step 和 `flfrc` 来源。
- 明确平滑 DOS 曲线不能替代 dispersion 和低频/虚频审阅。

### `workflows/phonon/dielectric-born-effective-charge.md`

- 将 dielectric tensor 和 Born effective charge 定位为 DFPT response quantities。
- 补强 `epsil=.true.`、绝缘体条件、Gamma limit、tensor symmetry、LO-TO splitting 和 non-analytic correction 的文件链边界。
- 增加 output review 表，覆盖 response convergence、dielectric tensor、Born tensors、tensor symmetry、warnings 和 polar correction。
- 明确金属或 occupation 边界不清时不应解释 Born charge 或 dielectric tensor。

### `workflows/phonon/ir-raman.md`

- 将 IR/Raman 定位为 Gamma phonon 与 response tensor 的后续解释，而非只读频率表。
- 补充 `epsil`、`lraman`、`fildyn`、`asr`、mode symmetry、degeneracy 和 broadening 边界。
- 增加 PASS / WARN / BLOCK，明确 harmonic DFPT 与有限温实验 spectrum 之间的近似边界。
- 保持本页为最低审阅框架，不扩写为完整 spectroscopy 教程。

### `workflows/phonon/phonon-debugging.md`

- 建立 imaginary frequency triage 的症状分类：`ph.x` 不收敛、acoustic 异常、小虚频、整条 branch 虚频、q2r 缺失、LO-TO 异常、2D Gamma 附近异常。
- 补充上游 SCF、force/stress、cutoff/k mesh/smearing、q-grid、ASR、`epsil` 和文件链的排查表。
- 明确 ASR 只作为诊断和约束，上游收敛仍需独立审阅。
- 补充 PASS / WARN / BLOCK，防止未经排查就宣称真实动力学不稳定。

## Source boundary

本轮使用的来源类别：

- QE official docs：用于 QE 程序和 package 边界。
- QE INPUT references：`INPUT_PH`、`INPUT_Q2R`、`INPUT_MATDYN`、`INPUT_DYNMAT` 用于参数定义和文件语义。
- PHonon user guide：用于 DFPT workflow 和 PHonon package 边界。
- canonical literature：DFPT、phonon、Born charge、dielectric tensor 和 response theory 的方法背景。
- internal standards：`standards/pass-warn-block.md`、`standards/output-review-checklist.md` 和 calculation record 规范。

参数定义以官方 `INPUT_*` 为准；文献只用于方法背景和判断边界，不替代官方参数语义。

## What was intentionally not changed

- 未处理 EPC、Wannier、GW/BSE、MD、NEB 或 thermodynamics 页面。
- 未大规模修改 `theory-minimum/` 或 `physics-judgement/` 正文。
- 未新增具体材料参数，也未新增材料无关的 q-grid、cutoff 或 k mesh 数值建议。
- 未将 IR/Raman 扩写为完整实验光谱教程。
- 未把 ASR、Gamma phonon、平滑 phonon DOS 或 harmonic DFPT 写成无条件物理结论。

## Follow-up

下一步建议进入 Phase 3：`theory-minimum/` 回填。优先让 `dfpt-phonons.md`、`dielectric-born-charge.md`、`plane-wave-cutoff.md`、`kpoints-symmetry-kpath.md` 与已补强的 ground-state、electronic、phonon workflow 形成稳定回链。
