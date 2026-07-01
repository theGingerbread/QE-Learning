# Project Backfill Priority Roadmap

本路线图按阶段组织 Deep Research 回填工作。当前分支只完成 reference intake、矩阵和 subagent 任务规划；后续执行应按阶段小步提交，避免一次性大规模改写。

## Phase 0: Reference Intake And Dedup

### 目标

- 确认所有 Deep Research 参考文档可读。
- 判断重复和互补关系。
- 建立 reference intake、backfill matrix 和 subagent task plan。

### 输入参考文档

- Quantum ESPRESSO Parameter Deep Research Blueprint for QE-Learning.docx
- QE Workflow Reference Upgrade for QE-Learning.docx
- QE Theory Minimum Research Brief for an Unresolved Topic Slot.docx
- QE Learning Source Map for Quantum ESPRESSO.docx
- DFT and Quantum ESPRESSO Result Credibility Judgement Blueprint.docx
- Deep Research Template for QE Output Evidence Review.docx
- Deep Research Review of the QE-Learning Learn Landing Page.docx
- Authoritative Literature Loop for QE and DFT Physical Judgement.docx
- Authoritative Literature Loop for QE _ DFT Physical Judgement.docx

### 目标仓库文件

- `PROJECT_REFERENCE_INTAKE.md`
- `DEEP_RESEARCH_BACKFILL_MATRIX.md`
- `SUBAGENT_BACKFILL_TASK_PLAN.md`
- `PROJECT_BACKFILL_PRIORITY_ROADMAP.md`

### 主要产出

- 文档读取状态。
- 重复判断。
- 仓库页面回填矩阵。
- 可派发 subagent prompt。
- 分阶段路线图。

### 验收标准

- 每份参考文档都有状态记录。
- 无法读取的文件明确报告。
- 两份 Authoritative Literature Loop 文档按“主题重复、内容互补”处理。
- 规划文件不复制参考文档原文。
- 规划文件不写私有路径。

### 不做什么

- 不大规模改写 `learn/`、`workflows/`、`theory-minimum/`、`physics-judgement/`、`references/`、`standards/` 正文。
- 不创建具体材料案例。

## Phase 1: Project Scope Correction

### 目标

- 微调入口页，确保项目唯一目标是 QE 计算参考手册和 DFT 知识体系。
- 明确 `learn/`、`workflows/`、`theory-minimum/`、`physics-judgement/`、`references/`、`standards/` 的职责边界。
- 将 Deep Research 入口建议转成稳定读者指引。

### 输入参考文档

- Deep Research Review of the QE-Learning Learn Landing Page.docx
- DFT and Quantum ESPRESSO Result Credibility Judgement Blueprint.docx
- QE Learning Source Map for Quantum ESPRESSO.docx

### 目标仓库文件

- `README.md`
- `learn/README.md`
- `learn/00-start-here.md`
- `workflows/README.md`
- `theory-minimum/README.md`
- `physics-judgement/README.md`
- `standards/README.md`

### 主要产出

- 简洁项目入口。
- 能力目标和完成判据。
- output review 和下游准入入口。
- theory-minimum 与 physics-judgement 分工说明。

### 验收标准

- README 不扩写成教程。
- 入口页能导向 workflow、theory、physics judgement、standards。
- 不出现具体材料案例或固定参数。
- 自动化工具只作为高级参考。

### 不做什么

- 不改变目录结构。
- 不新增大类目录。
- 不把入口页写成调研报告。

## Phase 2: Main Workflow Upgrade

### 目标

- 把主线 workflow 写成可复查 QE 原生命令行参考。
- 每个 workflow 页面包含 input 字段、output review、收敛要求、PASS/WARN/BLOCK、下游准入和来源边界。

### 输入参考文档

- QE Workflow Reference Upgrade for QE-Learning.docx
- Quantum ESPRESSO Parameter Deep Research Blueprint for QE-Learning.docx
- Deep Research Template for QE Output Evidence Review.docx

### 目标仓库文件

