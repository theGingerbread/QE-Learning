# Electrostatic potential workflow

## 本页解决什么问题

本页说明如何审阅 `pp.x` 和 `average.x` 的 electrostatic/local potential 后处理。potential profile 常用于 slab、surface、interface、band alignment 和 work function 前置分析。电势有零点/规范选择和边界条件问题；profile 图像不能脱离上游 SCF、平均方向、真空平台和能量参考直接解释。

## 页面定位

- 对应学习路线：[learn/07-postprocessing-loop.md](../../learn/07-postprocessing-loop.md)
- 上游依赖：[workflows/ground-state/scf.md](../ground-state/scf.md)
- 下游：[workflows/electronic/work-function.md](work-function.md)
- 物理边界：[physics-judgement/work-function-and-electrostatic-boundary.md](../../physics-judgement/work-function-and-electrostatic-boundary.md)

## 上游依赖

- SCF output 已通过 review，结构、赝势、k mesh、smearing 和边界条件记录完整。
- 已明确要提取的 potential 类型，并按当前 `INPUT_PP` 核对 `plot_num`。
- 若用于 slab/work function，必须记录表面法向、平均方向、真空区域、是否有偶极修正或低维边界设置。
- `average.x` 的输入格式和单位应按当前 QE PostProc 文档核对；不同版本或构建可能有差异。

## 计算图

```text
final static SCF
  -> pp.x potential plot_num
  -> potential filplot
  -> average.x along <direction>
  -> planar / averaged potential profile
  -> output review
```

## 关键 QE 输入对象

| 字段 / 设置 | 程序 | 控制什么 | 常见风险 | Output 中如何验证 |
|---|---|---|---|---|
| `prefix/outdir` | `pp.x` | 读取 SCF 势和密度数据 | 旧 scratch 或错误结构 | `pp.x` output |
| `plot_num` | `pp.x` | 选择 potential 类型 | 混淆 electrostatic/local/total potential | `INPUT_PP` 与 output |
| `filplot` | `pp.x` | average.x 读取的中间文件 | 文件覆盖或来源不明 | `filplot` 生成记录 |
| `iflag/output_format` | `pp.x` | 输出维度和格式 | 与 average.x 或可视化不匹配 | output 和文件头 |
| average direction | `average.x` | 方向平均 | 与 slab 法向不一致 | averaged profile 横轴 |
| boundary / dipole settings | `pw.x` | slab/低维静电边界 | 忽略偶极场或周期镜像 | SCF output 和 input record |

## 命令与文件边界

```bash
pp.x -in pp.potential.<system>.in > pp.potential.<system>.out
average.x < average.<system>.in > average.<system>.out
```

`average.x` 在 QE PostProc 中常以 line-based 输入读取 `filplot` 并输出平均 profile；具体输入顺序应按当前 PostProc 文档核对。不要把 `pp.x` 三维势文件、`average.x` 平均 profile 和绘图后的能量零点混成一个不可追踪文件。

## 通用输入模板

```fortran
&INPUTPP
  prefix = '<system>',
  outdir = '<scratch_dir>',
  plot_num = <potential_plot_num>,
  filplot = 'potential.<system>.dat',
/
&PLOT
  iflag = <plot_dimension>,
  output_format = <output_format>,
  fileout = 'potential.<system>.<format>',
/
```

`average.x` 输入请按当前 QE PostProc 文档记录为 line-based 文件，并在 record 中写明 `input_file`、`output_file`、平均方向和 profile 横轴单位。

## Output review

| 检查项 | 从哪里看 | 能证明什么 | 不能证明什么 | WARN/BLOCK 触发 |
|---|---|---|---|---|
| 上游读取 | `pp.x` output、`prefix/outdir` | potential 来自目标 SCF | SCF 和 slab 边界已可信 | 读取错误数据为 `BLOCK` |
| potential 类型 | `plot_num`、`INPUT_PP`、output | 提取的势类型可复查 | 不同势类型可混用 | 势类型未说明为 `WARN`；选错为 `BLOCK` |
| 平均方向 | average input/output、cell 方向记录 | profile 方向与目标一致 | profile 已有真空平台 | 法向/方向不清为 `WARN/BLOCK` |
| 真空平台 | averaged profile、绘图脚本 | 是否存在平坦参考区 | work function 已定量可信 | 平台不平坦且仍读数为 `BLOCK` |
| 能量零点 | SCF Fermi energy、profile offset、record | 能量参考可复查 | 零点选择无影响 | Fermi/profile 参考混乱为 `BLOCK` |
| warning / file overwrite | `pp.x`/`average.x` output、文件时间戳 | 文件链没有明显破坏 | 图像解释完成 | 输出文件缺失或覆盖风险为 `WARN/BLOCK` |

## 收敛与可靠性

- potential profile 继承 SCF、结构、边界条件和真空设置的误差。
- slab 或 surface 判断必须审阅真空平台、平均方向、偶极效应和周期镜像。
- potential 的零点不是绝对物理量；跨计算比较必须说明参考和同一数据链。

## PASS / WARN / BLOCK

| 状态 | 条件 | 是否允许进入下游 |
|---|---|---|
| `PASS` | 上游 SCF 为 `PASS`；potential 类型、平均方向、文件链、单位和能量参考可复查；若用于 slab，真空平台存在 | 允许进入 work-function pre-analysis、band alignment 草图或 potential figure |
| `WARN` | profile 可读但平台、方向、边界或单位仍需复核 | 只允许探索性图像，不写定量 work function |
| `BLOCK` | 上游为 `BLOCK`；`plot_num` 错误；方向不明；无真空平台却读 vacuum level；文件链错配 | 不允许进入 work-function 或 electrostatic interpretation |

## 常见误区

- 混淆 local potential、electrostatic potential 和绘图后平移过的 potential。
- 不记录 average direction。
- 真空平台不平坦仍直接读 work function。
- 将不同计算的 Fermi energy 和 potential profile 混用。
- 把可视化曲线平滑程度当成静电边界可信度。

## 下游影响

electrostatic potential 是 work function、slab electrostatics、interface alignment 和部分 charged-state 讨论的前置证据。若本页为 `WARN` 或 `BLOCK`，下游 work-function 也不能升级为定量结论。

## 来源与边界

- QE `pp.x` input reference: <https://www.quantum-espresso.org/Doc/INPUT_PP.html>
- QE PostProc guide: <https://www.quantum-espresso.org/Doc/pp_user_guide/>
- 物理边界：[physics-judgement/work-function-and-electrostatic-boundary.md](../../physics-judgement/work-function-and-electrostatic-boundary.md)
- 本仓库规范：[standards/output-review-checklist.md](../../standards/output-review-checklist.md)
