# Project Reference Intake

本文件记录 Deep Research 参考文档的读取状态、主题去重和可回填方向。这里的参考文档是研究中间成果，用于规划后续回填；仓库正文中的稳定结论仍应追溯到 QE 官方文档、`INPUT_*` reference、QE 论文、DFT/DFPT/Wannier/EPW/GW/BSE/reproducibility 等 canonical literature，以及官方工具文档。

## 读取总览

| 文档名 | 是否存在 | 是否成功读取 | 段落数 | 表格数 | 主要用途 | 去重判断 |
|---|---:|---:|---:|---:|---|---|
| Quantum ESPRESSO Parameter Deep Research Blueprint for QE-Learning.docx | 是 | 是 | 59 | 0 | QE 参数定义、参数分类、output review、PASS/WARN/BLOCK | 独立 |
| QE Workflow Reference Upgrade for QE-Learning.docx | 是 | 是 | 203 | 0 | workflow 页面升级、程序链、输入字段、输出审阅 | 独立 |
| QE Theory Minimum Research Brief for an Unresolved Topic Slot.docx | 是 | 是 | 68 | 1 | `theory-minimum/` 最低理论补强 | 独立 |
| QE Learning Source Map for Quantum ESPRESSO.docx | 是 | 是 | 96 | 2 | 来源分级、source map、canonical source 入口 | 独立 |
| DFT and Quantum ESPRESSO Result Credibility Judgement Blueprint.docx | 是 | 是 | 86 | 0 | `physics-judgement/` 可信度判断框架 | 独立 |
| Deep Research Template for QE Output Evidence Review.docx | 是 | 是 | 71 | 1 | output evidence review、`JOB DONE` 边界、下游准入 | 独立 |
| Deep Research Review of the QE-Learning Learn Landing Page.docx | 是 | 是 | 46 | 2 | `learn/` 入口、能力目标、完成判据 | 独立 |
| Authoritative Literature Loop for QE and DFT Physical Judgement.docx | 是 | 是 | 163 | 9 | canonical literature spine、reading loops、物理判断主题矩阵 | 与下一份主题重复、内容互补 |
| Authoritative Literature Loop for QE _ DFT Physical Judgement.docx | 是 | 是 | 193 | 15 | canonical literature spine、topic matrix、工具与高级主题入口 | 与上一份主题重复、内容互补 |

两个 Authoritative Literature Loop 文档不是逐字重复：标题和核心主题高度相近，但表格数量、链接集合和部分主题覆盖不同。后续回填时应合并使用：共同来源只保留一次，差异来源进入 `references/canonical-literature.md` 或 `references/reading-maintenance-policy.md` 的候选清单。

## Quantum ESPRESSO Parameter Deep Research Blueprint for QE-Learning.docx

### 文件状态

- 是否存在：是
- 是否成功读取：是
- 是否疑似重复：否
- 主要主题：QE 参数来源层级、官方定义核对、参数分类、output review、PASS/WARN/BLOCK、manual-ready 参数条目。

### 可用于 QE-Learning 的内容

- 可回填到哪些目录：`workflows/`、`theory-minimum/`、`standards/`、`references/`。
- 可回填到哪些具体页面：
  - `workflows/ground-state/scf.md`
  - `workflows/ground-state/nscf.md`
  - `workflows/ground-state/cutoff-convergence.md`
  - `workflows/ground-state/kpoint-convergence.md`
  - `workflows/ground-state/smearing-and-occupations.md`
  - `workflows/ground-state/relax.md`
  - `workflows/ground-state/vc-relax.md`
  - `workflows/phonon/gamma-phonon.md`
  - `workflows/phonon/phonon-dispersion-dfpt.md`
  - `standards/output-review-checklist.md`
  - `references/source-index.md`
- 可提炼的页面结构：参数条目应区分官方定义、物理/数值/文件链角色、相关 namelist/card、output 证据、常见误用、下游影响和来源。
- 可提炼的判断规则：
  - `ecutwfc`、`ecutrho`、`K_POINTS`、`occupations`、`smearing`、`degauss` 等是数值可靠性控制，不应写成固定推荐值。
  - `input_dft`、`HUBBARD`、`noncolin`、`lspinorb`、`vdw_corr` 等更接近物理模型选择，改变它们等于改变计算问题。
  - `prefix/outdir` 是 workflow 数据边，不只是文件命名习惯。
