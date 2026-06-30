# Molecular dynamics workflow

## 页面定位

- 对应学习路线：[learn/09-feature-expansion-map.md](../../learn/09-feature-expansion-map.md)
- 上游依赖：基础 SCF、收敛性、结构和赝势记录
- 下游用途：高级物性分析或专题 workflow
- 规范入口：[standards/calculation-record-template.md](../../standards/calculation-record-template.md)、[standards/pass-warn-block.md](../../standards/pass-warn-block.md)

## 适用问题

QE 中分子动力学相关计算的边界页，关注积分、温控、轨迹和能量漂移审阅。

## 进入该 workflow 前必须已经掌握什么

SCF 稳定性、力可靠性、时间步长和目标 ensemble。

## 关键 QE 程序或输入字段

| 字段或程序 | 用途 |
|---|---|
| `calculation` | MD/BOMD 相关计算模式 |
| `ion_dynamics` | 离子动力学设置 |
| `dt` | 时间步长 |
| temperature/thermostat settings | 温控参数 |

## output review 要点

- 能量、温度、压力随步数变化
- SCF 每步是否收敛
- 轨迹是否有异常结构
- restart 信息是否完整

## 常见风险

- 时间步长过大
- SCF 每步未收敛
- 把短轨迹当统计结论

## 与基础 workflow 的关系

- 依赖 SCF、cutoff/k 点、smearing 和赝势记录。
- 高级开关改变 Hamiltonian 或数据链时，应重新审阅下游 bands、DOS、phonon 或后处理可比性。
- 本页是边界页；完整执行细节应在掌握基础 workflow 后按官方文档展开。

## 资料来源

- QE INPUT_PW reference: <https://www.quantum-espresso.org/Doc/INPUT_PW.html>
- QE CP documentation: <https://www.quantum-espresso.org/documentation/>
