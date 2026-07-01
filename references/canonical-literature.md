# Canonical Literature

本页维护 QE-Learning 的 canonical literature spine。它不是 DOI 清单，也不替代逐篇精读；它说明哪些公开文献支撑仓库中的物理判断。QE 参数定义、程序行为和工具接口仍以 [source-index.md](source-index.md) 中的官方文档入口为准。

## 分级规则

| 等级 | 定义 | 仓库用途 |
|---|---|---|
| A0 | 不可跳过；缺它会误解 DFT/QE 基础 | `theory-minimum/` 与 `physics-judgement/` 的基础判断 |
| A1 | 方法核心；缺它会误解某类 workflow | `workflows/`、`theory-minimum/` 和高级边界页 |
| A2 | 判断必读；缺它会误判 failure mode | `physics-judgement/` 的 failure-mode 和 uncertainty 判断 |
| B1 | 前沿入口；进入专题研究前先读 | `references/` 与 `workflows/advanced/` gateway |
| B2 | 专题深入；有具体科研问题再读 | 方向性补充，不进入基础路线 |
| C | 背景 | 历史和拓展阅读 |

## Fast Core Loop

Fast Core Loop 控制在 20 篇内，用于建立 QE/DFT 物理判断力。它不覆盖所有专题，但覆盖本仓库目前最常用的判断轴。

| 序 | 文献 | 等级 | 支持的判断 |
|---|---|---|---|
| 1 | Hohenberg & Kohn, *Inhomogeneous Electron Gas* | A0 | ground-state density 边界 |
| 2 | Kohn & Sham, *Self-Consistent Equations Including Exchange and Correlation Effects* | A0 | KS 辅助体系和 SCF 框架 |
| 3 | Kohn, Nobel Lecture | A0 | density-functional 方法边界 |
| 4 | Perdew, Burke & Ernzerhof, *GGA Made Simple* | A1 | GGA functional 起点 |
| 5 | Kim, Sim & Burke, DFT error decomposition | A2 | functional error / density-driven error |
| 6 | Mori-Sanchez, Cohen & Yang, DFT limitations | A2 | delocalization、gap、charge-transfer 边界 |
| 7 | Vanderbilt, Ultrasoft pseudopotentials | A1 | USPP 与 cutoff / augmentation charge 边界 |
| 8 | Blochl, PAW method | A1 | PAW 思想与 PP 边界 |
| 9 | Monkhorst & Pack, special k-points | A1 | k mesh 是 Brillouin-zone integration 对象 |
| 10 | Methfessel & Paxton, metallic smearing | A1 | smearing 的数值角色 |
| 11 | Blochl, Jepsen & Andersen, tetrahedron method | A1 | DOS / Fermi-surface integration |
| 12 | Giannozzi et al., QE code paper | A1 | QE 方法和模块总入口 |
| 13 | Giannozzi et al., QE advanced capabilities | A1 | QE 高级模块能力边界 |
| 14 | Baroni et al., DFPT review | A0 | phonon / response workflow 总入口 |
| 15 | Gonze & Lee, dynamical matrices / Born charge / dielectric tensor | A1 | polar phonon、LO-TO、response tensors |
| 16 | Cococcioni & de Gironcoli, linear-response DFT+U | A2 | U provenance |
| 17 | Marzari & Vanderbilt, MLWF | A1 | Wannier validation 起点 |
| 18 | Giustino, electron-phonon interactions review | A1 | EPC data chain |
| 19 | Onida, Reining & Rubio, electronic excitations | A0 | GW/BSE/excited-state boundary |
| 20 | Lejaeghere et al., DFT reproducibility | A2 | uncertainty / reproducibility |

## DFT foundations

