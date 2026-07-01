# PDOS workflow

## 本页解决什么问题

本页说明如何审阅 `projwfc.x` 的 projected DOS workflow。PDOS 用于把 Kohn-Sham states 投影到 QE/赝势定义的原子和轨道通道上，辅助分析态密度来源。它是投影分析，不是唯一的化学成分分解，也不能单独证明价态、电荷转移、成键强度或局域化机制。

## 页面定位

- 对应学习路线：[learn/05-electronic-structure-loop.md](../../learn/05-electronic-structure-loop.md)
- 上游依赖：[workflows/ground-state/scf.md](../ground-state/scf.md)、[workflows/ground-state/nscf.md](../ground-state/nscf.md)、[workflows/electronic/dos.md](dos.md)
- 理论边界：[theory-minimum/pseudopotentials.md](../../theory-minimum/pseudopotentials.md)、[physics-judgement/band-gap-problem-and-delocalization.md](../../physics-judgement/band-gap-problem-and-delocalization.md)
- 规范入口：[standards/output-review-checklist.md](../../standards/output-review-checklist.md)

## 上游依赖

- SCF 和 NSCF 状态已通过审阅，并保留 `projwfc.x` 需要读取的 wavefunctions。
- `prefix/outdir`、赝势、泛函、spin/SOC/DFT+U 设置与上游一致。
- `nbnd` 覆盖 PDOS 目标能区。
- total DOS 的 energy zero、broadening 和能量窗口可作为对照。
- 需要记录 PDOS 文件命名、原子顺序、投影通道和赝势 projector 的边界。

## 计算图

```text
final static SCF
  -> pw.x nscf on <dense_uniform_k_mesh>
  -> projwfc.x
  -> projected DOS files / projection summary
  -> output review
```

## 关键 QE 输入对象

| 字段 / 设置 | 程序 | 控制什么 | 常见风险 | Output 中如何验证 |
|---|---|---|---|---|
| `prefix/outdir` | `projwfc.x` | 读取 NSCF wavefunctions | 读取旧波函数或错误结构 | `projwfc.x` output 的读取信息 |
| `filpdos` | `projwfc.x` | PDOS 文件名前缀 | 文件与体系/参数无法对应 | 生成的分通道 PDOS 文件 |
| `filproj` | `projwfc.x` | projection 输出文件 | 只保留图，不保留投影证据 | projection 文件或 stdout |
| `Emin/Emax/DeltaE` | `projwfc.x` | PDOS 能量窗口和步长 | 与 total DOS 不一致 | PDOS 文件能量范围 |
| `ngauss/degauss` | `projwfc.x` | 投影 DOS 展宽 | 与 DOS broadening 混用不记录 | input/output record |
| `lsym` | `projwfc.x` | 投影对称化行为 | 对称性处理影响通道解释 | output 中投影和对称性信息 |

## 命令与文件边界

```bash
projwfc.x -in projwfc.<system>.in > projwfc.<system>.out
```

`projwfc.x` 读取上游 wavefunctions 和 eigenvalues。若 NSCF 没有写出或保留必要 wavefunctions，PDOS 可能失败或读到旧数据。PDOS 文件名通常包含原子、轨道或投影通道信息；记录时应保存 output 中的通道说明，而不是只保存最终曲线。

## 通用输入模板

```fortran
&PROJWFC
  prefix = '<system>',
  outdir = '<scratch_dir>',
  filpdos = 'pdos.<system>',
  filproj = 'proj.<system>.dat',
  Emin = <energy_min>,
  Emax = <energy_max>,
  DeltaE = <energy_step>,
  degauss = <pdos_broadening>,
  lsym = <projection_symmetry_flag>,
/
```

## Output review

| 检查项 | 从哪里看 | 能证明什么 | 不能证明什么 | WARN/BLOCK 触发 |
|---|---|---|---|---|
| wavefunction 读取 | `projwfc.x` output、`prefix/outdir` | 投影来自目标 NSCF 数据链 | 上游 NSCF 已充分收敛 | 读取失败或错配为 `BLOCK` |
| band/window 覆盖 | `nbnd`、PDOS energy window、projection summary | 目标能区有可投影态 | 高能态解释一定完整 | `nbnd` 或窗口不足为 `WARN/BLOCK` |
| 投影通道 | state labels、atomic labels、PDOS filenames | 原子/轨道标签可追踪 | 投影是唯一化学分解 | 通道不可解释或原子顺序不明为 `BLOCK` |
| total DOS 对照 | DOS/PDOS 文件、broadening、energy zero | PDOS 与 total DOS 可交叉审阅 | PDOS 求和必须严格等于 DOS | 明显冲突未解释为 `WARN/BLOCK` |
| spin/SOC/noncollinear | output 中 spinor、components、labels | 投影分量与物理模型一致 | 分量可直接按标量轨道解释 | SOC/非共线标签未说明为 `WARN` |
| warnings | `projwfc.x` stdout | 投影过程无明显 I/O 或通道错误 | 物理解释已经成立 | warning 影响文件完整性为 `BLOCK` |

## 收敛与可靠性

- PDOS 继承 SCF/NSCF 的 cutoff、k mesh、smearing 和 wavefunction 质量。
- projection basis 与 pseudopotential/projector 定义相关；更换赝势会改变可解释边界。
- Lowdin charge 可作为辅助输出，但不应被当作充分价态证据。
- PDOS 与 charge density、ELF、Wannier projection 属于不同证据类型，不能相互替代。

## PASS / WARN / BLOCK

| 状态 | 条件 | 是否允许进入下游 |
|---|---|---|
| `PASS` | 上游 SCF/NSCF/DOS 可追踪；wavefunctions 读取正确；投影通道清楚；energy zero/broadening 与 DOS 对齐；PDOS 文件完整 | 允许进入轨道成分趋势、PDOS 图和与 bands/DOS 的交叉解释 |
| `WARN` | 通道标签复杂；PDOS 与 DOS 有可解释差异；spin/SOC 分量仍需人工复核 | 只允许探索性解释，不用于最终轨道归属或价态结论 |
| `BLOCK` | wavefunction 缺失；`prefix/outdir` 错配；`nbnd` 不足；投影通道不可解释；total DOS 与 PDOS 矛盾且无法排查 | 不允许进入 PDOS 解释或图件归档 |

## 常见误区

- 把 PDOS 当作唯一、严格的化学成分分解。
- 不看 `projwfc.x` output 里的投影标签，只凭文件名解释轨道。
- 更换赝势或 projector 后直接比较 PDOS 强度。
- 用 Lowdin charge 单独证明价态或电荷转移。
- SOC/非共线情况下仍按普通标量轨道解释所有通道。

## 下游影响

PDOS 会影响 DOS/PDOS interpretation、orbital attribution、Wannier projection 选择、DFT+U manifold 讨论和 publication figure。进入 Wannier 或 DFT+U 解释前，应把 PDOS 作为候选证据，而不是最终判据。

## 来源与边界

- QE `projwfc.x` input reference: <https://www.quantum-espresso.org/Doc/INPUT_PROJWFC.html>
- QE `dos.x` input reference: <https://www.quantum-espresso.org/Doc/INPUT_DOS.html>
- 本仓库规范：[standards/output-review-checklist.md](../../standards/output-review-checklist.md)
- 物理边界：[physics-judgement/band-gap-problem-and-delocalization.md](../../physics-judgement/band-gap-problem-and-delocalization.md)、[physics-judgement/wannier-validation-and-window-choice.md](../../physics-judgement/wannier-validation-and-window-choice.md)