- 可提炼的 PASS / WARN / BLOCK：
  - `PASS`：参数定义来自官方文档，output 中能验证设置生效，并且目标 observable 的收敛性已记录。
  - `WARN`：参数可运行但未说明与目标 observable 的关系，或 output 中只看到程序结束而没有可靠性证据。
  - `BLOCK`：参数来源不明、与赝势/泛函/下游 workflow 不一致，或关键设置无法在 output 中验证。
- 可提炼的 source map：优先引用 QE documentation、`INPUT_PW`、`INPUT_PH`、package-specific documentation、pseudopotential 页面。
- 可提炼的 QA 规则：新增参数解释前必须核对官方 `INPUT_*`，并标注 stable、version-sensitive 或 boundary。

### 不应直接写入仓库的内容

- 不应复制原文中的完整调研段落、临时链接参数或未经清洗的链接。
- 原因：该文档是研究蓝图，不是最终来源；仓库正文应只保留可复查结论和公开来源。

## QE Workflow Reference Upgrade for QE-Learning.docx

### 文件状态

- 是否存在：是
- 是否成功读取：是
- 是否疑似重复：否
- 主要主题：workflow 定位、上游依赖、文件契约、QE 程序链、关键输入、output review、收敛层级、PASS/WARN/BLOCK、常见失败模式。

### 可用于 QE-Learning 的内容

- 可回填到哪些目录：`workflows/`、`learn/`、`standards/`。
- 可回填到哪些具体页面：
  - `workflows/README.md`
  - `workflows/ground-state/*.md`
  - `workflows/electronic/*.md`
  - `workflows/phonon/*.md`
  - `workflows/advanced/*.md`
  - `learn/01-qe-workflow-map.md`
  - `standards/output-review-checklist.md`
  - `standards/pass-warn-block.md`
- 可提炼的页面结构：每个 workflow 页面应包含计算目标、上游依赖、程序链、关键字段、output review、收敛要求、PASS/WARN/BLOCK、下游准入、来源与版本边界。
- 可提炼的判断规则：
  - workflow 判断必须同时处理 numerical convergence、physical-model choice、postprocessing error 和 workflow propagation error。
  - 高级页只写边界、官方入口和审阅风险，不扩写成完整专题。
  - output review 必须决定是否允许进入下游，而不是只确认命令成功。
- 可提炼的 PASS / WARN / BLOCK：
  - `PASS`：上游依赖、输入字段、output 证据、收敛记录和下游准入全部一致。
  - `WARN`：缺少部分收敛或边界说明，只能进入探索性下游。
  - `BLOCK`：上游状态混用、关键 output 缺失、程序链断裂或有未解释错误。
- 可提炼的 source map：`INPUT_PW`、`INPUT_DOS`、`INPUT_PH`、`INPUT_Q2R`、`INPUT_MATDYN`、PHonon user guide、PostProc user guide。
- 可提炼的 QA 规则：所有 workflow 页面都应能回答“这个 output 是否允许进入下游”。

### 不应直接写入仓库的内容

- 不应保留通用占位如 `<postprocessor>` 作为最终页面内容。
- 原因：规划文档可以保留模板，但正文页面必须写成具体 QE 程序和字段。

## QE Theory Minimum Research Brief for an Unresolved Topic Slot.docx

### 文件状态

- 是否存在：是
- 是否成功读取：是
- 是否疑似重复：否
- 主要主题：`theory-minimum/` 候选主题交叉表、最低理论深度、误解保留、output review、workflow impact、source spine。

### 可用于 QE-Learning 的内容

- 可回填到哪些目录：`theory-minimum/`、`workflows/`、`physics-judgement/`。
- 可回填到哪些具体页面：
  - `theory-minimum/dft-ks-scf.md`
  - `theory-minimum/plane-wave-cutoff.md`
  - `theory-minimum/pseudopotentials.md`
  - `theory-minimum/kpoints-symmetry-kpath.md`
  - `theory-minimum/smearing-metals.md`
  - `theory-minimum/force-stress-relaxation.md`
  - `theory-minimum/dfpt-phonons.md`
  - `theory-minimum/dielectric-born-charge.md`
