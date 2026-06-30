# NEB reaction path workflow

## 页面定位

- 对应学习路线：[learn/09-feature-expansion-map.md](../../learn/09-feature-expansion-map.md)
- 上游依赖：基础 SCF、收敛性、结构和赝势记录
- 下游用途：高级物性分析或专题 workflow
- 规范入口：[standards/calculation-record-template.md](../../standards/calculation-record-template.md)、[standards/pass-warn-block.md](../../standards/pass-warn-block.md)

## 适用问题

计算端点之间的最小能量路径和能垒，关注 images、路径力和收敛。

## 进入该 workflow 前必须已经掌握什么

两个端点结构、SCF/relax 参数、路径构造和能量可比性。

## 关键 QE 程序或输入字段

| 字段或程序 | 用途 |
|---|---|
| `neb.x` input | NEB 主控制 |
| number of images | 路径离散数量 |
| spring/path settings | 路径优化参数 |
| climbing image options | 能垒定位 |

## output review 要点

- 每个 image 的能量和力
- 路径是否连续
- NEB 是否收敛
- 端点是否保持目标结构

## 常见风险

- 端点不可比
- images 结构构造错误
- 只看能垒不看路径力收敛

## 与基础 workflow 的关系

- 依赖 SCF、cutoff/k 点、smearing 和赝势记录。
- 高级开关改变 Hamiltonian 或数据链时，应重新审阅下游 bands、DOS、phonon 或后处理可比性。
- 本页是边界页；完整执行细节应在掌握基础 workflow 后按官方文档展开。

## 资料来源

- QE PWneb documentation: <https://www.quantum-espresso.org/documentation/>
