# Spin polarization workflow

## 页面定位

- 对应学习路线：[learn/09-feature-expansion-map.md](../../learn/09-feature-expansion-map.md)
- 上游依赖：基础 SCF、收敛性、结构和赝势记录
- 下游用途：高级物性分析或专题 workflow
- 规范入口：[standards/calculation-record-template.md](../../standards/calculation-record-template.md)、[standards/pass-warn-block.md](../../standards/pass-warn-block.md)

## 适用问题

磁性或自旋极化基态计算，需要比较不同初始磁矩、总磁矩和局域磁矩输出。

## 进入该 workflow 前必须已经掌握什么

SCF、occupation/smearing、赝势来源和基础收敛。

## 关键 QE 程序或输入字段

| 字段或程序 | 用途 |
|---|---|
| `nspin` | 启用自旋极化 |
| `starting_magnetization` | 设置初始磁矩 |
| `tot_magnetization` | 约束总磁矩时使用 |

## output review 要点

- total magnetization 和 absolute magnetization
- atomic magnetic moments
- 不同初始磁矩是否收敛到同一/不同态
- bands/DOS 是否保持同一自旋设置

## 常见风险

- 初始磁矩未记录
- 把局域磁矩和总磁矩混淆
- 开自旋后沿用非磁收敛结论

## 与基础 workflow 的关系

- 依赖 SCF、cutoff/k 点、smearing 和赝势记录。
- 高级开关改变 Hamiltonian 或数据链时，应重新审阅下游 bands、DOS、phonon 或后处理可比性。
- 本页是边界页；完整执行细节应在掌握基础 workflow 后按官方文档展开。

## 资料来源

- QE INPUT_PW reference: <https://www.quantum-espresso.org/Doc/INPUT_PW.html>
