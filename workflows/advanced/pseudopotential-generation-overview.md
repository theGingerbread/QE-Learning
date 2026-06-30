# Pseudopotential generation overview

## 页面定位

- 对应学习路线：[learn/09-feature-expansion-map.md](../../learn/09-feature-expansion-map.md)
- 上游依赖：基础 SCF、收敛性、结构和赝势记录
- 下游用途：高级物性分析或专题 workflow
- 规范入口：[standards/calculation-record-template.md](../../standards/calculation-record-template.md)、[standards/pass-warn-block.md](../../standards/pass-warn-block.md)

## 适用问题

赝势生成的边界页，强调生成、测试、验证和记录要求。

## 进入该 workflow 前必须已经掌握什么

赝势选择、cutoff convergence、参考构型和目标元素物理。

## 关键 QE 程序或输入字段

| 字段或程序 | 用途 |
|---|---|
| `ld1.x` / atomic inputs | 生成赝势 |
| reference configuration | 参考电子构型 |
| UPF metadata | 赝势元数据 |
| validation tests | 测试计算 |

## output review 要点

- UPF 元数据是否完整
- log 是否有 warning
- cutoff 和结构/原子测试是否通过
- 与公共库赝势是否可对照

## 常见风险

- 生成后不验证
- 泛函/价态记录不足
- 拿未测试赝势进入生产 workflow

## 与基础 workflow 的关系

- 依赖 SCF、cutoff/k 点、smearing 和赝势记录。
- 高级开关改变 Hamiltonian 或数据链时，应重新审阅下游 bands、DOS、phonon 或后处理可比性。
- 本页是边界页；完整执行细节应在掌握基础 workflow 后按官方文档展开。

## 资料来源

- QE pseudopotentials page: <https://www.quantum-espresso.org/pseudopotentials/>
- QE documentation: <https://www.quantum-espresso.org/documentation/>
