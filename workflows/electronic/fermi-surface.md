# Fermi surface workflow

## 本页解决什么问题

本页说明如何审阅 Fermi surface workflow：从 metallic system 的 dense uniform NSCF eigenvalues 生成 BXSF 或其他费米面可视化数据，并与 bands、DOS 和 occupations 交叉判断 Fermi-level 附近电子结构。Fermi surface 对 k mesh、smearing、Fermi energy、band crossings、SOC 和磁性分支非常敏感；粗网格图像不能作为定量结论。

## 页面定位

- 对应学习路线：[learn/05-electronic-structure-loop.md](../../learn/05-electronic-structure-loop.md)
- 上游依赖：[workflows/ground-state/scf.md](../ground-state/scf.md)、[workflows/ground-state/nscf.md](../ground-state/nscf.md)、[workflows/electronic/dos.md](dos.md)、[workflows/electronic/bands.md](bands.md)
- 理论边界：[theory-minimum/smearing-metals.md](../../theory-minimum/smearing-metals.md)、[physics-judgement/kmesh-smearing-sensitivity.md](../../physics-judgement/kmesh-smearing-sensitivity.md)
- 规范入口：[standards/output-review-checklist.md](../../standards/output-review-checklist.md)

## 上游依赖

- SCF 与 dense NSCF 均已通过 review。
- 体系确认为金属性或存在需要审阅的 Fermi-level crossing。
- NSCF 使用 dense uniform mesh；high-symmetry bands path 不可生成费米面。
- Fermi energy、occupations/smearing、band 数量、spin/SOC/磁性设置已记录。
- 可视化工具和 BXSF 文件只用于显示，不能替代 k mesh sensitivity。

## 计算图

```text
final static SCF
  -> pw.x nscf on <dense_uniform_k_mesh>
  -> fs.x
  -> BXSF / Fermi surface file
  -> visualization
  -> output review
```

## 关键 QE 输入对象

| 字段 / 设置 | 程序 | 控制什么 | 常见风险 | Output 中如何验证 |
|---|---|---|---|---|
| `K_POINTS automatic` | `pw.x nscf` | dense uniform mesh | 用 bands path 或稀疏 mesh | NSCF output 的 k 点数量 |
| `occupations/smearing/degauss` | `pw.x` | Fermi-level occupation | smearing artifact 被解释为费米面 | output 中 occupation 和 Fermi energy |
| `nbnd` | `pw.x nscf` | 目标 band 覆盖 | band crossing 截断 | NSCF output 的 band 数和能量范围 |
| `prefix/outdir` | `fs.x` | 读取 NSCF 数据 | 读取旧 eigenvalues | `fs.x` output |
| `filfermi` 或 BXSF 输出名 | `fs.x` | 费米面文件 | 文件来源不可追踪 | BXSF 文件和 record |
| visualization settings | XCrySDen / viewer | 费米面显示 | 图像设置被当作物理证据 | viewer 记录和截图说明 |

## 命令与文件边界

```bash
pw.x -in pw.nscf.<system>.in > pw.nscf.<system>.out
fs.x -in fs.<system>.in > fs.<system>.out
```

`fs.x` 应读取 dense NSCF 数据并生成 BXSF 或等价输出。BXSF 文件必须与当前 `prefix/outdir`、Fermi energy 和 k mesh 对应。外部可视化工具只显示文件内容；图像不自动证明费米面拓扑或嵌套特征。

## 通用输入模板

```fortran
&FERMI
  prefix = '<system>',
  outdir = '<scratch_dir>',
  filfermi = 'fermi-surface.<system>.bxsf',
/
```

`fs.x` 输入字段应按当前 QE PostProc 文档核对；若本地版本使用不同字段名或 line-based 格式，应在 record 中按实际输入记录。

## Output review

| 检查项 | 从哪里看 | 能证明什么 | 不能证明什么 | WARN/BLOCK 触发 |
|---|---|---|---|---|
| metallicity 前提 | SCF/NSCF/DOS/bands output | 费米面 workflow 有物理对象 | 费米面已定量可信 | 非金属或小 gap 状态不清为 `WARN/BLOCK` |
| dense NSCF | NSCF k-point summary | 费米面来自 uniform mesh | k mesh 已足够 | mesh 太稀且用于定量形状为 `WARN/BLOCK` |
| Fermi energy | SCF/NSCF output、BXSF header | 能量参考可复查 | Fermi level 对 smearing 不敏感 | Fermi energy 不稳定或未记录为 `BLOCK` |
| band coverage | `nbnd`、eigenvalue range | crossing bands 被包含 | 所有相关 band 已正确连接 | band 数不足为 `BLOCK` |
| `fs.x` 输出 | stdout、BXSF 文件 | 可视化文件来自当前运行 | 图像解释已完成 | 文件缺失或 prefix 错配为 `BLOCK` |
| 与 DOS/bands 对照 | DOS at Fermi、bands crossing | 金属性判断可交叉检查 | DOS/bands 一致就完成所有收敛 | 图像与 bands/DOS 矛盾未解释为 `WARN/BLOCK` |

## 收敛与可靠性

- Fermi surface 对 k mesh、smearing、Fermi energy 和 band crossing 位置敏感。
- 小带隙、半金属、磁性或 SOC 体系需要特别审阅 degeneracy、spin splitting 和 band index。
- BXSF 图像粗糙、破碎或随 smearing 大幅改变时，不应写定量结论。
- Fermi surface 若用于 EPC、transport 或 nesting 解释，需要进入更严格的 k/q mesh sensitivity 和高级 workflow。

## PASS / WARN / BLOCK

| 状态 | 条件 | 是否允许进入下游 |
|---|---|---|
| `PASS` | SCF/NSCF 为 `PASS`；体系金属性明确；dense uniform mesh、Fermi energy、bands 数和 BXSF 文件可复查；与 bands/DOS 不冲突或差异已解释 | 允许进入定性 Fermi surface 图、与 DOS/bands 交叉检查、后续高级 workflow 前置记录 |
| `WARN` | mesh 或 smearing 只适合探索；小 gap/semimetal 边界不清；图像仅作预览 | 只允许内部诊断，不用于定量拓扑、nesting 或 transport 结论 |
| `BLOCK` | 上游为 `BLOCK`；非金属前提错误；k mesh 不是 uniform dense；Fermi level 未定义；band 数不足；图像与 DOS/bands 冲突未排查 | 不允许进入 Fermi surface 解释或高级下游 |

## 常见误区

- 用 bands path 或 SCF 稀疏 mesh 生成费米面。
- 只看 BXSF 图像，不检查 Fermi energy 和 band index。
- 把 smearing 造成的模糊或伪交叉当成物理费米面。
- 忽略 SOC 或磁性导致的能带劈裂。
- 将可视化软件输出当作 k mesh convergence 证据。

## 下游影响

Fermi surface 会影响 figures、metallicity statement、Wannier/EPC/transport 前置判断和 publication record。进入 EPC 或 transport 时，本页只能作为前置审阅，不能替代 dense interpolation 和目标 observable 收敛。

## 来源与边界

- QE PostProc guide: <https://www.quantum-espresso.org/Doc/pp_user_guide/>
- QE `pw.x` input reference: <https://www.quantum-espresso.org/Doc/INPUT_PW.html>
- XCrySDen: <http://www.xcrysden.org/>
- 本仓库规范：[standards/output-review-checklist.md](../../standards/output-review-checklist.md)
- 物理边界：[physics-judgement/kmesh-smearing-sensitivity.md](../../physics-judgement/kmesh-smearing-sensitivity.md)
