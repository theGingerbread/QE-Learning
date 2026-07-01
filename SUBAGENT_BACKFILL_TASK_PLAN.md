# Subagent Backfill Task Plan

本文件把 Deep Research 参考材料转化为可派发给 subagent 的后续任务。每个任务只回填目标文件，不改变目录哲学，不引入具体材料案例，不写万能参数，不把研究中间文档当作正文权威来源。

## 全局约束

- 写作语言：中文。
- 风格：参考手册风格，服务 QE input/output 阅读、workflow 判断和 DFT 可靠性审查。
- 来源：正文稳定结论必须回到 QE 官方文档、`INPUT_*` reference、官方 guide、canonical literature 或官方工具文档。
- 参数：不写固定材料参数答案；参数必须映射到 output review 和目标 observable。
- 证据：workflow 页面必须包含 output review 和下游准入。
- 判断：physics-judgement 页面必须包含数值误差、模型误差、边界误差或 workflow 传播误差的区分。
- 边界：自动化工具只作为高级参考，不替代 QE 原生命令行学习。

## A. Learn Path Refinement Subagent

### Task ID: A1

### Target files

- `README.md`
- `learn/README.md`
- `learn/00-start-here.md`

### Reference docs to use

- Deep Research Review of the QE-Learning Learn Landing Page.docx
- Deep Research Template for QE Output Evidence Review.docx
- DFT and Quantum ESPRESSO Result Credibility Judgement Blueprint.docx

### Goal

把入口页强化为“QE 参考手册 + DFT 知识体系”的稳定入口，让读者知道学习路径按能力目标、完成判据和可验证 output 证据推进。

### Required research

- 核对现有 README 和 `learn/` 入口是否已经说明五个目录职责。
- 从 Learn Landing Page Review 中提取能力目标、完成判据、可验证输出和常见误区。
- 从 Output Evidence Review 中提取 `JOB DONE` 边界、output review 和下游准入写法。

### Required backfill structure

- `README.md` 保持短入口，只补必要一句或一小段。
- `learn/README.md` 保留页面表格，补“如何与 workflows/standards 配合阅读”。
- `learn/00-start-here.md` 补“跑通不等于可信”的 output evidence 链。

### Must include

- 能力目标。
- 完成判据。
- 可验证输出。
- `PASS / WARN / BLOCK`。
- 下游准入。

### Must not include

- 时间计划。
- 具体材料案例。
- 具体 input/output 文件。
- 外部自动化执行系统说明。

### Acceptance criteria

- 新读者能从入口页判断先读什么、为什么读 output、如何决定进入下游。
- 入口页不变成长教程。

### Suggested commit scope

`Refine QE-Learning entry and learn path evidence gates`

### Task ID: A2

### Target files

- `learn/01-qe-workflow-map.md`
- `learn/02-first-scf-loop.md`
- `learn/03-convergence-loop.md`
- `learn/04-relaxation-loop.md`
- `learn/05-electronic-structure-loop.md`
- `learn/06-phonon-dfpt-loop.md`
- `learn/07-postprocessing-loop.md`
- `learn/08-hpc-and-reproducibility.md`
- `learn/09-feature-expansion-map.md`

### Reference docs to use

- QE Workflow Reference Upgrade for QE-Learning.docx
- Quantum ESPRESSO Parameter Deep Research Blueprint for QE-Learning.docx
- Deep Research Template for QE Output Evidence Review.docx
- DFT and Quantum ESPRESSO Result Credibility Judgement Blueprint.docx

### Goal

把 `learn/` 的每个阶段与具体 workflow、参数角色、output evidence 和下游准入对应起来。

### Required research

- 提取 QE 程序链和 `prefix/outdir` 数据边。
- 提取 convergence、relax、electronic、phonon、post-processing 的能力门槛。
- 核对 `learn/` 中是否存在空泛“应检查”表述，并替换为可审阅证据。

### Required backfill structure