| 文献 | 等级 | 支持的判断 | 对应仓库页面 | 备注 |
|---|---|---|---|---|
| Hohenberg & Kohn, *Inhomogeneous Electron Gas* | A0 | DFT 是 ground-state density framework | [dft-ks-scf.md](../theory-minimum/dft-ks-scf.md)、[dft-ground-state-boundary.md](../physics-judgement/dft-ground-state-boundary.md) | 基础理论边界 |
| Kohn & Sham, *Self-Consistent Equations Including Exchange and Correlation Effects* | A0 | KS auxiliary system、SCF 和 eigenvalue 解释边界 | [dft-ks-scf.md](../theory-minimum/dft-ks-scf.md)、[kohn-sham-eigenvalue-boundary.md](../physics-judgement/kohn-sham-eigenvalue-boundary.md) | KS eigenvalue 不自动等同实验激发 |
| Kohn, Nobel Lecture | A0 | density vs wavefunction 方法视角 | [01-dft-approximation-map.md](../physics-judgement/01-dft-approximation-map.md) | 用于物理判断导论 |

## Exchange-correlation and DFT errors

| 文献 | 等级 | 支持的判断 | 对应仓库页面 | 备注 |
|---|---|---|---|---|
| Perdew, Burke & Ernzerhof, *Generalized Gradient Approximation Made Simple* | A1 | PBE/GGA functional 起点 | [functional-choice.md](../theory-minimum/functional-choice.md)、[functional-choice-and-sensitivity.md](../physics-judgement/functional-choice-and-sensitivity.md) | functional 是模型选择 |
| Perdew et al., PBEsol | B1 | solids/surfaces 中 functional sensitivity 的专题入口 | [functional-choice-and-sensitivity.md](../physics-judgement/functional-choice-and-sensitivity.md) | 不是普适改进结论 |
| Kim, Sim & Burke, DFT error decomposition | A2 | functional error 与 density-driven error 区分 | [numerical-vs-model-error.md](../physics-judgement/numerical-vs-model-error.md) | 支撑 numerical vs model error |
| Mori-Sanchez, Cohen & Yang, DFT limitations | A2 | delocalization、self-interaction、band-gap limitation | [band-gap-problem-and-delocalization.md](../physics-judgement/band-gap-problem-and-delocalization.md) | 支撑 gap / charge-transfer 边界 |

## Pseudopotential, plane-wave, k-point and smearing

| 文献 | 等级 | 支持的判断 | 对应仓库页面 | 备注 |
|---|---|---|---|---|
| Vanderbilt, Ultrasoft pseudopotentials | A1 | USPP 与 `ecutrho` / augmentation 边界 | [pseudopotentials.md](../theory-minimum/pseudopotentials.md)、[plane-wave-cutoff.md](../theory-minimum/plane-wave-cutoff.md) | 参数定义仍回到 QE `INPUT_PW` |
| Blochl, PAW method | A1 | PAW model boundary | [pseudopotentials.md](../theory-minimum/pseudopotentials.md) | 与 QE PP 使用边界相关 |
| Monkhorst & Pack, special k-points | A1 | uniform k mesh 是 integration 对象 | [kpoints-symmetry-kpath.md](../theory-minimum/kpoints-symmetry-kpath.md)、[kpoint-convergence.md](../workflows/ground-state/kpoint-convergence.md) | band path 不能替代 mesh convergence |
| Methfessel & Paxton, metallic smearing | A1 | smearing 是金属 BZ integration 数值策略 | [smearing-metals.md](../theory-minimum/smearing-metals.md) | `degauss` 不等同实验温度 |
| Blochl, Jepsen & Andersen, improved tetrahedron method | A1 | DOS / Fermi-surface integration 边界 | [dos.md](../workflows/electronic/dos.md)、[fermi-surface.md](../workflows/electronic/fermi-surface.md) | 是否使用取决于 QE 字段和目标 workflow |

## QE software and reproducibility

