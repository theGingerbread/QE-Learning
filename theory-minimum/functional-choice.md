# Exchange-Correlation Functional Choice

## QE 中对应的问题

交换关联泛函不是普通数值参数，而是 DFT 模型的一部分。在 QE 中，它会影响总能、平衡结构、力、应力、bands、DOS、phonon、磁性、表面能、vdW 相关结构和后续响应性质。学习 QE 时最低要掌握的是：泛函选择必须和赝势、结构优化、收敛测试和目标 observable 一起记录。

本页只说明 QE 使用所需的最低判断，不评价某个泛函对具体材料一定更好，也不给材料特定推荐。

## 输入字段

| 字段 | 所属程序 | 含义 | 常见误用 |
|---|---|---|---|
| `input_dft` | `pw.x` / `&SYSTEM` | 显式指定交换关联泛函或让 QE 从赝势信息推断 | 手动覆盖 UPF 信息但不记录原因 |
| UPF header | pseudopotential | 记录赝势生成时使用的 XC 信息 | 混用不同 XC 赝势却只看文件名 |
| `vdw_corr` | `pw.x` / `&SYSTEM` | 启用半经验或非局域 vdW 修正入口 | 把 vdW 当作后处理装饰，不重审结构 |
| hybrid 相关字段 | `pw.x` | exact exchange / screened hybrid 相关设置 | 只替换 `input_dft`，不重审收敛和计算成本 |
| `HUBBARD` | `pw.x` | DFT+U 不是泛函本身，但改变局域子空间模型 | 用 U 拟合某个结果却不记录来源 |

## output review

- 查看 SCF output 中 exchange-correlation functional 的回显，确认它与记录一致。
- 查看 pseudopotential 加载信息和 warning，确认所有元素的 UPF 来源、XC 族和相对论类型可追踪。
- 如果结构由某个 functional relax 得到，后续 bands、DOS、phonon 或 work function 应说明是否沿用同一模型。
- 比较不同 functional 的结果时，不能只比较最后数值；应同时记录结构、赝势、cutoff、k mesh、smearing 和下游 workflow 是否重新审阅。
- hybrid、meta-GGA、vdW、DFT+U 等分支涉及额外字段和版本边界，参数含义以 QE 官方文档为准。

## 常见错误

| 错误 | 为什么危险 | 最低诊断动作 |
|---|---|---|
| 把 functional 当作“精度等级” | 更高阶或更复杂不自动保证所有性质更准 | 说明目标 observable 和模型选择原因 |
| 用一种 functional relax，另一种 functional 解释 phonon/bands | 结构差异会传递到下游性质 | 记录模型切换，并重做 final SCF 与必要收敛 |
| 混用 pseudopotential XC | electron-ion model 不一致 | 回查 UPF header、QE output 和 pseudo source |
| 认为加密 k mesh 可修复 band gap problem | band gap problem 属于模型边界，不是普通积分误差 | 回到 physics judgement 的 band-gap 页面 |
| 不记录 vdW/U/hybrid 来源 | 结果不可复查，模型不可比较 | 写入 calculation record 的 model provenance |

## 最低掌握深度

读完本页应能回答：

- `input_dft` 和 UPF 中的 XC 信息为什么必须一起审阅。
- 为什么 functional choice 是模型选择，而不是 cutoff/k mesh 这类数值收敛参数。
- 为什么换 functional 后需要重新审阅结构、赝势、cutoff、k mesh 和目标 observable。
- 为什么 band gap、磁性、phonon、vdW 结构和 work function 对 functional 可能有不同敏感性。
- 什么时候只能写 `WARN`：例如模型切换已记录但未完成下游收敛或实验/高阶方法对照。

## 对应 workflow

- [workflows/ground-state/scf.md](../workflows/ground-state/scf.md)
- [workflows/ground-state/relax.md](../workflows/ground-state/relax.md)
- [workflows/electronic/bands.md](../workflows/electronic/bands.md)
- [workflows/phonon/phonon-dispersion-dfpt.md](../workflows/phonon/phonon-dispersion-dfpt.md)
- [workflows/advanced/hybrid-functional-overview.md](../workflows/advanced/hybrid-functional-overview.md)
- [workflows/advanced/vdW-corrections.md](../workflows/advanced/vdW-corrections.md)
- [workflows/advanced/dft-plus-u.md](../workflows/advanced/dft-plus-u.md)
- [physics-judgement/functional-choice-and-sensitivity.md](../physics-judgement/functional-choice-and-sensitivity.md)
- [physics-judgement/band-gap-problem-and-delocalization.md](../physics-judgement/band-gap-problem-and-delocalization.md)

## 资料来源

- [QE INPUT_PW](https://www.quantum-espresso.org/Doc/INPUT_PW.html)
- [theory-minimum/pseudopotentials.md](pseudopotentials.md)
- [physics-judgement/02-exchange-correlation-ladder.md](../physics-judgement/02-exchange-correlation-ladder.md)
- [references/canonical-literature.md](../references/canonical-literature.md)