- 每页补一组“必读 output 证据”。
- 每页补一组“进入下游前的完成判据”。
- 每页链接对应 workflow 和 standards 页面。

### Must include

- output review。
- 下游准入。
- 与 `standards/output-review-checklist.md` 的关系。
- 对具体材料案例的边界说明。

### Must not include

- 固定体系、固定参数、固定日期安排。
- 大段外部链接。

### Acceptance criteria

- 读完 `learn/` 能画出 QE workflow，并知道每一步何时 `PASS / WARN / BLOCK`。

### Suggested commit scope

`Backfill learn path with workflow evidence gates`

## B. Workflow Reference Upgrade Subagent

### Task ID: B1

### Target files

- `workflows/README.md`
- `workflows/ground-state/scf.md`
- `workflows/ground-state/nscf.md`
- `workflows/ground-state/cutoff-convergence.md`
- `workflows/ground-state/kpoint-convergence.md`
- `workflows/ground-state/smearing-and-occupations.md`
- `workflows/ground-state/relax.md`
- `workflows/ground-state/vc-relax.md`

### Reference docs to use

- QE Workflow Reference Upgrade for QE-Learning.docx
- Quantum ESPRESSO Parameter Deep Research Blueprint for QE-Learning.docx
- Deep Research Template for QE Output Evidence Review.docx

### Goal

把 ground-state workflow 页面升级为可复查的 QE 原生命令行参考手册。

### Required research

- 核对 `INPUT_PW` 中相关 namelist/card：`CONTROL`、`SYSTEM`、`ELECTRONS`、`IONS`、`CELL`、`ATOMIC_SPECIES`、`K_POINTS`、`CELL_PARAMETERS`。
- 核对 output evidence：SCF 收敛、estimated accuracy、pseudopotential loading、cutoff、k-points、forces、stress、warnings。
- 区分 numerical convergence、model choice 和 file-chain parameter。

### Required backfill structure

每页至少包含：

1. 计算目标。
2. 上游依赖。
3. QE 程序链。
4. 关键 input 字段。
5. output review。
6. 收敛要求。
7. `PASS / WARN / BLOCK`。
8. 常见误区。
9. 下游影响。
10. 来源与版本边界。

### Must include

- `prefix/outdir` 数据边。
- `ecutwfc/ecutrho` 与赝势类型关系。
- kmesh 与 k-path 区别。
- smearing 对 energy/force/DOS/phonon 的影响。
- relax/vc-relax 后 final static SCF 的下游准入。

### Must not include

- 具体材料参数。
- “固定 cutoff/kmesh 足够”的说法。
- 把 `JOB DONE` 写成 PASS。

### Acceptance criteria

- 每个 ground-state 页面都能回答“这个 output 是否允许进入下游”。
- 每个页面都能指导读者从 output 中摘录证据。

### Suggested commit scope

`Upgrade ground-state workflows with output evidence review`

### Task ID: B2

### Target files

- `workflows/electronic/bands.md`
- `workflows/electronic/dos.md`
- `workflows/electronic/pdos.md`
- `workflows/electronic/charge-density.md`
- `workflows/electronic/electrostatic-potential.md`
- `workflows/electronic/elf.md`
- `workflows/electronic/work-function.md`
- `workflows/electronic/fermi-surface.md`

### Reference docs to use

- QE Workflow Reference Upgrade for QE-Learning.docx
- DFT and Quantum ESPRESSO Result Credibility Judgement Blueprint.docx
- Deep Research Template for QE Output Evidence Review.docx

### Goal

把 electronic workflow 页面升级为电子结构和后处理参考手册，强调 KS eigenvalue、DOS/PDOS、后处理和 work function 的解释边界。

### Required research

- 核对 `INPUT_BANDS`、`INPUT_DOS`、`INPUT_PROJWFC`、`INPUT_PP`。
- 核对 PostProc 文档中 `pp.x`、`average.x`、`fs.x` 的入口和限制。
- 核对 bands/DOS/PDOS 的 output review 能证明什么，不能证明什么。