- `workflows/ground-state/scf.md`
- `workflows/ground-state/nscf.md`
- `workflows/ground-state/cutoff-convergence.md`
- `workflows/ground-state/kpoint-convergence.md`
- `workflows/ground-state/smearing-and-occupations.md`
- `workflows/ground-state/relax.md`
- `workflows/ground-state/vc-relax.md`
- `workflows/electronic/bands.md`
- `workflows/electronic/dos.md`
- `workflows/electronic/pdos.md`
- `workflows/electronic/charge-density.md`
- `workflows/electronic/electrostatic-potential.md`
- `workflows/electronic/work-function.md`
- `workflows/phonon/gamma-phonon.md`
- `workflows/phonon/phonon-dispersion-dfpt.md`
- `workflows/phonon/phonon-dos.md`
- `workflows/phonon/dielectric-born-effective-charge.md`
- `workflows/phonon/phonon-debugging.md`

### 主要产出

- SCF/NSCF/convergence/relax/vc-relax 主线补强。
- bands/DOS/PDOS 和 post-processing 解释边界补强。
- phonon/DFPT/q2r/matdyn 文件链和 output evidence 补强。

### 验收标准

- 每个 workflow 页面都能回答“是否允许进入下游”。
- 每个页面都有 workflow-specific output review。
- 参数解释能追溯到官方 `INPUT_*`。
- 不写具体材料 input/output。

### 不做什么

- 不写固定参数答案。
- 不把高级功能扩写成完整专题教程。

## Phase 3: Theory Minimum Upgrade

### 目标

- 把最低理论页补成 QE input/output 可回查层。
- 明确哪些理论只需最低掌握，哪些判断应进入 `physics-judgement/`。

### 输入参考文档

- QE Theory Minimum Research Brief for an Unresolved Topic Slot.docx
- Quantum ESPRESSO Parameter Deep Research Blueprint for QE-Learning.docx
- QE Learning Source Map for Quantum ESPRESSO.docx

### 目标仓库文件

- `theory-minimum/README.md`
- `theory-minimum/dft-ks-scf.md`
- `theory-minimum/plane-wave-cutoff.md`
- `theory-minimum/pseudopotentials.md`
- `theory-minimum/kpoints-symmetry-kpath.md`
- `theory-minimum/smearing-metals.md`
- `theory-minimum/force-stress-relaxation.md`
- `theory-minimum/magnetism-soc-dftu.md`
- `theory-minimum/dfpt-phonons.md`
- `theory-minimum/dielectric-born-charge.md`
- `theory-minimum/functional-choice.md`

### 主要产出

- DFT/Kohn-Sham/SCF 与 QE output 的关系。
- plane-wave cutoff、PP、kmesh、smearing 的最低理论。
- force/stress、DFPT、dielectric/Born、magnetism/SOC/DFT+U 的使用边界。

### 验收标准

- 每个理论概念都映射到 QE input 字段、output 迹象或 workflow decision。
- 不写长篇推导。
- 不把模型误差写成数值收敛问题。

### 不做什么

- 不扩写成 DFT 教材。
- 不写具体材料理论故事。

## Phase 4: Physics Judgement Upgrade

### 目标

- 把结果可信度判断页补成科研判断参考册。
- 帮助读者区分数值误差、模型误差、边界误差、后处理误差和 workflow 传播误差。

### 输入参考文档

- DFT and Quantum ESPRESSO Result Credibility Judgement Blueprint.docx
- Authoritative Literature Loop for QE and DFT Physical Judgement.docx
- Authoritative Literature Loop for QE _ DFT Physical Judgement.docx
- QE Learning Source Map for Quantum ESPRESSO.docx

### 目标仓库文件

