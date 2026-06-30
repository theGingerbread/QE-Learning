# Magnetism, SOC and DFT+U

## QE 中对应的问题

磁性、SOC 和 DFT+U 会改变 Hamiltonian、对称性、赝势要求和下游可比性。它们不是单纯的绘图开关。

## 常见错误

- SOC 使用不匹配赝势。
- 初始磁矩和最终磁矩没有记录。
- 把 total magnetization、absolute magnetization 和局域磁矩混为一谈。
- U 值没有来源，开 DFT+U 后沿用旧收敛结论。

## 输入字段

| 字段 | 所属程序 | 物理/数值含义 | 常见误用 |
|---|---|---|---|
| `nspin/starting_magnetization` | pw.x | 启用并初始化自旋极化 | 不记录初始磁矩 |
| `noncolin/lspinorb` | pw.x | 启用非共线和 SOC | 赝势或结构前提不匹配 |
| `HUBBARD card` | pw.x | 定义 Hubbard 参数和通道 | U 值来源不明 |
| `occupations/smearing` | pw.x | 影响磁性金属收敛 | 与非磁计算混用策略 |

## output review

- total/absolute magnetization 和 atomic magnetic moments。
- spinor/SOC、Hubbard 参数和对称性回显。
- SCF 是否收敛，磁矩是否依赖初始条件。

## 最低掌握深度

能说明每个物理开关需要什么赝势/输入前提，以及它会改变哪些下游 workflow 的可比性。

## 对应 workflow

- [workflows/advanced/spin-polarization.md](../workflows/advanced/spin-polarization.md)
- [workflows/advanced/noncollinear-soc.md](../workflows/advanced/noncollinear-soc.md)
- [workflows/advanced/dft-plus-u.md](../workflows/advanced/dft-plus-u.md)

## 资料来源

- QE INPUT_PW reference: <https://www.quantum-espresso.org/Doc/INPUT_PW.html>