### Required backfill structure

- 每页补“上游状态必须是什么”。
- 每页补“output 中要摘录哪些证据”。
- 每页补“下游允许进入哪些解释，禁止哪些过度结论”。

### Must include

- `SCF -> bands -> bands.x` 与 `SCF -> NSCF -> dos.x/projwfc.x` 区别。
- k-path 与 uniform dense kmesh 区别。
- Fermi reference、energy zero、broadening、PDOS projection 边界。
- work function 的 potential plateau、vacuum level、Fermi level 和 uncertainty。

### Must not include

- 把普通 bands 当实验光谱。
- 把 PDOS 当精确电荷分解。
- 把 work function 写成无条件单行公式。

### Acceptance criteria

- 每个 electronic 页面都有 output review 和解释边界。
- 读者能判断 bands/DOS/PDOS 是否相互一致。

### Suggested commit scope

`Upgrade electronic workflows with interpretation boundaries`

### Task ID: B3

### Target files

- `workflows/phonon/gamma-phonon.md`
- `workflows/phonon/phonon-dispersion-dfpt.md`
- `workflows/phonon/phonon-dos.md`
- `workflows/phonon/dielectric-born-effective-charge.md`
- `workflows/phonon/ir-raman.md`
- `workflows/phonon/phonon-debugging.md`

### Reference docs to use

- QE Workflow Reference Upgrade for QE-Learning.docx
- QE Theory Minimum Research Brief for an Unresolved Topic Slot.docx
- Deep Research Template for QE Output Evidence Review.docx
- DFT and Quantum ESPRESSO Result Credibility Judgement Blueprint.docx

### Goal

把 phonon workflow 页面升级为 DFPT response workflow 参考手册。

### Required research

- 核对 `INPUT_PH`、`INPUT_Q2R`、`INPUT_MATDYN`、`INPUT_DYNMAT` 和 PHonon user guide。
- 核对 `epsil`、`tr2_ph`、`ldisp`、`nq1/nq2/nq3`、`fildyn`、`asr/zasr`。
- 提取虚频、ASR、Born charge、dielectric tensor、LO-TO splitting 的 output review。

### Required backfill structure

- 每页写清程序链和文件链。
- 每页写清 output review 证据。
- 每页写清 `PASS / WARN / BLOCK`。

### Must include

- Gamma phonon 与 q-grid phonon 区别。
- `ph.x -> q2r.x -> matdyn.x` 的 dyn/fc/freq 文件关系。
- 虚频三分法：数值误差、结构未充分优化、真实动力学不稳定。
- ASR 的作用和不能替代收敛的边界。
- metal/insulator 条件下 dielectric/Born 分支边界。

### Must not include

- 把 phonon 写成普通后处理。
- 把虚频直接等同真实不稳定。
- 把 ASR 写成修复收敛的手段。

### Acceptance criteria

- phonon 页面能支持下游准入和异常诊断。

### Suggested commit scope

`Upgrade phonon workflows with DFPT evidence gates`

### Task ID: B4

### Target files

- `workflows/advanced/*.md`

### Reference docs to use

- QE Workflow Reference Upgrade for QE-Learning.docx
- Authoritative Literature Loop for QE and DFT Physical Judgement.docx
- Authoritative Literature Loop for QE _ DFT Physical Judgement.docx

### Goal

把 advanced workflow 页面保持为边界页，但补足输入字段、output review、风险和官方入口。

### Required research

- 核对相关官方文档入口：DFT+U、SOC、hybrid、MD、NEB、Wannier90、EPW、pseudopotential generation。
- 从 literature loop 中提取 advanced method 的物理边界。

### Required backfill structure

- 适用问题。
- 进入前必须掌握什么。
- 关键 QE 程序或输入字段。
- output review 要点。
- 常见风险。
- 与基础 workflow 的关系。
- 资料来源。