- 可提炼的页面结构：理论页应从 QE 使用问题进入，映射到 input 字段、output 证据、常见误解、最低掌握深度和对应 workflow。
- 可提炼的判断规则：
  - 理论最低层只解释正确使用 QE 必需的概念。
  - 更深的结果可信度、模型误差和前沿边界应链接到 `physics-judgement/`。
  - 不把 Kohn-Sham eigenvalue、DFT gap、smearing 后 DOS 或虚频解释写成无条件结论。
- 可提炼的 PASS / WARN / BLOCK：理论页本身不替代 workflow 判断，但应说明哪个概念缺失会触发 workflow 的 `WARN` 或 `BLOCK`。
- 可提炼的 source map：Kohn-Sham、Monkhorst-Pack、pseudopotential、DFPT、QE `INPUT_*`。
- 可提炼的 QA 规则：理论段落必须能回到 input/output 或 workflow decision。

### 不应直接写入仓库的内容

- 不应把候选主题交叉表原样复制为正文。
- 原因：表格是调研组织工具，正文需要面向读者的判断说明。

## QE Learning Source Map for Quantum ESPRESSO.docx

### 文件状态

- 是否存在：是
- 是否成功读取：是
- 是否疑似重复：否
- 主要主题：来源优先级、source judgement framework、prioritized source table、详细来源条目、relationship map。

### 可用于 QE-Learning 的内容

- 可回填到哪些目录：`references/`、`standards/`、`physics-judgement/`。
- 可回填到哪些具体页面：
  - `references/source-index.md`
  - `references/canonical-literature.md`
  - `references/reading-maintenance-policy.md`
  - `references/tutorial-sites/official-qe-docs.md`
  - `standards/citation-and-source-policy.md`
- 可提炼的页面结构：来源页应说明来源支持什么判断、来源类型、使用边界、对应仓库页面和维护注意事项。
- 可提炼的判断规则：
  - 参数定义优先官方 `INPUT_*`。
  - 程序链优先官方 guide 和 package-specific docs。
  - 教程用于学习路径和操作分解，不替代官方参数定义。
  - 论文用于理论边界和 canonical conclusion，不替代版本敏感字段。
- 可提炼的 PASS / WARN / BLOCK：来源审查可使用 `PASS` 表示来源可追溯，`WARN` 表示来源间接或需全文核验，`BLOCK` 表示无法追踪。
- 可提炼的 source map：QE documentation、`INPUT_PW`、`INPUT_PH`、`INPUT_PP`、QE Learn、Materials Cloud、AiiDA-QE optional、ASE/pymatgen/SeeK-path 等工具文档。
- 可提炼的 QA 规则：每个链接必须说明“支持什么判断”，不按链接数量或流行度排序。

### 不应直接写入仓库的内容

- 不应把全部链接堆入正文，也不应保留带跟踪参数的 URL。
- 原因：仓库需要可维护来源索引，链接应清洗、分类、注明用途。

## DFT and Quantum ESPRESSO Result Credibility Judgement Blueprint.docx

### 文件状态

- 是否存在：是
- 是否成功读取：是
- 是否疑似重复：否
- 主要主题：可信度判断页应是什么、现象定义、误差分类、QE evidence map、结论强度、PASS/WARN/BLOCK、禁止过度解释。

### 可用于 QE-Learning 的内容

- 可回填到哪些目录：`physics-judgement/`、`standards/`、`workflows/`。
- 可回填到哪些具体页面：
  - `physics-judgement/numerical-vs-model-error.md`
  - `physics-judgement/dft-ground-state-boundary.md`
  - `physics-judgement/kohn-sham-eigenvalue-boundary.md`
  - `physics-judgement/band-gap-problem-and-delocalization.md`
  - `physics-judgement/imaginary-frequency-triage.md`
  - `physics-judgement/uncertainty-statement-template.md`
  - `standards/output-review-checklist.md`
- 可提炼的页面结构：可信度页面应从现象和判断结论开始，再说明可能原因、QE input/output 证据、PASS/WARN/BLOCK、禁止过度结论和来源。
- 可提炼的判断规则：
  - `JOB DONE` 不能证明结果可信。
  - DFT ground-state 计算的 total energy、density、force/stress 与 Kohn-Sham eigenvalue、光谱、激发态的可信度层级不同。
  - 数值误差、模型误差、边界误差、后处理误差和 workflow 传播误差要分开记录。
- 可提炼的 PASS / WARN / BLOCK：
  - `PASS`：关键证据完整，误差类型已分类，下游声明与证据层级匹配。
  - `WARN`：可用于趋势或探索，但缺少模型边界或来源核验。
  - `BLOCK`：存在过度解释、来源缺失或关键 output 证据缺失。
