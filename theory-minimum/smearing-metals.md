# Smearing and metals

## 它在 QE 中对应什么问题？

occupation 和 smearing 决定电子占据方式，影响金属 SCF 收敛、Fermi energy、力、DOS 和 phonon。

## 不理解它会造成什么错误？

- 金属使用 fixed occupations 导致 SCF 不稳。
- 绝缘体无理由使用 smearing 并解释为物理温度。
- 不同 workflow 随意改变 `degauss`，结果不可比。
- DOS 积分策略和 SCF 收敛策略混淆。

## 相关 QE 输入字段

| 字段 | 所属程序 | 物理/数值含义 | 常见误用 |
|---|---|---|---|
| `occupations` | pw.x | 选择 fixed、smearing、tetrahedra 等占据策略 | 金属/绝缘体策略混用 |
| `smearing` | pw.x | 选择展宽函数 | 未记录选择理由 |
| `degauss` | pw.x | 展宽宽度，单位 Ry | 过大改变能量、力或费米面 |
| `K_POINTS` | pw.x | 金属对 k mesh 更敏感 | 用粗 k mesh 掩盖 smearing 问题 |

## output 中如何发现问题？

- occupation scheme、Fermi energy 和 number of electrons 是否合理。
- SCF iteration 是否因占据设置振荡。
- total energy、force 或 DOS 是否对 `degauss` 过敏。

## 最低掌握深度

能说明金属 SCF 为什么常需要 smearing，并把 smearing scan 结果写入 PASS / WARN / BLOCK。

## 与 workflow 页面的对应关系

- [workflows/ground-state/smearing-and-occupations.md](../workflows/ground-state/smearing-and-occupations.md)
- [workflows/electronic/dos.md](../workflows/electronic/dos.md)
- [workflows/phonon/phonon-dispersion-dfpt.md](../workflows/phonon/phonon-dispersion-dfpt.md)

## 资料来源

- QE INPUT_PW reference: <https://www.quantum-espresso.org/Doc/INPUT_PW.html>
