# Electron-phonon overview

## 页面定位

- 对应学习路线：[learn/09-feature-expansion-map.md](../../learn/09-feature-expansion-map.md)
- 上游依赖：基础 SCF、收敛性、结构和赝势记录
- 下游用途：高级物性分析或专题 workflow
- 规范入口：[standards/calculation-record-template.md](../../standards/calculation-record-template.md)、[standards/pass-warn-block.md](../../standards/pass-warn-block.md)

## 适用问题

electron-phonon coupling 的数据依赖边界页，说明 SCF、phonon、Wannier/EPW 前置质量要求。

## 进入该 workflow 前必须已经掌握什么

严格 SCF、q-grid phonon、NSCF/Wannier 基础和 phonon debugging 能力。

## 关键 QE 程序或输入字段

| 字段或程序 | 用途 |
|---|---|
| `ph.x` electron-phonon related settings | DFPT 数据来源 |
| q-grid/k-grid | EPC 采样 |
| EPW inputs | Wannier interpolation 入口 |

## output review 要点

- phonon 是否收敛
- k/q mesh 是否记录
- Wannier interpolation 是否通过对照
- EPC 输出单位和定义是否明确

## 常见风险

- 用未收敛 phonon 做 EPC
- Wannierization 未验证
- 把 EPC 高级结果当基础 QE 输出

## 与基础 workflow 的关系

- 依赖 SCF、cutoff/k 点、smearing 和赝势记录。
- 高级开关改变 Hamiltonian 或数据链时，应重新审阅下游 bands、DOS、phonon 或后处理可比性。
- 本页是边界页；完整执行细节应在掌握基础 workflow 后按官方文档展开。

## 资料来源

- QE PHonon user guide: <https://www.quantum-espresso.org/Doc/ph_user_guide/>
- EPW documentation: <https://docs.epw-code.org/>
