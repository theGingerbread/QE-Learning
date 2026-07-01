# Charge density workflow

## 本页解决什么问题

本页说明如何审阅 `pp.x` charge density 后处理。charge density 文件来自已收敛的 SCF ground-state density，可用于空间分布可视化、定性比较和后续分析准备。`pp.x` 只是提取或转换已有数据，不会修复上游 SCF、cutoff、k mesh、赝势或物理模型问题。

## 页面定位

- 对应学习路线：[learn/07-postprocessing-loop.md](../../learn/07-postprocessing-loop.md)
- 上游依赖：[workflows/ground-state/scf.md](../ground-state/scf.md)
- 规范入口：[standards/output-review-checklist.md](../../standards/output-review-checklist.md)、[standards/pass-warn-block.md](../../standards/pass-warn-block.md)

## 上游依赖

- SCF output 已通过 review，`prefix/outdir` 指向当前结构、赝势、泛函和 spin/SOC 设置。
- `plot_num` 已按当前 QE `INPUT_PP` 核对为目标 charge density 类型。
- `filplot`、`fileout`、`iflag`、`output_format` 与后续可视化或分析工具匹配。
- 若做 difference charge density，参与差分的所有密度必须使用一致的 cell、原子顺序、FFT grid、单位和参考定义。

## 计算图

```text
final static SCF density
  -> pp.x with charge-density plot_num
  -> filplot
  -> fileout for visualization / analysis
  -> output review
```

## 关键 QE 输入对象

| 字段 / 设置 | 程序 | 控制什么 | 常见风险 | Output 中如何验证 |
|---|---|---|---|---|
| `prefix/outdir` | `pp.x` | 读取上游 SCF 数据 | 读取旧 density 或错误结构 | `pp.x` output 读取信息 |
| `plot_num` | `pp.x` | 选择输出的空间场 | 未核对编号含义 | `INPUT_PP` 和 `pp.x` output |
| `filplot` | `pp.x` | 中间 plot 文件 | 被旧文件覆盖 | 文件生成时间和 output |
| `iflag` | `pp.x` | 输出维度 | 用切片解释整体 3D 分布 | output 的 grid / dimension |
| `output_format` | `pp.x` | 输出格式 | 可视化工具不匹配 | `fileout` 格式和工具读取 |
| `fileout` | `pp.x` | 最终空间场文件 | 文件名无法追踪来源 | 文件名、record、output |

## 命令与文件边界

```bash
pp.x -in pp.density.<system>.in > pp.density.<system>.out
```

`pp.x` 读取 `prefix/outdir` 中的 SCF 数据；`filplot` 和 `fileout` 只是后处理产物。可视化软件只显示这些数据，不判断上游是否收敛。跨计算差分需要把所有输入数据链写进 record，否则差分图进入 `WARN` 或 `BLOCK`。

## 通用输入模板

```fortran
&INPUTPP
  prefix = '<system>',
  outdir = '<scratch_dir>',
  plot_num = <charge_density_plot_num>,
  filplot = 'charge-density.<system>.dat',
/
&PLOT
  iflag = <plot_dimension>,
  output_format = <output_format>,
  fileout = 'charge-density.<system>.<format>',
/
```

## Output review

| 检查项 | 从哪里看 | 能证明什么 | 不能证明什么 | WARN/BLOCK 触发 |
|---|---|---|---|---|
| 上游读取 | `pp.x` output、`prefix/outdir` | 空间场来自目标 SCF | SCF 本身可信 | 读取错误 scratch 为 `BLOCK` |
| `plot_num` | input record、`INPUT_PP`、`pp.x` output | 输出量类型可复查 | 图像一定有目标物理含义 | 编号未核对为 `WARN`；选错输出量为 `BLOCK` |
| grid / dimension | `pp.x` output、`iflag`、文件头 | 输出维度与分析目标一致 | 网格足以做所有定量分析 | 切片/方向错误为 `WARN/BLOCK` |
| 文件生成 | `filplot`、`fileout`、时间戳、record | 后处理文件来自当前运行 | 文件内容已经可解释 | 文件缺失或被旧文件覆盖为 `BLOCK` |
| 可视化设置 | figure script、isosurface/cut plane 记录 | 图像可复现 | 图像是定量积分结果 | 未记录等值面/色标/裁剪为 `WARN` |
| 差分密度 | 参与差分的记录、cell/grid 对照 | 差分计算可追踪 | 差分一定代表电荷转移 | 参考计算不一致为 `BLOCK` |

## 收敛与可靠性

- charge density 质量继承 SCF 的收敛、cutoff、FFT grid、赝势和模型设置。
- isosurface 或 contour 图只能作为可视化证据；定量电荷讨论需要积分区域、参考定义和误差说明。
- difference charge density 对网格、参考态和结构对齐敏感，不能把不同 cell 或不同 FFT grid 的文件直接相减。

## PASS / WARN / BLOCK

| 状态 | 条件 | 是否允许进入下游 |
|---|---|---|
| `PASS` | 上游 SCF 为 `PASS`；`plot_num`、grid、format、fileout 清楚；文件来自当前 `prefix/outdir`；可视化设置已记录 | 允许进入图像生成、定性空间分布讨论和受限定量分析准备 |
| `WARN` | 上游为 `WARN`；图像只用于预览；可视化设置不完整；差分参考仍需核对 | 只允许探索性显示，不写定量结论 |
| `BLOCK` | 上游 SCF 为 `BLOCK`；读取旧数据；`plot_num` 错误；文件缺失；差分对象不可比 | 不允许进入 charge density 解释或图件归档 |

## 常见误区

- 把漂亮的 isosurface 当作定量电荷结论。
- 不记录 `plot_num` 和 `output_format`。
- 用不同结构或网格的密度做差分。
- 忽略上游 SCF 的 cutoff 和 FFT grid 对密度图的影响。
- 可视化软件中调整等值面后不更新记录。

## 下游影响

charge density 可影响 figures、difference-density discussion、ELF/PDOS 交叉解释和 publication record。它不替代 DOS、PDOS、Bader/积分分析或物理模型判断。

## 来源与边界

- QE `pp.x` input reference: <https://www.quantum-espresso.org/Doc/INPUT_PP.html>
- QE PostProc guide: <https://www.quantum-espresso.org/Doc/pp_user_guide/>
- 本仓库规范：[standards/output-review-checklist.md](../../standards/output-review-checklist.md)

`plot_num` 和 output format 属于 version-sensitive 内容，应以当前 QE PostProc 文档为准。
