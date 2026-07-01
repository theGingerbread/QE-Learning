# Exchange-Correlation Functional Choice

## 本页解决什么问题

Exchange-correlation functional 是 Kohn-Sham DFT 中定义近似能量泛函的核心模型选择。在 QE 中，functional choice 会进入 `pw.x` 的 `input_dft`、赝势 UPF 元信息、vdW / hybrid / DFT+U 等扩展设置，并改变 total energy、平衡结构、forces、stress、bands、DOS、phonon、磁性、surface/work-function 和 response quantities。

本页给出 QE 用户最低需要掌握的 functional 判断：它不是 cutoff、k mesh 或 `conv_thr` 这类数值收敛参数，而是 Hamiltonian 和能量面的一部分。换 functional 后，结构、赝势、cutoff/k mesh/smearing、SCF、relax、phonon 和所有下游解释都需要重新审阅 provenance。

## 物理图像

Kohn-Sham DFT 把复杂的多电子相互作用压缩到 exchange-correlation functional 中。这个 functional 同时影响电子如何局域或离域、键长和体积偏好、磁性解、能带位置、声子力常数和弱相互作用结构。不同 functional 不是同一数值模型下的“精度档位”，而是不同近似模型；它们可能在某些 observables 上更合适，在另一些 observables 上更差。

QE 计算中常见的误差分层是：cutoff、k mesh、smearing 等数值参数决定“在这个模型里算得是否稳定”；functional、DFT+U、SOC、vdW 或 hybrid 决定“当前模型是否适合这个物理问题”。如果 band gap、磁性排序、层间距离或 phonon soft mode 对 functional 很敏感，单纯加密 k mesh 或提高 cutoff 只能降低数值噪声，不能消除模型边界。

## 最低理论结构

最低需要记住三个层级：

1. `E_xc[n]` 是 density functional approximation 的核心，决定 exchange-correlation energy 和 potential。
2. `input_dft`、UPF 中的 functional 元信息、vdW/hybrid/U/SOC 设置共同定义实际计算模型。
3. 同一 observable 的可比性要求模型链一致；若模型改变，应重新审阅结构和下游 workflow。

常见 functional family 的名称只提供方法类别线索，不能直接给出普适优劣顺序。LDA/GGA/meta-GGA/hybrid/vdW/DFT+U 等方法涉及不同近似、计算成本和适用边界。对 QE-Learning 而言，最低目标不是评价哪个 functional “更好”，而是让用户能记录模型、识别模型切换、判断下游是否仍可比较。

## QE 中的对应对象

| 对象 | 程序 / 文件 | 判断意义 | Output 中如何验证 |
|---|---|---|---|
| `input_dft` | `pw.x` / `&SYSTEM` | 显式指定 exchange-correlation functional，或让 QE 从赝势信息推断 | SCF output 中 XC functional 回显 |
| UPF header | pseudopotential | 记录赝势生成时的 XC、valence、relativistic treatment 等信息 | pseudopotential loading 信息、warning、source record |
| `vdw_corr` | `pw.x` / `&SYSTEM` | 启用 QE 支持的 dispersion correction 分支 | SCF output 中 vdW / XC 回显和 warning |
| hybrid 相关字段 | `pw.x` | exact exchange / screened hybrid 等模型分支 | input 回显、计算成本、k-point / q-point 限制和 warning |
| `HUBBARD` | `pw.x` | DFT+U 改变局域 manifold 模型，不是简单 functional 标签 | Hubbard setup、occupation matrices、warning |
| `prefix/outdir` | QE 文件链 | 下游 bands/DOS/phonon 是否读取同一模型的 ground-state 数据 | 下游 output 中读取的 data-file、prefix 和 scratch |

## 如何读 output

Output review 应先确认当前模型到底是什么，再解释数值结果：

- SCF output 中 exchange-correlation functional 的回显是否与 input record 一致。
- pseudopotential loading 信息是否显示所有 UPF 来源可追踪，XC family 是否与 `input_dft` 保持可解释关系。
- 是否出现 PP/XC mismatch、unsupported functional、vdW/hybrid/Hubbard warning。
- relax 或 vc-relax 后的 final structure 是否来自同一 functional；若换 functional 后直接复用旧结构，应进入 `WARN` 或 `BLOCK`。
- bands、DOS、phonon、work function、Born charge 等下游是否基于同一 `prefix/outdir` 和同一模型重新计算。
- functional sensitivity 对目标 observable 是否被记录，例如 lattice constant、band gap、magnetic state、phonon frequency、work function 或 weak-interaction geometry。

这些 output 证据能证明“当前 run 使用了某个可追踪模型”；它们不能证明该模型对目标物理问题一定足够，也不能把 semilocal gap、DFT+U gap 或 hybrid gap 自动升级为实验测量层面的带隙结论。

