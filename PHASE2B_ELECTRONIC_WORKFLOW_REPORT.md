# Phase 2-B Electronic Workflow Report

## Scope

本轮只处理 `workflows/electronic/` 中的电子结构与后处理 workflow 页面，并最小范围补强 `standards/output-review-checklist.md` 中 electronic workflow 相关的 output review 条目。

本轮目标是把 bands、DOS、PDOS、charge density、electrostatic potential、ELF、work function 和 Fermi surface 写成可审查、可复查、可作为参考手册阅读的 QE 原生命令行 workflow 页面。它不进入 phonon/DFPT、Wannier、EPC、GW/BSE、MD、NEB 或 thermodynamics 页面。

`workflows/electronic/` 当前没有 `README.md`，本轮未新增目录索引页，避免扩大结构范围。

## Files changed

- `workflows/electronic/bands.md`
- `workflows/electronic/dos.md`
- `workflows/electronic/pdos.md`
- `workflows/electronic/charge-density.md`
- `workflows/electronic/electrostatic-potential.md`
- `workflows/electronic/elf.md`
- `workflows/electronic/work-function.md`
- `workflows/electronic/fermi-surface.md`
- `standards/output-review-checklist.md`

## Workflow pages upgraded

### `workflows/electronic/bands.md`

- 补强 bands 的目标边界：沿 high-symmetry k-path 评估 Kohn-Sham eigenvalue dispersion，不替代 DOS 的 uniform mesh。
- 补强上游 final static SCF、`prefix/outdir`、k-path 来源、cell convention、`nbnd`、`bands.x` 和 `filband` 文件边界。
- 增加 output review 证据表，覆盖上游读取、k-path、band 数量、energy reference、spin/SOC/symmetry 和 `bands.x` 产物。
- 明确 semilocal DFT band gap 需要物理边界，不能直接写成实验 gap。
- 增加 `PASS / WARN / BLOCK`，覆盖 k-path 与结构错配、energy zero 不明、`prefix/outdir` 错配和 `filband` 缺失。

### `workflows/electronic/dos.md`

- 补强 DOS 数据链：final static SCF -> dense uniform NSCF -> `dos.x` -> `fildos`。
- 补强 `K_POINTS automatic`、`occupations/smearing/degauss`、`bz_sum`、`Emin/Emax/DeltaE`、`fildos` 和 energy reference。
- 增加 output review 证据表，覆盖 NSCF 上游、k-points、broadening/method、energy grid、Fermi reference 和 bands 对照。
- 明确 DOS 曲线平滑不等于收敛，DOS gap / peak / Fermi-level DOS 需要记录 k mesh、broadening 和能量零点。
- 增加 `PASS / WARN / BLOCK`，覆盖用 bands path 做 DOS、kmesh 过粗、smearing/degauss 未记录、Fermi level 不明和 DOS/bands 冲突。

### `workflows/electronic/pdos.md`

- 补强 PDOS 的解释边界：投影分析不是唯一化学成分分解。
- 补强 `projwfc.x`、wavefunction 读取、projection basis、`filpdos`、`filproj`、`lsym`、energy window 和 broadening。
- 增加 output review 证据表，覆盖 wavefunction 读取、band/window 覆盖、投影通道、total DOS 对照、spin/SOC/noncollinear 分量和 warning。
- 明确 Lowdin charge 与 PDOS 只能作为辅助证据，不能单独证明价态、电荷转移或键强度。
- 增加 `PASS / WARN / BLOCK`，覆盖 wavefunction 缺失、`prefix/outdir` 错配、`nbnd` 不足、投影通道不清和 PDOS/DOS 冲突。

### `workflows/electronic/charge-density.md`

- 补强 `pp.x` 从 SCF density 提取空间场数据的文件链边界。
- 补强 `plot_num`、`filplot`、`iflag`、`output_format`、`fileout` 和 difference charge density 的一致性要求。
- 增加 output review 证据表，覆盖上游读取、`plot_num`、grid/dimension、文件生成、可视化设置和差分密度。
- 明确 isosurface / contour 图不能替代积分或定量分析。

### `workflows/electronic/electrostatic-potential.md`

- 补强 potential 类型、平均方向、energy reference、slab 真空平台和 `average.x` 的版本敏感边界。
- 增加 output review 证据表，覆盖上游读取、potential 类型、average direction、vacuum plateau、energy zero 和 file overwrite。
- 明确 potential 零点和真空平台不清时，不能进入 work function 定量分析。

