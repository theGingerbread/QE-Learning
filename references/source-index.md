# Source Index

本页是 QE-Learning 的公开来源总入口。它按“能支持什么判断”组织来源，而不是按链接数量组织资料。正文页面需要引用来源时，优先链接到本页、[canonical-literature.md](canonical-literature.md) 或具体导读页，再在页末说明该来源用于核对什么。

## 使用规则

- 参数定义、默认值、输入卡片、文件名语义和程序行为：优先核对 QE 官方 `INPUT_*` reference 或 package guide。
- 程序链、文件依赖和 package 使用边界：优先核对 QE official documentation / user guide；教程只辅助理解 workflow。
- DFT、DFPT、pseudopotential、Wannier、EPC、excited-state、reproducibility 等方法判断：进入 [canonical-literature.md](canonical-literature.md) 和 [canonical.bib](canonical.bib)。
- 工具文档只说明工具边界和接口要求，不替代 QE 原生命令行 workflow、output review 或物理判断。
- Version-sensitive 字段必须查当前官方文档。旧页面、教程截图或历史笔记不能替代当前 `INPUT_*`。
- 外部教程用于学习顺序和操作拆解，不用于给出参数定义或材料无关数值建议。

## 来源如何进入 output review 和 PASS / WARN / BLOCK

来源不是装饰性引用。每个来源应服务一个明确审阅动作：

| 来源类别 | 在 output review 中支持什么 | 对 `PASS / WARN / BLOCK` 的作用 | 不能支持什么 |
|---|---|---|---|
| QE official `INPUT_*` / package docs | 核对字段、程序、文件依赖、输出文件语义和 version-sensitive 限制 | 字段或程序行为未核对时，相关判断最多为 `WARN`；字段明显不匹配可触发 `BLOCK` | 目标 observable 的物理充分性 |
| QE output evidence | 核对本次 run 实际读取的结构、PP、k/q mesh、SCF/DFPT 收敛、warning、文件链 | 是 `PASS / WARN / BLOCK` 的直接证据来源 | 方法学普适结论 |
| Canonical literature | 支撑 DFT/DFPT/PP/Wannier/EPC/excited-state/uncertainty 的方法边界 | 决定 claim strength 和是否需要 Boundary 说明 | 当前版本参数语法 |
| Tool documentation | 核对 Wannier90、EPW、Yambo、SeeK-path、Phonopy 等工具接口和输出边界 | 工具链未核对时，高级下游通常只能 `WARN` 或 `BLOCK` | QE 原生 workflow 质量 |
| Tutorial websites | 帮助学习 workflow 顺序、命令组织和常见输出阅读 | 可作为学习辅助，不应单独决定 `PASS` | 官方参数定义、材料无关数值建议 |

当正文页面引用来源时，应写清“该来源支持什么判断、不支持什么结论”。如果无法说明用途，链接不应进入 source spine。

## QE official documentation