## 对 workflow 的影响

- SCF：`input_dft` 与 UPF 元信息决定 Hamiltonian；换 functional 后应视为新模型链。
- Convergence：cutoff/k mesh/smearing 收敛必须在当前 functional 和 PP 组合下审阅；旧收敛结论不能无记录迁移。
- Relax / vc-relax：functional 改变能量面，可能改变 equilibrium structure、forces 和 stress。
- Bands / DOS / PDOS：functional 改变 eigenvalue dispersion、gap、DOS 边缘和投影解释边界。
- Phonon / DFPT：functional 改变 force constants、Born charge、dielectric tensor 和 soft-mode 判断。
- Advanced workflows：vdW、DFT+U、hybrid、SOC、Wannier、EPC、GW/BSE 等下游都需要清楚记录模型来源和一致性。

## 常见误区

- 把 functional 当作“越高级越准”的线性等级。
- `input_dft` 与 UPF functional 不一致，却不记录目的和边界。
- 用一种 functional relax，另一种 functional 做 bands、DOS 或 phonon，但不重新做 final static SCF。
- 看到 band gap 不合预期就换 functional，却不说明模型目标、下游重算和 source boundary。
- 把 vdW、hybrid 或 DFT+U 当作无代价、无边界的精度提升。
- 只比较最后 total energy 或 gap 数值，不比较结构、PP、cutoff、k mesh、smearing 和下游文件链。
- 用教程或个人经验替代 QE `INPUT_PW` 对字段含义的定义。

## PASS / WARN / BLOCK 关联

| 状态 | 条件 | 下游准入 |
|---|---|---|
| PASS | `input_dft`、UPF functional、PP 来源、结构状态、SCF 和下游数据链一致；目标 observable 的模型边界已写入记录；必要 sensitivity 或对照已完成 | 可进入带边界的 workflow 结论 |
| WARN | 模型选择可追踪，但 functional sensitivity、PP/XC 一致性、下游重算或目标 observable 边界仍不完整 | 可用于学习、趋势或诊断，不应写成最终定量结论 |
| BLOCK | functional/PP 不一致且无说明；换 functional 后复用旧 scratch、旧结构或旧 phonon；把某个 functional 写成无边界的可靠性保证；无 source boundary 的强物理结论 | 停止下游比较和科研结论，重建模型链 |

## 与 physics-judgement 的边界

本页解释 functional choice 如何进入 QE input/output 和 workflow 准入。更高层的可信度判断应进入：

- [functional-choice-and-sensitivity.md](../physics-judgement/functional-choice-and-sensitivity.md)
- [02-exchange-correlation-ladder.md](../physics-judgement/02-exchange-correlation-ladder.md)
- [band-gap-problem-and-delocalization.md](../physics-judgement/band-gap-problem-and-delocalization.md)
- [pseudopotential-transferability-and-functional-consistency.md](../physics-judgement/pseudopotential-transferability-and-functional-consistency.md)
- [vdw-and-low-dimensional-boundary.md](../physics-judgement/vdw-and-low-dimensional-boundary.md)

## 对应 workflow

- [SCF workflow](../workflows/ground-state/scf.md)
- [relax workflow](../workflows/ground-state/relax.md)
- [bands workflow](../workflows/electronic/bands.md)
- [phonon dispersion DFPT workflow](../workflows/phonon/phonon-dispersion-dfpt.md)
- [hybrid functional overview](../workflows/advanced/hybrid-functional-overview.md)
- [vdW corrections](../workflows/advanced/vdW-corrections.md)
- [DFT+U workflow](../workflows/advanced/dft-plus-u.md)

## 来源与边界

- Stable: `input_dft`、`vdw_corr`、Hubbard syntax 和 hybrid 相关字段的具体语义以当前 QE official `INPUT_PW` 为准。
- Stable: UPF provenance、PP/XC consistency 和 `ATOMIC_SPECIES` 记录应按 [pseudopotentials.md](pseudopotentials.md) 与 [calculation-record-template.md](../standards/calculation-record-template.md) 处理。
- Boundary: functional sensitivity 是模型边界判断，不是材料无关的参数推荐。
- Version-sensitive: meta-GGA、hybrid、vdW、DFT+U 输入语法和支持范围可能随 QE 版本变化，使用前应核对官方文档。

## 资料来源

- [QE INPUT_PW](https://www.quantum-espresso.org/Doc/INPUT_PW.html)
- [Pseudopotentials](pseudopotentials.md)
- [Functional choice and sensitivity](../physics-judgement/functional-choice-and-sensitivity.md)
- [Canonical literature](../references/canonical-literature.md)