### Must include

- U provenance。
- fully relativistic pseudopotential 与 SOC。
- vdW 模型选择。
- Wannier bands 回对。
- EPC 完整数据链。

### Must not include

- 完整专题教程。
- 具体材料推荐。
- “高级方法一定更准”的表述。

### Acceptance criteria

- 高级页至少达到边界页标准：知道什么时候进入、查什么官方文档、看什么 output、哪些结论不能下。

### Suggested commit scope

`Refine advanced workflow boundary pages`

## C. Parameter Deep Research Subagent

### Task ID: C1

### Target files

- `workflows/ground-state/scf.md`
- `workflows/ground-state/nscf.md`
- `workflows/ground-state/cutoff-convergence.md`
- `workflows/ground-state/kpoint-convergence.md`
- `workflows/ground-state/smearing-and-occupations.md`
- `standards/output-review-checklist.md`

### Reference docs to use

- Quantum ESPRESSO Parameter Deep Research Blueprint for QE-Learning.docx
- Deep Research Template for QE Output Evidence Review.docx

### Goal

补强基础参数的官方定义、参数类型、output 映射和误用边界。

### Required research

- 查 QE 官方 `INPUT_PW`。
- 对 `ecutwfc`、`ecutrho`、`K_POINTS`、`occupations`、`smearing`、`degauss`、`nbnd`、`conv_thr`、`mixing_beta`、`prefix/outdir` 建立参数条目。

### Required backfill structure

每个参数说明应包含：

- 官方字段位置。
- 参数类型：物理模型、数值收敛、文件链、后处理设置。
- 影响的 observable。
- output 中如何验证。
- 常见误用。
- 下游影响。

### Must include

- `ecutrho` 与赝势类型关系。
- `K_POINTS automatic` 与 high-symmetry path 区别。
- smearing 与 metal/insulator 边界。
- `prefix/outdir` 与文件名区别。

### Must not include

- 固定参数推荐。
- 未查官方文档的字段定义。

### Acceptance criteria

- 每个参数都能映射到 output review。

### Suggested commit scope

`Backfill core QE parameter review entries`

### Task ID: C2

### Target files

- `workflows/advanced/dft-plus-u.md`
- `workflows/advanced/noncollinear-soc.md`
- `workflows/advanced/vdW-corrections.md`
- `workflows/advanced/hybrid-functional-overview.md`
- `workflows/phonon/gamma-phonon.md`
- `workflows/phonon/phonon-dispersion-dfpt.md`

### Reference docs to use

- Quantum ESPRESSO Parameter Deep Research Blueprint for QE-Learning.docx
- Authoritative Literature Loop for QE and DFT Physical Judgement.docx
- Authoritative Literature Loop for QE _ DFT Physical Judgement.docx

### Goal

补强高级和 DFPT 字段的版本敏感性、模型边界和 output review。

### Required research

- 查 QE 官方 `INPUT_PW`、`INPUT_PH`、`INPUT_HP`。
- 核对 `input_dft`、`HUBBARD`、`noncolin`、`lspinorb`、`vdw_corr`、`tr2_ph`、`epsil`、`ldisp`、`nq1/nq2/nq3`。

### Required backfill structure

- 字段官方入口。
- 模型选择含义。
- 版本敏感说明。
- output review。
- 不可过度解释的结论。

### Must include

- DFT+U U 值来源记录。
- SOC 需要相对论赝势边界。
- vdW 模型选择改变结构与下游。
- phonon response threshold 与 SCF/结构质量关系。

### Must not include

- 把高级参数写成基础默认设置。
- 把模型选择写成数值收敛调参。

### Acceptance criteria

- 高级参数说明有来源、边界和 output 映射。

### Suggested commit scope

`Backfill advanced QE parameter boundaries`

## D. Theory Minimum Subagent

### Task ID: D1

### Target files