- 可提炼的 source map：DFT 近似、band gap problem、DFPT、pseudopotential、QE user guide、PH docs。
- 可提炼的 QA 规则：每个 physics judgement 结论应标注 Strong、Moderate、Boundary 或 Version-sensitive。

### 不应直接写入仓库的内容

- 不应把示例 output 或外部测试输出当作仓库案例。
- 原因：本仓库只保留通用证据结构，不维护具体材料 output。

## Deep Research Template for QE Output Evidence Review.docx

### 文件状态

- 是否存在：是
- 是否成功读取：是
- 是否疑似重复：否
- 主要主题：QE output evidence item 的含义、出现位置、能证明什么、不能证明什么、false confidence 风险、PASS/WARN/BLOCK 使用方式。

### 可用于 QE-Learning 的内容

- 可回填到哪些目录：`standards/`、`workflows/`、`learn/`。
- 可回填到哪些具体页面：
  - `standards/output-review-checklist.md`
  - `standards/pass-warn-block.md`
  - `standards/calculation-record-template.md`
  - `workflows/ground-state/scf.md`
  - `workflows/ground-state/relax.md`
  - `workflows/phonon/phonon-debugging.md`
- 可提炼的页面结构：每个 output evidence entry 应说明位置、证据含义、不能证明的内容、触发 WARN/BLOCK 的条件、记录字段和下游影响。
- 可提炼的判断规则：
  - `convergence has been achieved` 只证明某个电子/离子/扰动收敛条件达到，不自动证明物理模型正确。
  - total energy、Fermi energy、forces、stress、symmetry、irreducible k-points、warnings 都需要与 input 和上游状态一起审阅。
  - phonon 输出需要额外审阅 perturbation convergence、dyn/fc/freq 文件链、acoustic modes、negative frequency 和 ASR 使用边界。
- 可提炼的 PASS / WARN / BLOCK：可直接形成 workflow-specific output review 表。
- 可提炼的 source map：`INPUT_PW`、`INPUT_PH`、`INPUT_DOS`、`INPUT_PROJWFC`、`INPUT_Q2R`、PH guide、PW guide、PP guide。
- 可提炼的 QA 规则：每个 output 证据必须说明“能证明什么”和“不能证明什么”。

### 不应直接写入仓库的内容

- 不应复制测试套输出路径或将外部 benchmark 输出写成仓库样例。
- 原因：output review 应是通用证据框架，不是具体 output 文件库。

## Deep Research Review of the QE-Learning Learn Landing Page.docx

### 文件状态

- 是否存在：是
- 是否成功读取：是
- 是否疑似重复：否
- 主要主题：学习入口阶段定位、能力目标、深度研究发现、常见错误、完成判据、可验证输出模板。

### 可用于 QE-Learning 的内容

- 可回填到哪些目录：`learn/`、`README.md`、`standards/`。
- 可回填到哪些具体页面：
  - `README.md`
  - `learn/README.md`
  - `learn/00-start-here.md`
  - `learn/01-qe-workflow-map.md`
  - `standards/output-review-checklist.md`
- 可提炼的页面结构：学习入口应围绕能力目标、完成判据、可验证输出、常见误解、与 workflow/standards 的联动展开。
- 可提炼的判断规则：
  - 学习路径按能力门槛组织，不按时间组织。
  - 初学者必须先理解 output review 和下游准入，不应只收集 input。
  - 学习完成证据包括能力复述、output 判断和可验证输出。
- 可提炼的 PASS / WARN / BLOCK：
  - `PASS`：学习者能解释 input、定位 output 证据并给出下游准入。
  - `WARN`：能运行命令但无法解释 output 或误差来源。
  - `BLOCK`：把程序结束当作物理结论。
- 可提炼的 source map：QE official、`INPUT_PW`、Pranab SCF、DFT reproducibility literature。
- 可提炼的 QA 规则：入口页应保持简洁，不扩写成全库索引。

### 不应直接写入仓库的内容

- 不应把 landing page review 中的审稿式评价原文写进 README。
- 原因：README 应是稳定入口，不是研究评审记录。

## Authoritative Literature Loop for QE and DFT Physical Judgement.docx

### 文件状态