| 文献 | 等级 | 支持的判断 | 对应仓库页面 | 备注 |
|---|---|---|---|---|
| Giannozzi et al., 2009 QE code paper | A1 | QE 模块化程序、PWscf/PHonon/PostProc 等方法入口 | [official-qe-docs.md](tutorial-sites/official-qe-docs.md)、[workflows/README.md](../workflows/README.md) | 不替代当前 input reference |
| Giannozzi et al., 2017 QE advanced capabilities | A1 | QE advanced modules、EPW、TDDFPT、XSpectra 等能力边界 | [learn/09-feature-expansion-map.md](../learn/09-feature-expansion-map.md) | 高级能力入口 |
| Giannozzi et al., 2020 QE toward exascale | B1 | QE 新版本能力和 exascale 方向 | [source-index.md](source-index.md) | 作为版本演化背景 |
| Lejaeghere et al., reproducibility in DFT solids | A2 | code/PP/functional/convergence 的 reproducibility 与 uncertainty | [uncertainty-statement-template.md](../physics-judgement/uncertainty-statement-template.md)、[calculation-record-template.md](../standards/calculation-record-template.md) | 支撑记录规范和 uncertainty statement |

## DFPT, phonons and response

| 文献 | 等级 | 支持的判断 | 对应仓库页面 | 备注 |
|---|---|---|---|---|
| Baroni et al., DFPT review | A0 | phonon 是 response calculation，不是普通后处理 | [dfpt-phonons.md](../theory-minimum/dfpt-phonons.md)、[phonon-dispersion-dfpt.md](../workflows/phonon/phonon-dispersion-dfpt.md) | DFPT 总入口 |
| Gonze & Lee, dynamical matrices / Born charges / dielectric tensors | A1 | Born effective charge、dielectric tensor、IFC 和 polar response | [dielectric-born-charge.md](../theory-minimum/dielectric-born-charge.md)、[dielectric-born-effective-charge.md](../workflows/phonon/dielectric-born-effective-charge.md) | 支撑 LO-TO / non-analytic correction 边界 |

## DFT+U and U provenance

| 文献 | 等级 | 支持的判断 | 对应仓库页面 | 备注 |
|---|---|---|---|---|
| Cococcioni & de Gironcoli, linear response DFT+U | A2 | U 值 provenance、linear-response U，不是元素常数 | [magnetism-soc-dftu.md](../theory-minimum/magnetism-soc-dftu.md)、[u-value-provenance-and-boundary.md](../physics-judgement/u-value-provenance-and-boundary.md) | 当前 A-level U provenance 核心 |
| Timrov / Marzari / Cococcioni DFPT Hubbard parameter papers | B1 | DFPT U、self-consistent U、U+V 的专题入口 | [u-value-provenance-and-boundary.md](../physics-judgement/u-value-provenance-and-boundary.md) | metadata 需在 Phase 4-B 精核后再入 BibTeX |

## vdW and low-dimensional systems

| 文献 | 等级 | 支持的判断 | 对应仓库页面 | 备注 |
|---|---|---|---|---|
| Dion et al., vdW-DF | A1 | nonlocal correlation / dispersion model boundary | [vdw-and-low-dimensional-boundary.md](../physics-judgement/vdw-and-low-dimensional-boundary.md)、[vdW-corrections.md](../workflows/advanced/vdW-corrections.md) | vdW model choice 不是数值收敛参数 |
| Tkatchenko & Scheffler, dispersion correction | B1 | dispersion correction family 的模型敏感性入口 | [vdw-and-low-dimensional-boundary.md](../physics-judgement/vdw-and-low-dimensional-boundary.md) | 不用于普适排序 |

## Wannier

| 文献 | 等级 | 支持的判断 | 对应仓库页面 | 备注 |
|---|---|---|---|---|
| Marzari & Vanderbilt, MLWF | A1 | Wannier functions 是子空间和 gauge 选择 | [wannier-validation-and-window-choice.md](../physics-judgement/wannier-validation-and-window-choice.md) | validation 起点 |
| Souza, Marzari & Vanderbilt, entangled bands | A1 | disentanglement、frozen/outer window 边界 | [wannier-validation-and-window-choice.md](../physics-judgement/wannier-validation-and-window-choice.md) | window choice failure mode |
| Marzari et al., MLWF review | B1 | Wannier interpolation 和应用综述入口 | [wannier90.md](tools/wannier90.md) | 进入专题前阅读 |