| 来源 | 支持什么判断 | 主要对应页面 | 边界 |
|---|---|---|---|
| [Quantum ESPRESSO documentation](https://www.quantum-espresso.org/documentation/) | QE 官方 package、user guide 和 input reference 总入口 | [official-qe-docs.md](tutorial-sites/official-qe-docs.md)、[workflows/README.md](../workflows/README.md) | 入口页本身不替代具体 `INPUT_*` |
| [QE INPUT_PW](https://www.quantum-espresso.org/Doc/INPUT_PW.html) | `pw.x` 的 SCF、NSCF、bands、relax、vc-relax、occupation、cutoff、k-point、DFT+U、SOC、vdW 等字段 | `workflows/ground-state/`、`theory-minimum/`、`physics-judgement/` | 字段含义以当前官方页为准；实践建议仍需 workflow review |
| [QE INPUT_PH](https://www.quantum-espresso.org/Doc/INPUT_PH.html) | `ph.x`、DFPT perturbation、q-grid、`epsil`、EPC 入口字段 | [workflows/phonon/](../workflows/phonon)、[theory-minimum/dfpt-phonons.md](../theory-minimum/dfpt-phonons.md) | response 判断还需 PHonon guide 与 output evidence |
| [QE INPUT_PP](https://www.quantum-espresso.org/Doc/INPUT_PP.html) | `pp.x` 后处理、`plot_num`、输出格式、空间场数据提取 | [workflows/electronic/charge-density.md](../workflows/electronic/charge-density.md)、[workflows/electronic/electrostatic-potential.md](../workflows/electronic/electrostatic-potential.md) | 可视化解释不能只靠字段定义 |
| [QE INPUT_BANDS](https://www.quantum-espresso.org/Doc/INPUT_BANDS.html) | `bands.x` 后处理字段和 band data 文件 | [workflows/electronic/bands.md](../workflows/electronic/bands.md) | band path 不替代 DOS mesh 或 excited-state method |
| [QE INPUT_DOS](https://www.quantum-espresso.org/Doc/INPUT_DOS.html) | `dos.x`、DOS energy window、输出文件字段 | [workflows/electronic/dos.md](../workflows/electronic/dos.md) | DOS 可信度仍依赖 NSCF mesh、smearing 和 energy reference |
| [QE INPUT_PROJWFC](https://www.quantum-espresso.org/Doc/INPUT_PROJWFC.html) | `projwfc.x`、PDOS、projection 输出字段 | [workflows/electronic/pdos.md](../workflows/electronic/pdos.md) | projection 解释依赖 PP/projector，不能当作排他性成分分解 |
| [QE INPUT_Q2R](https://www.quantum-espresso.org/Doc/INPUT_Q2R.html) | `q2r.x`、dynamical matrices 到 IFC 的文件链 | [workflows/phonon/phonon-dispersion-dfpt.md](../workflows/phonon/phonon-dispersion-dfpt.md) | IFC 可信度依赖完整 q-grid 和上游 ph.x convergence |
| [QE INPUT_MATDYN](https://www.quantum-espresso.org/Doc/INPUT_MATDYN.html) | `matdyn.x`、phonon dispersion / phonon DOS 输出字段 | [workflows/phonon/phonon-dos.md](../workflows/phonon/phonon-dos.md) | smoothing 或 DOS mode 不替代 imaginary-frequency triage |
| [QE INPUT_DYNMAT](https://www.quantum-espresso.org/Doc/INPUT_DYNMAT.html) | `dynmat.x`、Gamma modes、ASR 和 mode analysis 字段 | [workflows/phonon/gamma-phonon.md](../workflows/phonon/gamma-phonon.md)、[workflows/phonon/ir-raman.md](../workflows/phonon/ir-raman.md) | Gamma phonon 不证明全 BZ 稳定 |
| [QE PHonon user guide](https://www.quantum-espresso.org/Doc/ph_user_guide/) | PHonon package 程序链、DFPT workflow 和文件组织 | [workflows/phonon/](../workflows/phonon) | 字段级定义仍回到 `INPUT_PH/Q2R/MATDYN/DYNMAT` |
| [QE code papers](canonical-literature.md#qe-software-and-reproducibility) | QE 方法、模块能力和 reproducibility 背景 | [canonical-literature.md](canonical-literature.md) | 论文不替代当前版本 input reference |

## QE workflow tutorials

教程用于理解 workflow 拆解和 output 阅读，不替代官方参数定义。

| 来源 | 支持什么判断 | 主要对应页面 | 边界 |
|---|---|---|---|
| [Pranab Das QE tutorial](https://pranabdas.github.io/espresso/) | SCF、convergence、relax、bands、DOS、PDOS、phonon 的 hands-on 程序链 | [pranab-das-qe-tutorial.md](tutorial-sites/pranab-das-qe-tutorial.md) | 教程参数需回到 QE `INPUT_*` 核对 |
| [Kyoto QE phonon DokuWiki](https://www2.yukawa.kyoto-u.ac.jp/~koudai.sugimoto/dokuwiki/doku.php?id=quantumespresso%3Aphonon%3A%E3%83%95%E3%82%A9%E3%83%8E%E3%83%B3%E3%81%AE%E8%A8%88%E7%AE%97) | Gamma phonon、finite-q、phonon DOS、ASR、`epsil`、Born charge、negative frequency 等 phonon 学习入口 | [kyoto-phonon-dokuwiki.md](tutorial-sites/kyoto-phonon-dokuwiki.md) | phonon 参数与版本行为仍回到 QE PHonon docs |
| [Materials Cloud QE school](https://github.com/materialscloud-org/QuantumESPRESSO-school-2023) | QE school 练习、教学型 notebooks 和高级专题入口 | [materials-cloud-qe-schools.md](tutorial-sites/materials-cloud-qe-schools.md) | 作为课程材料，不替代本仓库 output review |
| [ENCCS QE tutorial](https://enccs.github.io/efficient-materials-modelling-on-hpc/espresso-tutorial/) | HPC 运行、并行和环境记录的学习入口 | [enccs-qe-hpc-tutorials.md](tutorial-sites/enccs-qe-hpc-tutorials.md) | HPC 环境命令需按本地集群文档核对 |

## Tool documentation

工具用于辅助结构、路径、后处理或高级数据链，不替代 QE 原生命令行学习。

### Structure, k-path and visualization

| 来源 | 支持什么边界 | 对应页面 | 不替代什么 |
|---|---|---|---|
| [ASE documentation](https://ase.gitlab.io/ase) | 结构脚本、calculator 和输入生成边界 | [ase.md](tools/ase.md) | QE input/output 审阅 |
| [pymatgen documentation](https://pymatgen.org/) | 结构对象、数据处理和材料文件操作边界 | [pymatgen.md](tools/pymatgen.md) | QE workflow 可靠性判断 |
| [SeeK-path documentation](https://seekpath.readthedocs.io/en/latest/maindoc.html) | high-symmetry k-path 来源记录 | [seekpath.md](tools/seekpath.md)、[workflows/electronic/bands.md](../workflows/electronic/bands.md) | 结构/对称性审查和 k-point convergence |
| [VESTA](https://jp-minerals.org/vesta/en/) / [XCrySDen](http://www.xcrysden.org/) | 结构、charge density、Fermi surface 和场数据可视化 | [vesta-xcrysden.md](tools/vesta-xcrysden.md) | 可视化不能替代定量 output review |

### Phonon

| 来源 | 支持什么边界 | 对应页面 | 不替代什么 |
|---|---|---|---|
| [Phonopy QE interface](https://phonopy.github.io/phonopy/qe.html) | finite-displacement phonon 与 QE force 数据接口 | [phonopy-qe.md](tools/phonopy-qe.md) | 本仓库主线 DFPT phonon workflow |

### Wannier, EPC and excited-state

| 来源 | 支持什么边界 | 对应页面 | 不替代什么 |
|---|---|---|---|
| [Wannier90 documentation](https://wannier90.readthedocs.io/) | projections、windows、disentanglement、interpolation 和 `.win/.wout` 审阅 | [wannier90.md](tools/wannier90.md)、[physics-judgement/wannier-validation-and-window-choice.md](../physics-judgement/wannier-validation-and-window-choice.md) | QE bands/NSCF 上游质量和 band validation |
| [QE INPUT_pw2wannier90](https://www.quantum-espresso.org/Doc/INPUT_pw2wannier90.html) | QE-to-Wannier interface 字段 | [wannier90.md](tools/wannier90.md) | Wannier90 官方文档和 band validation |
| [EPW documentation](https://docs.epw-code.org/) | EPC、Wannier interpolation、dense k/q 和 EPC outputs 的高级入口 | [epw.md](tools/epw.md)、[physics-judgement/epc-data-chain-and-convergence.md](../physics-judgement/epc-data-chain-and-convergence.md) | SCF、phonon、Wannier convergence |
| [Yambo educational wiki](https://wiki.yambo-code.eu/wiki/index.php?title=Main_Page) / [Yambo learn](https://www.yambo-code.eu/learn/) | GW/BSE 和 excited-state workflow 学习入口 | [yambo.md](tools/yambo.md)、[physics-judgement/ground-state-vs-excited-state.md](../physics-judgement/ground-state-vs-excited-state.md) | ground-state DFT、KS-level bands/DOS 边界 |

### Workflow / provenance advanced reference

| 来源 | 支持什么边界 | 对应页面 | 不替代什么 |
|---|---|---|---|
| [AiiDA-QE tutorials](https://aiida-quantumespresso.readthedocs.io/en/latest/tutorials/) | provenance、workflow graph、restart 和 scheduler integration 的高级参考 | [aiida-qe-optional.md](tools/aiida-qe-optional.md)、[learn/08-hpc-and-reproducibility.md](../learn/08-hpc-and-reproducibility.md) | QE 原生命令行 workflow、output review 和物理判断 |

## Canonical literature spine

| 来源 | 支持什么判断 | 对应页面 | 边界 |
|---|---|---|---|
| [Canonical Literature](canonical-literature.md) | A0/A1/A2/B1/B2/C 文献分级，支撑 DFT、DFPT、PP、Wannier、EPC、excited-state、reproducibility 等判断 | `theory-minimum/`、`physics-judgement/` | 不替代 QE 或工具官方字段文档 |
| [Canonical BibTeX](canonical.bib) | 已核对核心文献的 BibTeX 起点 | [canonical-literature.md](canonical-literature.md) | 只收录 metadata 较稳定的条目，不强行补未知 DOI |
| [Reading Maintenance Policy](reading-maintenance-policy.md) | 文献新增、分级调整和 source freshness 维护规则 | [standards/citation-and-source-policy.md](../standards/citation-and-source-policy.md) | 不作为正文引用来源本身 |
