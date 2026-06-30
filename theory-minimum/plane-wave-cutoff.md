# Plane-wave cutoff

## QE 中对应的问题

平面波 cutoff 控制基组大小，是 QE 中总能、力、应力、phonon 和后处理可信度的核心数值参数。`ecutwfc` 控制波函数 cutoff，`ecutrho` 控制电荷密度和势的 cutoff。

## 常见错误

- 直接照搬教程 cutoff，不对目标性质做收敛测试。
- 换赝势后沿用旧 cutoff。
- 只看总能收敛，忽略力、应力或 phonon 对 cutoff 的敏感性。
- 对 USPP/PAW 的 `ecutrho` 设置过低。

## 输入字段

| 字段 | 所属程序 | 物理/数值含义 | 常见误用 |
|---|---|---|---|
| `ecutwfc` | pw.x | 波函数平面波 kinetic-energy cutoff，单位 Ry | 只用单点结果判断可信 |
| `ecutrho` | pw.x | 电荷密度和势 cutoff，单位 Ry | 对增强电荷或应力敏感任务设得过低 |
| `ATOMIC_SPECIES` | pw.x | 赝势文件决定推荐 cutoff 和 valence 设置 | 混用不同来源赝势后不重新收敛 |
| `tstress/tprnfor` | pw.x | 输出应力和力以辅助 cutoff 判断 | 只记录总能，不记录目标量 |

## output review

- output 中 `kinetic-energy cutoff` 与 `charge density cutoff` 是否符合 input。
- 总能、力、应力或目标性质随 cutoff scan 是否达到可接受变化。
- 赝势类型和 warning 是否提示 cutoff 风险。

## 最低掌握深度

能设计 `<ecutwfc>/<ecutrho>` 扫描，固定其他变量，用目标量而不只用总能给出 PASS / WARN / BLOCK。

## 对应 workflow

- [workflows/ground-state/cutoff-convergence.md](../workflows/ground-state/cutoff-convergence.md)
- [workflows/ground-state/scf.md](../workflows/ground-state/scf.md)
- [workflows/ground-state/relax.md](../workflows/ground-state/relax.md)
- [workflows/phonon/phonon-dispersion-dfpt.md](../workflows/phonon/phonon-dispersion-dfpt.md)

## 资料来源

- QE INPUT_PW reference: <https://www.quantum-espresso.org/Doc/INPUT_PW.html>
- QE pseudopotentials page: <https://www.quantum-espresso.org/pseudopotentials/>
