# Noncollinear SOC workflow

## 页面定位

- 对应学习路线：[learn/09-feature-expansion-map.md](../../learn/09-feature-expansion-map.md)
- 上游依赖：基础 SCF、收敛性、结构和赝势记录
- 下游用途：高级物性分析或专题 workflow
- 规范入口：[standards/calculation-record-template.md](../../standards/calculation-record-template.md)、[standards/pass-warn-block.md](../../standards/pass-warn-block.md)

## 适用问题

非共线磁性和 spin-orbit coupling 计算，用于 SOC splitting、磁各向异性或自旋纹理前置分析。

## 进入该 workflow 前必须已经掌握什么

自旋极化、赝势 relativistic 能力、SCF 收敛和对称性影响。

## 关键 QE 程序或输入字段

| 字段或程序 | 用途 |
|---|---|
| `noncolin` | 启用非共线自旋 |
| `lspinorb` | 启用 spin-orbit coupling |
| fully relativistic pseudopotential | SOC 前提 |

## output review 要点

- output 是否回显 noncollinear/spin-orbit 设置
- 赝势是否支持 SOC
- 磁矩方向和总能差是否可比
- bands 是否与 SOC 设置一致

## 常见风险

- 使用不合适赝势
- SOC 与非 SOC 结果直接比较但不记录差异
- 能量差小于数值误差仍解释物理

## 与基础 workflow 的关系

- 依赖 SCF、cutoff/k 点、smearing 和赝势记录。
- 高级开关改变 Hamiltonian 或数据链时，应重新审阅下游 bands、DOS、phonon 或后处理可比性。
- 本页是边界页；完整执行细节应在掌握基础 workflow 后按官方文档展开。

## 资料来源

- QE INPUT_PW reference: <https://www.quantum-espresso.org/Doc/INPUT_PW.html>
- QE pseudopotentials page: <https://www.quantum-espresso.org/pseudopotentials/>