- `theory-minimum/README.md`
- `theory-minimum/dft-ks-scf.md`
- `theory-minimum/plane-wave-cutoff.md`
- `theory-minimum/pseudopotentials.md`
- `theory-minimum/kpoints-symmetry-kpath.md`
- `theory-minimum/smearing-metals.md`

### Reference docs to use

- QE Theory Minimum Research Brief for an Unresolved Topic Slot.docx
- Quantum ESPRESSO Parameter Deep Research Blueprint for QE-Learning.docx
- QE Learning Source Map for Quantum ESPRESSO.docx

### Goal

把最低理论页补成 QE input/output 可回查层。

### Required research

- 核对 DFT、Kohn-Sham、plane-wave、pseudopotential、Monkhorst-Pack、smearing 相关 canonical sources。
- 核对 QE `INPUT_PW` 中对应字段。

### Required backfill structure

每页包含：

- QE 中对应的问题。
- 输入字段。
- output review。
- 常见错误。
- 最低掌握深度。
- 对应 workflow。
- 资料来源。

### Must include

- total energy 与 eigenvalue 解释边界。
- cutoff 与 basis convergence。
- PP 来源、泛函一致性、UPF 元信息。
- uniform kmesh 与 high-symmetry path 区别。
- smearing 对金属和小带隙体系的边界。

### Must not include

- 长篇推导。
- 固定材料例子。
- 无来源经验判断。

### Acceptance criteria

- 每个理论概念都能落到 QE input/output/workflow。

### Suggested commit scope

`Refine theory minimum foundations for QE input output review`

### Task ID: D2

### Target files

- `theory-minimum/force-stress-relaxation.md`
- `theory-minimum/magnetism-soc-dftu.md`
- `theory-minimum/dfpt-phonons.md`
- `theory-minimum/dielectric-born-charge.md`
- `theory-minimum/functional-choice.md`

### Reference docs to use

- QE Theory Minimum Research Brief for an Unresolved Topic Slot.docx
- DFT and Quantum ESPRESSO Result Credibility Judgement Blueprint.docx
- Authoritative Literature Loop for QE and DFT Physical Judgement.docx

### Goal

补强结构、DFPT、磁性、SOC、DFT+U 和 functional choice 的最低理论边界。

### Required research

- 核对 QE `INPUT_PW`、`INPUT_PH`。
- 核对 DFPT、Born charge、DFT+U、SOC 和 exchange-correlation functional 的 canonical sources。

### Required backfill structure

- 每页补“哪些问题属于 theory-minimum，哪些应进入 physics-judgement”。
- 每页补 output evidence 和常见误读。

### Must include

- relax/vc-relax 后 static SCF。
- phonon 对 SCF/结构/收敛更敏感。
- `epsil` 与 insulator condition。
- U/SOC/vdW 属于模型选择。

### Must not include

- 把理论页扩写成专题综述。

### Acceptance criteria

- theory-minimum 与 physics-judgement 分工清楚。

### Suggested commit scope

`Refine theory minimum response and model-boundary pages`

## E. Physics Judgement Subagent

### Task ID: E1

### Target files

- `physics-judgement/README.md`
- `physics-judgement/numerical-vs-model-error.md`
- `physics-judgement/dft-ground-state-boundary.md`
- `physics-judgement/kohn-sham-eigenvalue-boundary.md`
- `physics-judgement/functional-choice-and-sensitivity.md`
- `physics-judgement/band-gap-problem-and-delocalization.md`

### Reference docs to use

- DFT and Quantum ESPRESSO Result Credibility Judgement Blueprint.docx
- Authoritative Literature Loop for QE and DFT Physical Judgement.docx
- Authoritative Literature Loop for QE _ DFT Physical Judgement.docx

### Goal

把 ground-state boundary、KS eigenvalue boundary、functional choice 和 band gap problem 写成可用于科研判断的参考页。

### Required research