### `workflows/electronic/elf.md`

- 补强 ELF 的定性解释边界：ELF 是局域化图像证据，不是键强度或电荷转移定量指标。
- 补强 `plot_num`、grid、format、可视化等值面、色标和交叉证据要求。
- 增加 output review 证据表和 `PASS / WARN / BLOCK`，避免把截图或等值面当成独立物理证明。

### `workflows/electronic/work-function.md`

- 补强 work function 的 slab electrostatics 逻辑：`E_vac - E_F` 必须来自同一计算链。
- 补强 slab 方向、vacuum region、Fermi energy、potential profile、dipole/boundary treatment 和 vacuum plateau。
- 增加 output review 证据表，覆盖 SCF 可信度、slab 方向、potential profile、Fermi energy、dipole/boundary 和同一数据链。
- 明确真空平台不平坦、Fermi level 未记录或 potential reference 不清时不得给定量 work function。

### `workflows/electronic/fermi-surface.md`

- 补强 Fermi surface 的适用边界：只适用于有 Fermi surface 的金属性或需审阅 Fermi-level crossing 的体系。
- 补强 dense NSCF、Fermi energy、occupations/smearing、`nbnd`、`fs.x`、BXSF 和可视化工具边界。
- 增加 output review 证据表，覆盖 metallicity 前提、dense NSCF、Fermi energy、band coverage、`fs.x` 输出和 bands/DOS 对照。
- 明确粗 kmesh、smearing artifact、small-gap/semimetal、SOC/磁性都会影响费米面解释。

### `standards/output-review-checklist.md`

- 为 Bands、DOS、PDOS、pp.x 增加 `检查项 | 从哪里看 | 能证明什么 | 不能证明什么 | WARN/BLOCK 触发` 证据表。
- 新增 Electrostatic potential、ELF、Work function、Fermi surface 审阅表。
- 新增 Electronic common BLOCK triggers，覆盖 `prefix/outdir` 错配、用 path 做 DOS/PDOS/Fermi surface、energy reference 缺失、DFT gap 过度解释、可视化过度解释和 work function 数据链断裂。

## Source boundary

本轮使用的来源类别：

- QE official documentation；
- QE `INPUT_PW`、`INPUT_BANDS`、`INPUT_DOS`、`INPUT_PROJWFC`、`INPUT_PP` references；
- QE PostProc guide；
- `references/source-index.md` 和 `references/canonical-literature.md` 中已有 canonical literature spine；
- 本仓库 `standards/pass-warn-block.md`、`standards/calculation-record-template.md` 和 `standards/output-review-checklist.md` 的内部规范。

参数定义以 QE 官方 `INPUT_*` 为准。Kohn-Sham eigenvalue、DFT band gap、DOS/PDOS 解释、visualization 和 work function 的边界来自 canonical literature 与本仓库 physics-judgement 页面；这些边界不替代 QE 官方参数定义。

## What was intentionally not changed

本轮没有处理：

- `workflows/phonon/` 中的 Gamma phonon、DFPT dispersion、q2r、matdyn、phonon DOS、Born effective charge、IR/Raman、phonon debugging；
- `workflows/advanced/` 中的 EPC、Wannier、GW/BSE、MD、NEB、hybrid、DFT+U、SOC、vdW；
- `theory-minimum/` 正文大扩写；
- `physics-judgement/` 正文大扩写；
- 任何具体材料案例、材料绑定数值建议或可被误读为通用答案的参数表述。

## Follow-up

Phase 2-C 建议进入 `workflows/phonon/`：

- `workflows/phonon/gamma-phonon.md`
- `workflows/phonon/phonon-dispersion-dfpt.md`
- `workflows/phonon/phonon-dos.md`
- `workflows/phonon/dielectric-born-effective-charge.md`
- `workflows/phonon/ir-raman.md`
- `workflows/phonon/phonon-debugging.md`

Phase 2-C 的重点应是 `ph.x`、`dynmat.x`、`q2r.x`、`matdyn.x` 的文件链，Gamma vs q-grid phonon，ASR 与虚频判断，Born effective charge / dielectric tensor 的适用条件，以及 phonon output review 和下游准入。