## EPC

| 文献 | 等级 | 支持的判断 | 对应仓库页面 | 备注 |
|---|---|---|---|---|
| Giustino, electron-phonon interactions review | A1 | EPC matrix elements、linewidth、Eliashberg、transport/superconductivity 边界 | [epc-data-chain-and-convergence.md](../physics-judgement/epc-data-chain-and-convergence.md) | EPC 物理判断核心 |
| Ponce et al., EPW code paper | A1 | EPW data chain、Wannier interpolation、EPC workflow | [epw.md](tools/epw.md)、[electron-phonon-overview.md](../workflows/advanced/electron-phonon-overview.md) | 工具行为仍查 EPW docs |

## Excited states, GW and BSE

| 文献 | 等级 | 支持的判断 | 对应仓库页面 | 备注 |
|---|---|---|---|---|
| Onida, Reining & Rubio, electronic excitations review | A0 | GW/BSE/excited-state boundary，KS bands 不替代谱学方法 | [ground-state-vs-excited-state.md](../physics-judgement/ground-state-vs-excited-state.md) | Yambo docs 是工具入口，不作为 canonical literature |

## Thermodynamics and uncertainty

| 文献 | 等级 | 支持的判断 | 对应仓库页面 | 备注 |
|---|---|---|---|---|
| Baroni et al., DFPT review | A0 | harmonic phonon / vibrational contribution 前置 | [energy-vs-free-energy.md](../physics-judgement/energy-vs-free-energy.md) | phonon 可信度先于 free-energy statement |
| Lejaeghere et al., DFT reproducibility | A2 | numerical/model/code/PP uncertainty statement | [uncertainty-statement-template.md](../physics-judgement/uncertainty-statement-template.md) | 支撑 calculation record |
| QHA / anharmonic thermodynamics references | B2 | finite-temperature free energy 专题入口 | [energy-vs-free-energy.md](../physics-judgement/energy-vs-free-energy.md) | 当前未提升为 A；后续需按具体页面用途补 metadata |

## 使用规则

- 页面正文只引用结论，不堆 DOI。
- 参数和程序行为仍以 QE 官方 `INPUT_*`、PHonon guide、Wannier90/EPW/Yambo 官方文档为准。
- 任何 version-sensitive 字段都不得只靠文献摘要确认。
- 新增文献进入 A 级前，必须说明它改变了哪个 output review 或 `PASS / WARN / BLOCK` 判断。
- BibTeX 只收录 metadata 已核验到可维护程度的条目；不确定 DOI 或卷页时先写入维护 TODO，不编造。

## 维护 TODO

- Timrov / Marzari / Cococcioni 的 DFPT Hubbard parameter 相关条目需要在 Phase 4-B 做 metadata 精核，再决定是否加入 [canonical.bib](canonical.bib)。
- QHA / anharmonic thermodynamics 文献目前只作为 B2 专题入口；只有当 `energy-vs-free-energy.md` 扩写为更具体方法页时再提升。

## 原始链接

- [QE documentation](https://www.quantum-espresso.org/documentation/)：官方文档总入口。
- [QE INPUT_PW](https://www.quantum-espresso.org/Doc/INPUT_PW.html)：`pw.x` 字段定义。
- [QE INPUT_PH](https://www.quantum-espresso.org/Doc/INPUT_PH.html)：`ph.x` 字段定义。
- [EPW documentation](https://docs.epw-code.org/)：EPW 工具行为和输入边界。
- [Wannier90 documentation](https://wannier90.readthedocs.io/)：Wannier90 工具行为和输入边界。
- [Yambo educational wiki](https://wiki.yambo-code.eu/wiki/index.php?title=Main_Page)：Yambo 工具学习入口。