- `physics-judgement/README.md`
- `physics-judgement/CONCLUSION_REFERENCE_BOOK.md`
- `physics-judgement/numerical-vs-model-error.md`
- `physics-judgement/dft-ground-state-boundary.md`
- `physics-judgement/kohn-sham-eigenvalue-boundary.md`
- `physics-judgement/functional-choice-and-sensitivity.md`
- `physics-judgement/pseudopotential-transferability-and-functional-consistency.md`
- `physics-judgement/band-gap-problem-and-delocalization.md`
- `physics-judgement/kmesh-smearing-sensitivity.md`
- `physics-judgement/relax-is-not-final-electronic-structure.md`
- `physics-judgement/imaginary-frequency-triage.md`
- `physics-judgement/u-value-provenance-and-boundary.md`
- `physics-judgement/soc-and-symmetry-boundary.md`
- `physics-judgement/vdw-and-low-dimensional-boundary.md`
- `physics-judgement/work-function-and-electrostatic-boundary.md`
- `physics-judgement/wannier-validation-and-window-choice.md`
- `physics-judgement/epc-data-chain-and-convergence.md`
- `physics-judgement/ground-state-vs-excited-state.md`
- `physics-judgement/energy-vs-free-energy.md`
- `physics-judgement/uncertainty-statement-template.md`

### 主要产出

- 可信度判断页的核心结论。
- `PASS / WARN / BLOCK`。
- output evidence。
- 不能做出的过度结论。
- conclusion strength 和来源边界。

### 验收标准

- 每页能服务实际科研判断。
- 每个强断言有来源或明确标注为 boundary。
- 不把高级方法写成普适更准。

### 不做什么

- 不写论文综述。
- 不堆 DOI。
- 不写具体材料案例。

## Phase 5: Source And Literature Spine

### 目标

- 建立来源和 canonical literature 的稳定骨架。
- 让关键判断可追溯。
- 让版本敏感项有维护入口。

### 输入参考文档

- QE Learning Source Map for Quantum ESPRESSO.docx
- Authoritative Literature Loop for QE and DFT Physical Judgement.docx
- Authoritative Literature Loop for QE _ DFT Physical Judgement.docx
- Quantum ESPRESSO Parameter Deep Research Blueprint for QE-Learning.docx

### 目标仓库文件

- `references/README.md`
- `references/source-index.md`
- `references/canonical-literature.md`
- `references/reading-maintenance-policy.md`
- `references/tutorial-sites/official-qe-docs.md`
- `standards/citation-and-source-policy.md`

### 主要产出

- 来源类型和用途说明。
- official docs、`INPUT_*`、package guide、canonical literature、tutorial/tool docs 的分工。
- A0/A1/A2/B/C 或等价来源层级。
- stable、version-sensitive、boundary 标记。

### 验收标准

- 每个来源说明支持什么判断。
- 参数定义优先官方文档。
- 论文来源用于理论和物理判断边界。
- 教程来源用于学习路径和 workflow decomposition。

### 不做什么

- 不把链接清单当正文。
- 不按工具热度或链接数量排序。

## Phase 6: Standards And QA

### 目标

- 统一记录、output review、PASS/WARN/BLOCK、source policy 和质量检查。
- 对回填分支做最终验证。

### 输入参考文档

- Deep Research Template for QE Output Evidence Review.docx
- DFT and Quantum ESPRESSO Result Credibility Judgement Blueprint.docx
- QE Learning Source Map for Quantum ESPRESSO.docx

### 目标仓库文件

- `standards/README.md`
- `standards/input-file-naming.md`
- `standards/calculation-record-template.md`
- `standards/project-layout.md`
- `standards/pass-warn-block.md`
- `standards/output-review-checklist.md`
- `standards/citation-and-source-policy.md`
- 全仓库 Markdown 文件。

### 主要产出

- output review 标准。
- calculation record template。
- source policy。
- QA checklist。
- final validation report。

### 验收标准

- Markdown 本地链接检查通过。
- 私有路径扫描通过。
- 材料绑定内容扫描通过。
- 术语一致性检查通过。
- `git diff --check` 通过。
- README 与目录索引一致。

### 不做什么

- 不以 QA 为名重构目录。
- 不新增具体材料目录。
- 不把 standards 写成外部执行系统规范。

## 推荐执行顺序

1. 完成 Phase 0 并提交规划文件。
2. 执行 Phase 1，保持入口简洁。
3. 执行 Phase 2，优先主线 workflow。
4. 执行 Phase 3 和 Phase 4，补齐理论和可信度判断闭环。
5. 执行 Phase 5，整理来源骨架。
6. 执行 Phase 6，做最终 QA 和报告。

每个 phase 建议独立提交，commit message 说明修改目的，避免使用泛泛的 “update docs”。
