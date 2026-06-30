# DFT+U workflow

## 页面定位

- 对应学习路线：[learn/09-feature-expansion-map.md](../../learn/09-feature-expansion-map.md)
- 上游依赖：基础 SCF、收敛性、结构和赝势记录
- 下游用途：高级物性分析或专题 workflow
- 规范入口：[standards/calculation-record-template.md](../../standards/calculation-record-template.md)、[standards/pass-warn-block.md](../../standards/pass-warn-block.md)

## 适用问题

在局域轨道上加入 Hubbard correction，用于需要修正局域电子的体系。

## 进入该 workflow 前必须已经掌握什么

SCF、PDOS/轨道判断、U 值来源、赝势与 projector 设置。

## 关键 QE 程序或输入字段

| 字段或程序 | 用途 |
|---|---|
| `HUBBARD` card | 定义 Hubbard 通道和参数 |
| `lda_plus_u` legacy settings | 旧输入风格需按版本核对 |
| projectors | 定义投影方式 |

## output review 要点

- Hubbard 参数是否在 output 回显
- 投影通道是否与目标轨道一致
- 磁矩、能隙和能量是否对 U 敏感
- U 值来源是否记录

## 常见风险

- U 值无来源
- 开 DFT+U 后不重做收敛
- 把 DFT+U 结果与普通 DFT 直接混比

## 与基础 workflow 的关系

- 依赖 SCF、cutoff/k 点、smearing 和赝势记录。
- 高级开关改变 Hamiltonian 或数据链时，应重新审阅下游 bands、DOS、phonon 或后处理可比性。
- 本页是边界页；完整执行细节应在掌握基础 workflow 后按官方文档展开。

## 资料来源

- QE INPUT_PW reference: <https://www.quantum-espresso.org/Doc/INPUT_PW.html>
