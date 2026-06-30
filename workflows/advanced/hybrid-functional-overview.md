# Hybrid functional overview

## 页面定位

- 对应学习路线：[learn/09-feature-expansion-map.md](../../learn/09-feature-expansion-map.md)
- 上游依赖：基础 SCF、收敛性、结构和赝势记录
- 下游用途：高级物性分析或专题 workflow
- 规范入口：[standards/calculation-record-template.md](../../standards/calculation-record-template.md)、[standards/pass-warn-block.md](../../standards/pass-warn-block.md)

## 适用问题

hybrid functional 计算的边界说明，强调计算成本、k 点、收敛和与普通 DFT 结果的可比性。

## 进入该 workflow 前必须已经掌握什么

SCF、cutoff/k 点收敛、bands/DOS 基础和资源预算。

## 关键 QE 程序或输入字段

| 字段或程序 | 用途 |
|---|---|
| `input_dft` | 选择 hybrid functional |
| exact-exchange related settings | 影响计算成本和收敛 |
| k mesh | hybrid 成本敏感 |

## output review 要点

- output 是否回显 functional
- SCF 是否稳定
- 资源消耗和并行设置是否记录
- 与 semilocal DFT 的结构/参数是否一致

## 常见风险

- 把 hybrid 当作单点开关
- k 点太粗导致带隙不可用
- 资源失败误判为物理问题

## 与基础 workflow 的关系

- 依赖 SCF、cutoff/k 点、smearing 和赝势记录。
- 高级开关改变 Hamiltonian 或数据链时，应重新审阅下游 bands、DOS、phonon 或后处理可比性。
- 本页是边界页；完整执行细节应在掌握基础 workflow 后按官方文档展开。

## 资料来源

- QE INPUT_PW reference: <https://www.quantum-espresso.org/Doc/INPUT_PW.html>