- 是否存在：是
- 是否成功读取：是
- 是否疑似重复：与下一份文档主题重复、内容互补。
- 主要主题：literature loop map、core reading layers、Fast Core Loop、Workflow-Oriented Loop、Frontier Entry Loop、topic-by-topic literature matrix、repo mapping、DOI set、agent-team writing plan、missing areas 和 maintenance policy。

### 可用于 QE-Learning 的内容

- 可回填到哪些目录：`references/`、`physics-judgement/`、`theory-minimum/`。
- 可回填到哪些具体页面：
  - `references/canonical-literature.md`
  - `references/reading-maintenance-policy.md`
  - `physics-judgement/CONCLUSION_REFERENCE_BOOK.md`
  - `physics-judgement/uncertainty-statement-template.md`
  - `theory-minimum/dft-ks-scf.md`
- 可提炼的页面结构：canonical literature 应按 Fast Core Loop、Workflow-Oriented Loop、Frontier Entry Loop、主题矩阵和维护策略组织。
- 可提炼的判断规则：
  - canonical source 应按支持层级使用，经典理论、方法论文和官方文档承担不同角色。
  - physics judgement 页面需要结论强度和是否需要全文核验标记。
  - frontiers 只作为边界入口，不写成方法承诺。
- 可提炼的 PASS / WARN / BLOCK：来源支撑充分且适用边界清楚为 `PASS`；摘要级结论或二手来源为 `WARN`；来源无法追踪为 `BLOCK`。
- 可提炼的 source map：HK、KS、DFPT、QE papers、Wannier90、EPW、DFT+U、vdW、GW/BSE、reproducibility。
- 可提炼的 QA 规则：Fast Core Loop 应保持小而稳定，避免无限扩 DOI。

### 不应直接写入仓库的内容

- 不应保留面向写作团队的过程性指令作为正文。
- 原因：仓库读者需要来源导读和判断边界，不需要内部调研过程。

## Authoritative Literature Loop for QE _ DFT Physical Judgement.docx

### 文件状态

- 是否存在：是
- 是否成功读取：是
- 是否疑似重复：与上一份文档主题重复、内容互补。
- 主要主题：literature loop map、topic-by-topic literature matrix、core reading loops、canonical sets、repo mapping、bibliography 和写作计划。

### 可用于 QE-Learning 的内容

- 可回填到哪些目录：`references/`、`physics-judgement/`、`workflows/advanced/`。
- 可回填到哪些具体页面：
  - `references/canonical-literature.md`
  - `references/canonical.bib`（如果后续维护 BibTeX）
  - `references/reading-maintenance-policy.md`
  - `workflows/advanced/wannier90-overview.md`
  - `workflows/advanced/electron-phonon-overview.md`
  - `physics-judgement/ground-state-vs-excited-state.md`
- 可提炼的页面结构：bibliography 应包含来源级别、主题、支持判断、是否版本敏感、后续核验状态。
- 可提炼的判断规则：
  - 普通 ground-state DFT bands 不能替代 quasiparticle 或 optical spectra 判断。
  - Wannierization、EPC、GW/BSE 和 advanced package 应作为数据链和边界判断，而非基础学习主线。
  - 来源维护需要标记 canonical、workflow-support、frontier-entry 和 optional-tool。
- 可提炼的 PASS / WARN / BLOCK：canonical literature 支撑明确为 `PASS`；只作 frontier entry 为 `WARN`；用于参数定义但不是官方文档为 `BLOCK` 或需改引官方来源。
- 可提炼的 source map：Wannier90、Yambo、GW/BSE、EPC、NEB、advanced electronic-structure sources。
- 可提炼的 QA 规则：两个 Authoritative 文档合并时，应按主题去重、保留互补来源，不复制重复 DOI 列表。

### 不应直接写入仓库的内容

- 不应把外部仓库旧 URL 或调研过程中的临时 repo mapping 原样保留。
- 原因：当前仓库应只引用现行页面和公开稳定来源。

## 合并使用原则

- `.docx` 参考文档只作为回填规划输入，不作为正文引用对象。
- 稳定参数定义优先核对 QE `INPUT_*` reference。
- 稳定 workflow 过程优先核对 QE official guide、package guide 和可靠教程。
- 稳定理论判断优先核对 canonical literature 或综述。
- 摘要级结论可以进入 planning 或 boundary note；进入正文前需要标注来源强度并尽量核验官方文档或论文正文。
