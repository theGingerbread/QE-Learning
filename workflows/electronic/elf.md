# ELF workflow

## 本页解决什么问题

本页说明如何审阅 `pp.x` electron localization function（ELF）后处理。ELF 用于辅助观察电子局域化空间分布，可与结构、charge density、DOS/PDOS 等证据交叉讨论。ELF 是函数定义和可视化阈值共同决定的图像证据，不能单独作为键强度、键级或电荷转移的定量结论。

## 页面定位

- 对应学习路线：[learn/07-postprocessing-loop.md](../../learn/07-postprocessing-loop.md)
- 上游依赖：[workflows/ground-state/scf.md](../ground-state/scf.md)、[workflows/electronic/charge-density.md](charge-density.md)
- 规范入口：[standards/output-review-checklist.md](../../standards/output-review-checklist.md)

## 上游依赖

- SCF density 已通过 review。
- `plot_num` 已按当前 QE `INPUT_PP` 核对为 ELF。
- `iflag`、`output_format`、`fileout` 与可视化目标一致。
- 可视化等值面、切片、色标和软件版本会写入 record。

## 计算图

```text
final static SCF density
  -> pp.x ELF plot_num
  -> ELF grid / slice file
  -> visualization
  -> output review
```

## 关键 QE 输入对象

| 字段 / 设置 | 程序 | 控制什么 | 常见风险 | Output 中如何验证 |
|---|---|---|---|---|
| `prefix/outdir` | `pp.x` | 读取 SCF 数据 | 读取旧 density | `pp.x` output |
| `plot_num` | `pp.x` | 选择 ELF 输出 | 编号未核对或选错场 | `INPUT_PP` 和 output |
| `iflag` | `pp.x` | 输出维度 | 切片被解释为整体 3D 信息 | output/grid |
| `output_format` | `pp.x` | 可视化格式 | 工具读取后丢失单位或网格 | `fileout` 和工具记录 |
| visualization settings | 外部工具 | 等值面、色标、切片方向 | 图像不可复现 | figure script / record |

## 命令与文件边界

```bash
pp.x -in pp.elf.<system>.in > pp.elf.<system>.out
```

ELF 文件来自 `prefix/outdir` 中的 SCF 数据。不同等值面、色标或切片方向会改变视觉印象，因此 figure record 必须保存可视化设置。不要把外部工具渲染结果当作 QE output 证据。

## 通用输入模板

```fortran
&INPUTPP
  prefix = '<system>',
  outdir = '<scratch_dir>',
  plot_num = <elf_plot_num>,
  filplot = 'elf.<system>.dat',
/
&PLOT
  iflag = <plot_dimension>,
  output_format = <output_format>,
  fileout = 'elf.<system>.<format>',
/
```

## Output review

| 检查项 | 从哪里看 | 能证明什么 | 不能证明什么 | WARN/BLOCK 触发 |
|---|---|---|---|---|
| 上游读取 | `pp.x` output、`prefix/outdir` | ELF 来自目标 SCF | SCF 模型已适合成键解释 | 上游为 `BLOCK` 或读取旧数据为 `BLOCK` |
| `plot_num` | input、`INPUT_PP`、output | 输出对象确为 ELF | ELF 图像已经可定量解释 | 编号未核对为 `WARN`；选错输出为 `BLOCK` |
| grid / format | `iflag`、`output_format`、file header | 文件可用于目标可视化 | 网格足以做所有比较 | 维度/格式不匹配为 `WARN/BLOCK` |
| visualization record | figure script、等值面、色标、方向 | 图像可复现 | 视觉差异代表物理差异 | 未记录设置为 `WARN` |
| 交叉证据 | charge density、PDOS、结构记录 | ELF 解释有辅助证据 | ELF 单独证明键强度 | 单独用 ELF 做定量结论为 `WARN/BLOCK` |

## 收敛与可靠性

- ELF 继承 SCF density、cutoff、FFT grid 和模型设置的误差。
- 可视化阈值会改变图像印象；跨体系或跨参数比较必须统一设置。
- ELF 适合辅助讨论局域化图像，不适合作为唯一化学键定量指标。

## PASS / WARN / BLOCK

| 状态 | 条件 | 是否允许进入下游 |
|---|---|---|
| `PASS` | 上游 SCF 为 `PASS`；ELF `plot_num`、grid、format 和可视化设置可复查；解释有结构/charge/DOS/PDOS 交叉证据 | 允许进入定性 ELF 图像和受限局域化讨论 |
| `WARN` | 图像可用但可视化设置或交叉证据不足 | 只允许预览或内部比较 |
| `BLOCK` | 读取错误数据；`plot_num` 选错；图像被单独用作定量键强度或电荷转移结论 | 不允许进入 ELF 解释或图件归档 |

## 常见误区

- 把 ELF 等值面大小当成键强度。
- 不记录等值面、色标和切片方向。
- 用不同可视化设置比较不同计算。
- 不看 `pp.x` output，只保存截图。
- 用 ELF 替代 PDOS、charge density 或结构证据。

## 下游影响

ELF 可进入 figures、charge-density/PDOS cross-check 和 publication record 的定性图像部分。若用于强结论，应有其他证据链支持。

## 来源与边界

- QE `pp.x` input reference: <https://www.quantum-espresso.org/Doc/INPUT_PP.html>
- QE PostProc guide: <https://www.quantum-espresso.org/Doc/pp_user_guide/>
- 本仓库规范：[standards/output-review-checklist.md](../../standards/output-review-checklist.md)