- 核对 HK、KS、exchange-correlation ladder、self-interaction、delocalization error、derivative discontinuity 的 canonical sources。
- 核对相关 QE 字段如 `input_dft`、hybrid 字段和 output evidence。

### Required backfill structure

每页必须包含：

- 核心判断结论。
- 问题来源。
- 相关 QE input 字段。
- output review 迹象。
- `PASS / WARN / BLOCK`。
- 常见误区。
- 回写到哪些 workflow/theory 页面。
- 资料来源和结论强度。

### Must include

- total energy/density/force/stress 与 eigenvalue/spectroscopy 的可信度层级。
- band gap problem 不是 kmesh 问题。
- 更高阶泛函不自动保证所有性质更准。

### Must not include

- 把普通 DFT bands 当实验光谱。
- 把 hybrid 或 meta-GGA 写成普适提升。

### Acceptance criteria

- 页面能帮助读者避免“算出来但解释错”。

### Suggested commit scope

`Backfill physics judgement foundations and band-gap boundaries`

### Task ID: E2

### Target files

- `physics-judgement/pseudopotential-transferability-and-functional-consistency.md`
- `physics-judgement/kmesh-smearing-sensitivity.md`
- `physics-judgement/relax-is-not-final-electronic-structure.md`
- `physics-judgement/imaginary-frequency-triage.md`
- `physics-judgement/u-value-provenance-and-boundary.md`
- `physics-judgement/soc-and-symmetry-boundary.md`
- `physics-judgement/vdw-and-low-dimensional-boundary.md`

### Reference docs to use

- Quantum ESPRESSO Parameter Deep Research Blueprint for QE-Learning.docx
- DFT and Quantum ESPRESSO Result Credibility Judgement Blueprint.docx
- Authoritative Literature Loop for QE and DFT Physical Judgement.docx

### Goal

把最影响科研可靠性的误差来源和模型边界写成可审阅判断页。

### Required research

- 核对 PP、kmesh/smearing、DFPT phonon、DFT+U、SOC、vdW 的 canonical sources 和 QE 官方字段。

### Required backfill structure

- 数值误差 vs 模型误差。
- output evidence。
- `PASS / WARN / BLOCK`。
- 不能做出的过度结论。

### Must include

- 换赝势需要重新审阅 cutoff、kmesh 和结果。
- 金属和 EPC 对 kmesh/smearing 敏感。
- relax/vc-relax 后需要 final static SCF 承接下游。
- 虚频三分法。
- U provenance。
- SOC 与相对论赝势、symmetry。
- vdW 对结构和下游的传播影响。

### Must not include

- 普适 U 值。
- 普适 vdW 模型推荐。
- 固定 smearing 宽度。

### Acceptance criteria

- 每页能给出可执行的判断边界和回查动作。

### Suggested commit scope

`Backfill physics judgement error triage pages`

### Task ID: E3

### Target files

- `physics-judgement/work-function-and-electrostatic-boundary.md`
- `physics-judgement/wannier-validation-and-window-choice.md`
- `physics-judgement/epc-data-chain-and-convergence.md`
- `physics-judgement/ground-state-vs-excited-state.md`
- `physics-judgement/energy-vs-free-energy.md`
- `physics-judgement/uncertainty-statement-template.md`

### Reference docs to use

- DFT and Quantum ESPRESSO Result Credibility Judgement Blueprint.docx
- Authoritative Literature Loop for QE and DFT Physical Judgement.docx
- Authoritative Literature Loop for QE _ DFT Physical Judgement.docx

### Goal

补强高级物理判断数据链和 uncertainty statement。

### Required research

- 核对 work function electrostatics、Wannier90、EPW、GW/BSE、MD/NEB/free energy、reproducibility sources。

### Required backfill structure

- 现象。
- 可能原因。
- output evidence。
- 数据链。
- `PASS / WARN / BLOCK`。
- uncertainty statement 模板。

### Must include

