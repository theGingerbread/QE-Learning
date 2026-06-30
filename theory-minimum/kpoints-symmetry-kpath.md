# K-points, symmetry and k-path

## QE 中对应的问题

k 点采样控制 Brillouin zone 积分，symmetry 控制 k 点约化和结构识别，k-path 控制 bands 图中的高对称路径。三者在 QE input 中语义不同。

## 常见错误

- 用 high-symmetry path 做 SCF 或 DOS。
- 用太粗 k mesh 判断金属性、DOS 或 phonon。
- primitive cell 与 conventional cell 混用导致 bands 标签错误。
- 开关 `nosym/noinv` 后不记录原因。

## 输入字段

| 字段 | 所属程序 | 物理/数值含义 | 常见误用 |
|---|---|---|---|
| `K_POINTS automatic` | pw.x | SCF/NSCF 的 uniform k mesh | 路径采样和积分采样混用 |
| `K_POINTS crystal_b` | pw.x bands | bands 高对称路径 | 用来做 DOS 或收敛测试 |
| `nosym/noinv` | pw.x | 控制对称性使用和反演约化 | 为修图随意关闭对称性 |
| `ibrav/CELL_PARAMETERS` | pw.x | 定义晶胞和 reciprocal basis | 结构标准化和 k-path 坐标基底不一致 |

## output review

- output 中 irreducible k-points 数量和 symmetry operations 是否符合预期。
- bands output 的 k 点顺序是否对应记录的 `<k_path>`。
- Fermi energy、总能或目标量是否随 k mesh 收敛。

## 最低掌握深度

能区分 SCF uniform mesh、NSCF dense mesh、bands path 三种 k 点语义，并记录 k-path 来源和 cell convention。

## 对应 workflow

- [workflows/ground-state/kpoint-convergence.md](../workflows/ground-state/kpoint-convergence.md)
- [workflows/electronic/bands.md](../workflows/electronic/bands.md)
- [workflows/electronic/dos.md](../workflows/electronic/dos.md)

## 资料来源

- QE INPUT_PW reference: <https://www.quantum-espresso.org/Doc/INPUT_PW.html>
- SeeK-path documentation: <https://seekpath.readthedocs.io/>
