# vdW corrections workflow

## 页面定位

- 对应学习路线：[learn/09-feature-expansion-map.md](../../learn/09-feature-expansion-map.md)
- 上游依赖：基础 SCF、收敛性、结构和赝势记录
- 下游用途：高级物性分析或专题 workflow
- 规范入口：[standards/calculation-record-template.md](../../standards/calculation-record-template.md)、[standards/pass-warn-block.md](../../standards/pass-warn-block.md)

## 适用问题

为层状、分子吸附或弱相互作用体系加入 van der Waals correction。

## 进入该 workflow 前必须已经掌握什么

SCF/relax、结构维度、目标相互作用类型和泛函选择。

## 关键 QE 程序或输入字段

| 字段或程序 | 用途 |
|---|---|
| `vdw_corr` | 选择 vdW correction |
| `input_dft` | 交换关联泛函 |
| cell/structure settings | 影响层间距和真空 |

## output review 要点

- output 是否回显 vdW 设置
- relax/vc-relax 后的距离和应力
- 与无 vdW 设置的差异是否可追溯

## 常见风险

- 结构优化对 vdW 方法敏感
- 不同 vdW 方法结果不可直接混用
- 只改功能开关不重做 relax

## 与基础 workflow 的关系

- 依赖 SCF、cutoff/k 点、smearing 和赝势记录。
- 高级开关改变 Hamiltonian 或数据链时，应重新审阅下游 bands、DOS、phonon 或后处理可比性。
- 本页是边界页；完整执行细节应在掌握基础 workflow 后按官方文档展开。

## 资料来源

- QE INPUT_PW reference: <https://www.quantum-espresso.org/Doc/INPUT_PW.html>