- work function 不只是 `E_vac - E_F`。
- Wannier bands 必须回对 QE bands。
- EPC 不能只看单一汇总量。
- ground-state DFT 不自动给出 excited-state observable。
- NEB 默认是 minimum-energy path 语境，不等同 free-energy path。
- DFT 结果必须说明 numerical/model/PP/finite-size/workflow uncertainty。

### Must not include

- 完整高级方法教程。
- 具体材料案例。

### Acceptance criteria

- 高级判断页能作为“何时需要更高级方法或更严格证据”的审阅框架。

### Suggested commit scope

`Backfill advanced physics judgement and uncertainty templates`

## F. Output Evidence Review Subagent

### Task ID: F1

### Target files

- `standards/output-review-checklist.md`
- `standards/pass-warn-block.md`
- `standards/calculation-record-template.md`

### Reference docs to use

- Deep Research Template for QE Output Evidence Review.docx
- DFT and Quantum ESPRESSO Result Credibility Judgement Blueprint.docx

### Goal

把 output evidence review 写成全仓库可复用的审阅标准。

### Required research

- 从 output evidence template 中提取证据项：`JOB DONE`、SCF convergence、estimated accuracy、total energy、Fermi energy、forces、stress、warnings、symmetry、irreducible k-points、phonon frequency、ph.x convergence、q2r/matdyn 文件链。
- 核对 QE 官方文档中这些 output 的程序语境。

### Required backfill structure

每个 evidence item 包含：

- 出现位置。
- 能证明什么。
- 不能证明什么。
- WARN/BLOCK 触发条件。
- 需要回查的 input 或上游状态。
- 允许进入的下游。

### Must include

- `JOB DONE` 只能证明程序正常结束。
- `convergence has been achieved` 必须说明是哪一类收敛。
- output review 必须服务下游准入。

### Must not include

- 把单个 output 行当作完整科学结论。

### Acceptance criteria

- standards 中的 output review 可被所有 workflow 页面引用。

### Suggested commit scope

`Strengthen output evidence review standards`

### Task ID: F2

### Target files

- `workflows/ground-state/*.md`
- `workflows/electronic/*.md`
- `workflows/phonon/*.md`

### Reference docs to use

- Deep Research Template for QE Output Evidence Review.docx
- QE Workflow Reference Upgrade for QE-Learning.docx

### Goal

把 standards 中的 output evidence 条目回填到各 workflow 页面。

### Required research

- 对照每个 workflow 的程序和 output。
- 避免通用套话，写成 workflow-specific review。

### Required backfill structure

- output review 小节中的每个 bullet 都应能对应程序 output 或生成文件。
- 每页给出 `PASS / WARN / BLOCK` 进入下游的条件。

### Must include

- SCF、NSCF、relax、vc-relax、bands、DOS、PDOS、pp.x、phonon 的差异化审阅。

### Must not include

- 复制同一段通用审阅文字到所有页面。

### Acceptance criteria

- workflow 页面可独立指导 output 审阅。

### Suggested commit scope

`Propagate output evidence review into workflows`

## G. Source Map and Literature Subagent

### Task ID: G1

### Target files

- `references/source-index.md`
- `references/README.md`
- `standards/citation-and-source-policy.md`

### Reference docs to use

- QE Learning Source Map for Quantum ESPRESSO.docx
- Quantum ESPRESSO Parameter Deep Research Blueprint for QE-Learning.docx

### Goal

把来源索引升级为“来源支持什么判断”的导读，而不是链接清单。

### Required research

- 清洗链接，去除跟踪参数。
- 将来源分成官方文档、官方 examples、QE papers、canonical literature、tutorial websites、auxiliary tools、version-sensitive docs。

### Required backfill structure

- 每个来源说明用途。
- 每个来源标注对应仓库页面。
- 参数定义必须优先官方 `INPUT_*`。

### Must include

- `INPUT_PW`、`INPUT_PH`、`INPUT_PP`、`INPUT_DOS`、`INPUT_PROJWFC`、`INPUT_Q2R`、`INPUT_MATDYN`。
- QE official docs、PHonon user guide、PostProc guide。
- tutorial sources 的用途边界。

