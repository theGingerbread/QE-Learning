# Deep Research Backfill Matrix

本矩阵把 Deep Research 参考文档映射到当前仓库页面、回填主题、推荐 subagent 和优先级。它用于后续派发任务，不直接等同于正文修改清单。

优先级定义：

- `P0`：影响项目定位、入口、学习路线、主线判断的页面。
- `P1`：影响 QE 主线计算可靠性的页面。
- `P2`：影响物理判断、理论边界、来源追踪的页面。
- `P3`：高级扩展、工具导读、后续优化页面。

| 仓库文档 | 当前类型 | 当前问题 | 可用参考文档 | 回填主题 | 推荐 subagent | 优先级 | 风险 |
|---|---|---|---|---|---|---|---|
| `README.md` | Project landing page | 定位已清楚，但可补“参考手册 + DFT 知识体系”的一句式边界和回填入口 | Learn Landing Page Review; Source Map | 五目录职责、学习主线、正文来源边界 | A. Learn Path Refinement | P0 | 不要扩写成教程或过程报告 |
| `learn/README.md` | Learn path | 已有能力路线，可补“可验证输出”与 workflow/standards 联动表 | Learn Landing Page Review; Output Evidence Review | 能力目标、完成判据、output review、下游准入 | A. Learn Path Refinement | P0 | 避免时间计划和具体材料任务 |
| `learn/00-start-here.md` | Learn path | 可进一步强化“跑通不等于可信”和个人记录边界 | Learn Landing Page Review; Result Credibility Blueprint | 初学闭环、PASS/WARN/BLOCK、output evidence | A. Learn Path Refinement | P0 | 不要写成项目宣言 |
| `learn/01-qe-workflow-map.md` | Learn path | 可补 `prefix/outdir` 数据边和分支 workflow 图 | Workflow Reference Upgrade; Parameter Blueprint | 程序链、数据依赖、分支关系 | A. Learn Path Refinement | P0 | 图不要变成工具执行系统 |
| `learn/02-first-scf-loop.md` | Learn path | 可补 SCF output evidence 与参数角色分类 | Parameter Blueprint; Output Evidence Review | program header、pseudopotential、cutoff、k-points、SCF iteration | A. Learn Path Refinement | P1 | 不要给固定参数 |
| `learn/03-convergence-loop.md` | Learn path | 可补目标 observable 与 numerical/model error 区分 | Parameter Blueprint; Numerical vs Model Error | cutoff、ecutrho、kmesh、smearing、convergence table | A. Learn Path Refinement | P1 | 避免把收敛阈值写成普适数值 |
| `learn/04-relaxation-loop.md` | Learn path | 可补 relax 后 final static SCF 和 stress/pressure 下游影响 | Workflow Reference Upgrade; Structure/Stress Blueprint | relax/vc-relax、force/stress、下游准入 | A. Learn Path Refinement | P1 | 不展开结构构建 |
| `learn/05-electronic-structure-loop.md` | Learn path | 可补 KS eigenvalue 边界、bands/DOS/PDOS 互查 | DFT Foundation; Workflow Reference Upgrade | bands、DOS、PDOS、Fermi reference、gap 解释边界 | A. Learn Path Refinement | P1 | 不把 KS gap 当实验 gap |
| `learn/06-phonon-dfpt-loop.md` | Learn path | 可补 phonon response workflow 的物理判断入口 | DFPT/Phonon Brief; Output Evidence Review | DFPT、q-grid、ASR、negative frequency、Born charge | A. Learn Path Refinement | P1 | 不把 ASR 写成收敛替代 |
| `learn/07-postprocessing-loop.md` | Learn path | 可补后处理证据与物理解释边界 | Workflow Reference Upgrade; Output Evidence Review | `pp.x`、charge density、potential、ELF、work function | A. Learn Path Refinement | P2 | 图像后处理不要过度解释 |
| `learn/08-hpc-and-reproducibility.md` | Learn path | 可补 provenance 与 uncertainty statement 的入口 | Source Map; Output Evidence Review; Literature Loop | environment、command、scratch、restart、source boundary | A. Learn Path Refinement | P2 | 不转成自动化系统文档 |
| `learn/09-feature-expansion-map.md` | Learn path | 可接入 canonical source 和 advanced boundary | Source Map; Authoritative Literature Loop | 高级功能入口、版本敏感项、来源类型 | A. Learn Path Refinement | P3 | 不写成功能百科 |
| `workflows/README.md` | Workflow reference | 可强化 workflow 页统一验收格式 | Workflow Reference Upgrade | 阅读方法、主线页/高级页区别、output review 标准 | B. Workflow Reference Upgrade | P0 | 不重写目录结构 |
| `workflows/ground-state/scf.md` | Workflow reference | 可补参数角色分类和 output evidence “能证明/不能证明” | Parameter Blueprint; Output Evidence Review | `CONTROL/SYSTEM/ELECTRONS`、pseudopotential、cutoff、kmesh、SCF convergence | B. Workflow Reference Upgrade | P1 | `JOB DONE` 不能等于 PASS |
| `workflows/ground-state/nscf.md` | Workflow reference | 可补 NSCF 与 bands/DOS/Wannier 下游数据边 | Workflow Reference Upgrade; Parameter Blueprint | dense kmesh、`nbnd`、occupation、`prefix/outdir` | B. Workflow Reference Upgrade | P1 | bands path 不能替代 DOS mesh |
| `workflows/ground-state/cutoff-convergence.md` | Workflow reference | 可补 target observable 和 PP 类型影响 | Parameter Blueprint; Numerical vs Model Error | `ecutwfc`、`ecutrho`、NC/USPP/PAW、force/stress/phonon | B. Workflow Reference Upgrade | P1 | 不写固定 cutoff |
| `workflows/ground-state/kpoint-convergence.md` | Workflow reference | 可补 irreducible k-points、shifted mesh、维度敏感性 | Parameter Blueprint; kmesh/smearing Blueprint | uniform kmesh、DOS mesh、metal/low-dimensional sensitivity | B. Workflow Reference Upgrade | P1 | 不把 high-symmetry path 当收敛测试 |
| `workflows/ground-state/smearing-and-occupations.md` | Workflow reference | 可补 smearing 对 energy/force/DOS/phonon 的证据边界 | Parameter Blueprint; Metals/Smearing Blueprint | `occupations`、`smearing`、`degauss`、Fermi energy | B. Workflow Reference Upgrade | P1 | 不给材料无关 degauss 建议 |
| `workflows/ground-state/relax.md` | Workflow reference | 可补 final static SCF 和 force/stress 下游准入 | Workflow Reference Upgrade; Relax Boundary | `calculation='relax'`、`&IONS`、final coordinates、forces | B. Workflow Reference Upgrade | P1 | 不把 relax output 直接当电子结构终态 |
| `workflows/ground-state/vc-relax.md` | Workflow reference | 可补 cell 改变后 kmesh 重审和低维边界 | Workflow Reference Upgrade; Relax Boundary | `&CELL`、stress、pressure、final cell、static SCF | B. Workflow Reference Upgrade | P1 | 不展开结构构造 |
| `workflows/electronic/bands.md` | Workflow reference | 可补 KS eigenvalue 边界和 k-path 来源 | DFT Foundation; Workflow Reference Upgrade | `pw.x bands`、`bands.x`、`K_POINTS crystal_b`、Fermi reference | B. Workflow Reference Upgrade | P1 | 不把 bands 当 spectroscopy |
| `workflows/electronic/dos.md` | Workflow reference | 可补 energy zero、broadening 和 bands 对照 | Workflow Reference Upgrade; kmesh/smearing Blueprint | NSCF dense mesh、`dos.x`、`Emin/Emax/DeltaE` | B. Workflow Reference Upgrade | P1 | 不用 bands path 算 DOS |
| `workflows/electronic/pdos.md` | Workflow reference | 可补 projector/赝势轨道标签边界 | Workflow Reference Upgrade; Band Gap/Delocalization | `projwfc.x`、orbital projection、Lowdin charge | B. Workflow Reference Upgrade | P1 | 不把 PDOS 投影当精确电荷分解 |
| `workflows/electronic/charge-density.md` | Workflow reference | 可补 charge density 与后处理解释边界 | Workflow Reference Upgrade; Output Evidence Review | `pp.x`、`plot_num`、visualization | B. Workflow Reference Upgrade | P2 | 图像不能自动证明定量结论 |
| `workflows/electronic/electrostatic-potential.md` | Workflow reference | 可补 average.x、单位、方向、真空平台 | Workflow Reference Upgrade; Work Function Boundary | `pp.x`、local potential、planar average | B. Workflow Reference Upgrade | P1 | 不把平台噪声结果写成 work function |
| `workflows/electronic/elf.md` | Workflow reference | 可补 ELF 解释边界 | Workflow Reference Upgrade | `pp.x`、ELF、visualization | B. Workflow Reference Upgrade | P3 | 不把 ELF 当键强度定量 |
| `workflows/electronic/work-function.md` | Workflow reference | 可补 slab electrostatics 和 uncertainty | Work Function Boundary; Output Evidence Review | vacuum level、Fermi level、dipole correction、potential plateau | B. Workflow Reference Upgrade | P1 | 不写成单行公式 |
| `workflows/electronic/fermi-surface.md` | Workflow reference | 可补 `fs.x`、BXSF、dense NSCF | Workflow Reference Upgrade; Metals/Smearing Blueprint | Fermi surface、kmesh、XCrySDen | B. Workflow Reference Upgrade | P2 | 只适合金属性边界 |
| `workflows/phonon/gamma-phonon.md` | Workflow reference | 可补 `epsil`、metal/insulator 和 `dynmat.x` 边界 | Workflow Reference Upgrade; DFPT Brief | `ph.x` q=0、`tr2_ph`、`fildyn`、ASR | B. Workflow Reference Upgrade | P1 | dielectric/Born 只在适用条件下解释 |
| `workflows/phonon/phonon-dispersion-dfpt.md` | Workflow reference | 可补 dyn/fc/freq 文件链和 q-grid evidence | Workflow Reference Upgrade; Output Evidence Review | `ph.x ldisp`、`q2r.x`、`matdyn.x`、negative frequency | B. Workflow Reference Upgrade | P1 | 虚频不能直接定性 |
| `workflows/phonon/phonon-dos.md` | Workflow reference | 可补 DOS mode、qmesh 和 ASR 边界 | Workflow Reference Upgrade; DFPT Brief | q-grid、force constants、frequency DOS | B. Workflow Reference Upgrade | P1 | 插值 DOS 依赖 q-grid |
| `workflows/phonon/dielectric-born-effective-charge.md` | Workflow reference | 可补 non-analytic correction 和 metal boundary | DFPT Brief; PH official docs | `epsil`、Born effective charge、dielectric tensor、LO-TO | B. Workflow Reference Upgrade | P1 | 金属中不要解释 Born charge |
| `workflows/phonon/ir-raman.md` | Workflow reference | 可补 PH 官方字段和最低边界 | Workflow Reference Upgrade; Source Map | Gamma phonon、IR/Raman branch、source check | B. Workflow Reference Upgrade | P3 | 不扩写成谱学教程 |
| `workflows/phonon/phonon-debugging.md` | Workflow reference | 可补虚频三分法和 ASR 边界 | Imaginary Frequency Triage; Output Evidence Review | ph.x convergence、acoustic modes、negative frequency、q-grid | B. Workflow Reference Upgrade | P1 | ASR 不能替代收敛 |
| `workflows/advanced/dft-plus-u.md` | Workflow reference | 可补 U provenance 和版本敏感 `HUBBARD` card | Parameter Blueprint; U Value Provenance | `HUBBARD`、hp.x、manifold、projector | E. Physics Judgement | P2 | 不把 U 当 gap fitting |
| `workflows/advanced/noncollinear-soc.md` | Workflow reference | 可补 SOC 赝势、symmetry 和 output evidence | Parameter Blueprint; SOC Boundary | `noncolin`、`lspinorb`、fully relativistic PP | E. Physics Judgement | P2 | 不把 SOC 写成单一开关 |
| `workflows/advanced/vdW-corrections.md` | Workflow reference | 可补 vdW 模型选择和结构传播 | Functional/Sensitivity; vdW Boundary | `vdw_corr`、functional consistency、relax/postprocess | E. Physics Judgement | P2 | 不写成普适精度提升 |
| `workflows/advanced/hybrid-functional-overview.md` | Workflow reference | 可补 exact exchange sampling 和 model uncertainty | Functional Blueprint; Literature Loop | `input_dft`、hybrid fields、`ecutfock` | E. Physics Judgement | P3 | 不写成万能 band gap 修正 |
| `workflows/advanced/wannier90-overview.md` | Workflow reference | 可补 window/projection/band validation | Wannier/EPC Blueprint; Literature Loop | projections、windows、spread、QE bands 回对 | E. Physics Judgement | P2 | spread 小不等于成功 |
| `workflows/advanced/electron-phonon-overview.md` | Workflow reference | 可补完整数据链和 observable 风险 | EPC Blueprint; Literature Loop | DFPT -> Wannier -> dense k/q -> observable | E. Physics Judgement | P2 | 不只看 lambda 或 Tc |
| `theory-minimum/README.md` | Theory minimum | 可补与 `physics-judgement/` 分工 | Theory Minimum Brief | 最低理论 vs 可信度判断 | D. Theory Minimum | P0 | 不重写成理论教材目录 |
| `theory-minimum/dft-ks-scf.md` | Theory minimum | 可补 ground-state boundary 和 KS eigenvalue boundary | Theory Minimum Brief; DFT Foundation | density、total energy、SCF、eigenvalue 解释边界 | D. Theory Minimum | P1 | 不做长推导 |
| `theory-minimum/plane-wave-cutoff.md` | Theory minimum | 可补 numerical convergence 与 PP 类型 | Parameter Blueprint | basis cutoff、`ecutwfc`、`ecutrho`、output check | D. Theory Minimum | P1 | 不给万能 cutoff |
| `theory-minimum/pseudopotentials.md` | Theory minimum | 可补 transferability、functional consistency、UPF 元信息 | Parameter Blueprint; Source Map | PP source、functional、valence、cutoff hints | D. Theory Minimum | P1 | 不把库推荐当科学保证 |
| `theory-minimum/kpoints-symmetry-kpath.md` | Theory minimum | 可补 uniform mesh vs k-path、symmetry reduction | Parameter Blueprint; Workflow Reference | kmesh、irreducible points、k-path convention | D. Theory Minimum | P1 | 不展开结构标准化 |
| `theory-minimum/smearing-metals.md` | Theory minimum | 可补 Fermi surface 和 smearing 边界 | kmesh/smearing Blueprint | occupations、Fermi energy、DOS broadening | D. Theory Minimum | P1 | 不用 smearing 掩盖小 gap |
| `theory-minimum/force-stress-relaxation.md` | Theory minimum | 可补 final static SCF 和 pressure/stress | Relax Boundary | force、stress、cell、downstream admissibility | D. Theory Minimum | P1 | 不把优化收敛当全部性质收敛 |
| `theory-minimum/magnetism-soc-dftu.md` | Theory minimum | 可补最低边界和 advanced 回链 | U/SOC Blueprint | spin、SOC、DFT+U、output moment | D. Theory Minimum | P2 | 不扩写成磁性教材 |
| `theory-minimum/dfpt-phonons.md` | Theory minimum | 可补 response workflow、q-grid 和虚频边界 | DFPT Brief; Imaginary Frequency Triage | `ph.x`、`tr2_ph`、`ldisp`、ASR | D. Theory Minimum | P1 | 不把 phonon 当普通后处理 |
| `theory-minimum/dielectric-born-charge.md` | Theory minimum | 可补 insulator condition 和 non-analytic correction | DFPT Brief | `epsil`、Born charge、dielectric tensor | D. Theory Minimum | P1 | 不在金属中解释 Born charge |
| `physics-judgement/README.md` | Physics judgement | 已有目录，可补 Deep Research 分层和结论强度说明 | Result Credibility Blueprint; Literature Loop | 现象回查、误差类型、claim strength | E. Physics Judgement | P0 | 不写成论文综述 |
| `physics-judgement/CONCLUSION_REFERENCE_BOOK.md` | Physics judgement | 可升级为 canonical conclusion pack | Authoritative Literature Loop; Source Map | 结论、来源类型、支撑文献、需全文核验 | E. Physics Judgement | P2 | 不堆 DOI |
| `physics-judgement/numerical-vs-model-error.md` | Physics judgement | 可补误差分类总框架 | Result Credibility Blueprint; Parameter Blueprint | numerical/model/boundary/postprocess/workflow propagation | E. Physics Judgement | P1 | 不把加密参数当模型修复 |
| `physics-judgement/pseudopotential-transferability-and-functional-consistency.md` | Physics judgement | 可补 PP transferability 和 functional consistency | Parameter Blueprint; Source Map | PP choice、UPF、functional matching、cutoff recalc | E. Physics Judgement | P1 | 不把 PP 可用性写成无条件 |
| `physics-judgement/band-gap-problem-and-delocalization.md` | Physics judgement | 可补 derivative discontinuity 和 delocalization risk | Functional Blueprint; Literature Loop | KS gap、SIE、PDOS、hybrid/GW boundary | E. Physics Judgement | P1 | 不把 kmesh 修成 gap problem |
| `physics-judgement/kmesh-smearing-sensitivity.md` | Physics judgement | 可补 metal/Fermi surface/EPC sensitivity | Parameter Blueprint; Metals/Smearing Blueprint | kmesh、smearing、DOS、phonon/EPC | E. Physics Judgement | P1 | 不给固定 degauss |
| `physics-judgement/imaginary-frequency-triage.md` | Physics judgement | 可补虚频三分法和 ASR 边界 | DFPT Brief; Output Evidence Review | 数值误差、结构未优化、真实不稳定 | E. Physics Judgement | P1 | 不把虚频直接定性 |
| `physics-judgement/u-value-provenance-and-boundary.md` | Physics judgement | 可补 U 来源和 hp.x 入口 | Literature Loop; Parameter Blueprint | U provenance、HUBBARD、linear response、model change | E. Physics Judgement | P1 | 不用 U 拟合 gap 后不记录 |
| `physics-judgement/soc-and-symmetry-boundary.md` | Physics judgement | 可补 relativistic PP 和 symmetry/output review | Parameter Blueprint; Literature Loop | `noncolin`、`lspinorb`、symmetry、bands | E. Physics Judgement | P2 | 不把 SOC 当开关 |
| `physics-judgement/vdw-and-low-dimensional-boundary.md` | Physics judgement | 可补 vdW model choice 与 low-dimensional boundary | Functional Blueprint; Literature Loop | `vdw_corr`、structure propagation、vacuum | E. Physics Judgement | P2 | 不展开结构构建 |
| `physics-judgement/work-function-and-electrostatic-boundary.md` | Physics judgement | 可补 electrostatic plateau 和 dipole correction | Work Function Boundary; Output Evidence Review | vacuum level、Fermi level、potential average、uncertainty | E. Physics Judgement | P1 | 不写单行公式 |
| `physics-judgement/wannier-validation-and-window-choice.md` | Physics judgement | 可补 QE bands 回对和 window 记录 | Wannier/EPC Blueprint; Literature Loop | projection、window、spread、band validation | E. Physics Judgement | P2 | spread 不是唯一质量证据 |
| `physics-judgement/epc-data-chain-and-convergence.md` | Physics judgement | 可补 data chain 和 convergence hierarchy | EPC Blueprint; Literature Loop | DFPT、Wannier、dense k/q、observable | E. Physics Judgement | P2 | 不只看 lambda/Tc |
| `physics-judgement/ground-state-vs-excited-state.md` | Physics judgement | 可补 GW/BSE/TDDFT 边界 | Literature Loop | KS eigenvalue vs excited state observable | E. Physics Judgement | P2 | 不把 ordinary DFT bands 当光谱 |
| `physics-judgement/energy-vs-free-energy.md` | Physics judgement | 可补 total energy/free energy/MD/NEB 边界 | Literature Loop | 0 K energy、phonon free energy、MD sampling、NEB | E. Physics Judgement | P2 | 不把 MEP 写成 free-energy path |
| `physics-judgement/uncertainty-statement-template.md` | Physics judgement | 可补可复用 uncertainty statement | Result Credibility Blueprint; Output Evidence Review | numerical/model/PP/finite-size/workflow uncertainty | E. Physics Judgement | P1 | 不写空泛免责声明 |
| `references/README.md` | Source map | 可补来源分类和阅读方式 | Source Map; Literature Loop | official docs、canonical literature、tutorials、tools | G. Source Map and Literature | P2 | 不堆链接 |
| `references/source-index.md` | Source map | 可清洗来源用途和版本敏感说明 | Source Map; Parameter Blueprint | official docs、INPUT_*、tool docs、tutorials | G. Source Map and Literature | P1 | 去掉 tracking URL |
| `references/canonical-literature.md` | Literature guide | 可接入 A0/A1/A2/B/C 分级 | Authoritative Literature Loop | canonical source spine、topic mapping、claim support | G. Source Map and Literature | P1 | 不无限扩 DOI |
| `references/reading-maintenance-policy.md` | Source map | 可补 source freshness 和 version-sensitive 规则 | Source Map; Literature Loop | 维护节奏、来源类型、核验标准 | G. Source Map and Literature | P2 | 不写成自动化流程 |
| `references/canonical.bib` | Literature guide | 若存在或后续新增，应从 loop 中去重维护 | Authoritative Literature Loop | BibTeX 候选、canonical set | G. Source Map and Literature | P3 | 本轮不必强制创建 |
| `standards/README.md` | Standard / QA | 可补 QA 总入口与 backfill gate | Output Evidence Review; Source Map | 文件命名、记录、output review、source policy | H. Standards and QA | P0 | 不写成行政流程 |
| `standards/output-review-checklist.md` | Output evidence review | 可按 evidence item 增补“能证明/不能证明” | Output Evidence Review | `JOB DONE`、SCF、NSCF、relax、phonon、warnings | F. Output Evidence Review | P1 | 不把单一证据过度解释 |
| `standards/pass-warn-block.md` | Standard / QA | 可补主题级例子和下游准入 | Output Evidence Review; Result Credibility Blueprint | PASS/WARN/BLOCK semantics、downstream allowed | H. Standards and QA | P1 | 术语必须全库一致 |
| `standards/calculation-record-template.md` | Standard / QA | 可补 uncertainty、source boundary、file chain | Output Evidence Review; Source Map | command、environment、prefix/outdir、input/output evidence | H. Standards and QA | P1 | 不要求仓库保存具体 output |
| `standards/citation-and-source-policy.md` | Standard / QA | 可补来源强度和 `.docx` 参考边界 | Source Map; Literature Loop | official/source/canonical/tutorial/tool 分级 | G. Source Map and Literature | P1 | 不把中间调研文档当正文来源 |
| `standards/input-file-naming.md` | Standard / QA | 可补文件名与 `prefix/outdir` 区别 | Parameter Blueprint | program/workflow/system naming、scratch boundary | H. Standards and QA | P2 | 不把文件名当数据链唯一依据 |
| `standards/project-layout.md` | Standard / QA | 可补个人项目记录与仓库结构边界 | Output Evidence Review | structures、pseudo、inputs、outputs、records | H. Standards and QA | P3 | 不创建案例目录 |
