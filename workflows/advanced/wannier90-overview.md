# Wannier90 overview

## 页面定位

- 对应学习路线：[learn/09-feature-expansion-map.md](../../learn/09-feature-expansion-map.md)
- 上游依赖：基础 SCF、收敛性、结构和赝势记录
- 下游用途：高级物性分析或专题 workflow
- 规范入口：[standards/calculation-record-template.md](../../standards/calculation-record-template.md)、[standards/pass-warn-block.md](../../standards/pass-warn-block.md)

## 适用问题

QE 到 Wannier90 的接口边界，关注 projections、窗口、插值 bands 对照和数据文件链。

## 进入该 workflow 前必须已经掌握什么

SCF/NSCF、bands、PDOS、目标轨道和 `nbnd` 策略。

## 关键 QE 程序或输入字段

| 字段或程序 | 用途 |
|---|---|
| `pw2wannier90.x` | QE 到 Wannier90 接口 |
| projections | Wannier 初始投影 |
| dis_win/dis_froz | 能量窗口 |
| *.mmn/*.amn/*.eig | 接口文件 |

## output review 要点

- 接口文件是否完整
- Wannier bands 是否对照 QE bands
- spreads 和投影是否合理
- 能量窗口是否记录

## 常见风险

- 投影选择无物理依据
- 未与 QE bands 对照
- 窗口调参无记录

## 与基础 workflow 的关系

- 依赖 SCF、cutoff/k 点、smearing 和赝势记录。
- 高级开关改变 Hamiltonian 或数据链时，应重新审阅下游 bands、DOS、phonon 或后处理可比性。
- 本页是边界页；完整执行细节应在掌握基础 workflow 后按官方文档展开。

## 资料来源

- QE INPUT_pw2wannier90 reference: <https://www.quantum-espresso.org/Doc/INPUT_pw2wannier90.html>
- Wannier90 documentation: <https://wannier90.readthedocs.io/>