### Must not include

- 未说明用途的 DOI 或 URL 堆叠。
- 用工具流行度判断科学价值。

### Acceptance criteria

- 用户能从来源页知道某链接支持哪个判断。

### Suggested commit scope

`Clarify source index purposes and source policy`

### Task ID: G2

### Target files

- `references/canonical-literature.md`
- `references/reading-maintenance-policy.md`
- `physics-judgement/CONCLUSION_REFERENCE_BOOK.md`

### Reference docs to use

- Authoritative Literature Loop for QE and DFT Physical Judgement.docx
- Authoritative Literature Loop for QE _ DFT Physical Judgement.docx

### Goal

建立 canonical literature spine 和结论来源映射。

### Required research

- 合并两个 literature loop 文档，按主题去重。
- 建立 A0/A1/A2/B1/B2/C 或等价来源层级。
- 标注 stable、version-sensitive、boundary。

### Required backfill structure

- Fast Core Loop。
- Workflow-Oriented Loop。
- Frontier Entry Loop。
- Topic-by-topic source map。
- Conclusion reference table。

### Must include

- 每个来源支持什么判断。
- 哪些判断需要全文核验。
- 哪些来源只能作为高级入口。

### Must not include

- 无边界 DOI 列表。
- 摘要级结论冒充全文核验。

### Acceptance criteria

- canonical source 能支撑 physics-judgement 和 theory-minimum。

### Suggested commit scope

`Consolidate canonical literature spine for physics judgement`

## H. Standards and QA Subagent

### Task ID: H1

### Target files

- `standards/README.md`
- `standards/input-file-naming.md`
- `standards/project-layout.md`
- `standards/calculation-record-template.md`
- `standards/pass-warn-block.md`
- `standards/output-review-checklist.md`
- `standards/citation-and-source-policy.md`

### Reference docs to use

- Deep Research Template for QE Output Evidence Review.docx
- QE Learning Source Map for Quantum ESPRESSO.docx
- DFT and Quantum ESPRESSO Result Credibility Judgement Blueprint.docx

### Goal

统一记录、命名、审阅、来源和 QA 标准。

### Required research

- 检查 standards 是否与 workflow 和 physics judgement 术语一致。
- 检查 calculation record 是否能记录 input/output/source/uncertainty/downstream。

### Required backfill structure

- 文件命名。
- calculation record。
- output review。
- PASS/WARN/BLOCK。
- source policy。
- QA checklist。

### Must include

- `prefix/outdir` 与文件名区别。
- `JOB DONE` 与 PASS 区别。
- uncertainty statement。
- source boundary。

### Must not include

- 要求仓库保存具体材料 input/output。
- 外部自动化系统执行规范。

### Acceptance criteria

- standards 可直接用于个人科研计算记录和仓库文档审查。

### Suggested commit scope

`Align standards for records output review and source policy`

### Task ID: H2

### Target files

- 全仓库 Markdown 文件。

### Reference docs to use

- 本任务计划。
- `standards/citation-and-source-policy.md`
- `standards/output-review-checklist.md`

### Goal

做最终 QA，确保回填后仓库仍是 QE 参考手册和 DFT 知识体系。

### Required research

- 检查目录结构。
- 检查 Markdown 链接。
- 检查私有路径。
- 检查材料绑定内容。
- 检查无来源断言。
- 检查术语一致性。

### Required backfill structure

输出 QA 报告，列出：

- 检查命令。
- 结果。
- 修复项。
- 残留人工复查项。

### Must include

- `git diff --check`。
- 本地链接检查。
- source section 检查。
- README 与目录索引一致性检查。

### Must not include

- 大规模正文重写。

### Acceptance criteria

- 回填分支可审查、可合并、无格式错误。

### Suggested commit scope

`Run final QA for deep research backfill`
