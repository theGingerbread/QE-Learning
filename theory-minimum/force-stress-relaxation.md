# Force, stress and relaxation

## 它在 QE 中对应什么问题？

relax 和 vc-relax 通过力与应力判断结构是否达到目标平衡。结构质量直接影响 phonon、bands、DOS 和反应路径。

## 不理解它会造成什么错误？

- 看到 `JOB DONE` 就接受结构。
- 忽略 final force、stress tensor 或 optimizer failure。
- 低维体系无约束 vc-relax 导致真空方向变化。
- 把未充分优化结构送入 phonon。

## 相关 QE 输入字段

| 字段 | 所属程序 | 物理/数值含义 | 常见误用 |
|---|---|---|---|
| `calculation` | pw.x | 选择 relax 或 vc-relax | 用 SCF 代替结构优化 |
| `forc_conv_thr` | pw.x | 力收敛阈值 | 阈值与下游目标不匹配 |
| `press_conv_thr` | pw.x | 压力/应力收敛阈值 | vc-relax 只看力不看压力 |
| `ion_dynamics/cell_dynamics` | pw.x | 离子和晶胞优化算法 | 失败后不分析历史直接续算 |
| `tstress/tprnfor` | pw.x | 打印 stress/force | 没有输出就无法审阅结构 |

## output 中如何发现问题？

- final coordinates、forces、total force 是否达到目标。
- stress tensor、pressure、cell update 是否合理。
- optimizer 是否 converged 或 failed。
- 最后一次电子 SCF 是否收敛。

## 最低掌握深度

能区分“可继续优化的中间结构”和“可进入 phonon/响应性质的结构”，并记录结构下游准入理由。

## 与 workflow 页面的对应关系

- [workflows/ground-state/relax.md](../workflows/ground-state/relax.md)
- [workflows/ground-state/vc-relax.md](../workflows/ground-state/vc-relax.md)
- [workflows/phonon/phonon-dispersion-dfpt.md](../workflows/phonon/phonon-dispersion-dfpt.md)

## 资料来源

- QE INPUT_PW reference: <https://www.quantum-espresso.org/Doc/INPUT_PW.html>
