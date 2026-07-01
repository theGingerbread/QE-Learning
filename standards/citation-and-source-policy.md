# Citation and Source Policy

## 本页解决什么问题

本页规定 QE-Learning 如何使用来源。目标是让参数定义、程序行为、workflow 判断、物理边界和 teaching convenience 分开追踪，避免把官方文档、教程、工具页面、论文和个人判断混成同一层证据。

所有新增或修改页面都应回答两个问题：该判断由什么来源支持；该来源能支持什么，不能支持什么。

## 来源类型

| 来源类型 | 可支持什么 | 不能支持什么 | 主要入口 |
|---|---|---|---|
| official docs | QE 参数定义、程序行为、package guide、文件格式、版本敏感字段 | 不能自动给出科研结论或材料参数 | [source-index.md](../references/source-index.md) |
| official examples | 官方示范输入、程序链、package 使用方式 | 不能作为普适参数推荐 | QE documentation / examples |
| canonical literature | DFT/DFPT/PP/Wannier/EPC/GW/BSE/reproducibility 的方法边界和 failure-mode 判断 | 不能替代当前版本 `INPUT_*` 字段定义 | [canonical-literature.md](../references/canonical-literature.md) |
| tool docs | Wannier90、EPW、Yambo、SeeK-path、Phonopy、ASE 等工具接口和使用边界 | 不能替代 QE 原生命令行 workflow 或 output review | [source-index.md](../references/source-index.md) |
| tutorial websites | workflow 拆解、学习顺序、hands-on 输出阅读辅助 | 不能定义 QE 参数、默认值或版本行为 | `references/tutorial-sites/` |
| internal judgement | 本仓库 `PASS / WARN / BLOCK`、output review、record template 和 uncertainty statement | 不能替代官方文档、工具文档或 canonical literature | `standards/`、`physics-judgement/` |
| personal inference | 页面维护者基于公开来源形成的审阅建议 | 不能写成无边界事实或定量推荐 | 必须在页末说明依据和边界 |

## 断言与来源优先级

| 断言类型 | 首选来源 | 可辅助来源 | 备注 |
|---|---|---|---|
| 参数定义、默认值、允许取值、namelist/card 语法 | QE 官方 `INPUT_*` 或工具官方 input reference | 官方 examples | 教程和论文不能替代官方字段定义 |
| 程序链、文件依赖、package 行为 | QE official guide / package docs | 高质量教程、官方 examples | `prefix/outdir`、`fildyn/flfrc`、interface files 等必须可追踪 |
| output review | 官方文档、实际 output 证据、本仓库 standards | 教程中的输出解读 | `JOB DONE` 只说明程序完成，不说明科研可信 |
| physical judgement | canonical literature、本仓库 physics judgement | workflow output evidence | 需区分 Strong、Moderate、Boundary、Version-sensitive |
| teaching convenience | tutorial-sites、本仓库 learn/workflow 页面 | official docs | 只能服务学习顺序，不生成参数推荐 |
| tool boundary | 工具官方文档 | 本仓库 tools 导读 | 工具页只说明位置和边界，不进入基础学习路线 |

## Version-sensitive 规则

以下内容属于 version-sensitive：

- QE `INPUT_*` 字段、默认值、允许取值、废弃状态或新增参数。
- PHonon、PostProc、EPW、Wannier90、Yambo、AiiDA-QE、SeeK-path、Phonopy 等工具的输入语法、接口文件和输出格式。
- `HUBBARD` syntax、DFT+U+V、SOC / noncollinear、hybrid、vdW、EPC、GW/BSE 等高级接口。
- restart、scratch、parallel I/O、scheduler 或 package-specific 文件约定。

写 version-sensitive 判断时必须：

- 指向当前官方文档或工具文档。
- 避免写成永久结论。
- 在页面末尾说明来源用于核对哪个字段或程序行为。
- 若无法核对，不写成事实；放入 TODO 或维护报告。

## 禁止写法

- 只凭博客、教程或课程讲义写 QE 参数定义。
- 用教程替代官方 `INPUT_*`。
- 用论文摘要替代工具版本文档。
- 把个人经验写成无边界结论。
- 堆链接但不说明用途。
- 使用私有路径、未公开文件、登录态链接、tracking URL 或无法复查的截图来源。
- 把某个 functional、vdW、DFT+U、SOC、hybrid、GW/BSE 或工具写成普适改进。
- 给材料无关的 cutoff、k mesh、smearing、q-grid、vacuum、Wannier window 或 EPC grid 数值建议。

## 页面来源写法

页面正文尽量不堆链接。来源集中放在页末，且每条来源说明用途：

```markdown
## 资料来源

- [QE INPUT_PW](https://www.quantum-espresso.org/Doc/INPUT_PW.html)：用于核对 `pw.x` 字段定义和版本敏感行为。
- [references/canonical-literature.md](../references/canonical-literature.md)：用于核对 DFT/DFPT 方法边界。
- [standards/output-review-checklist.md](output-review-checklist.md)：用于统一 output review 和下游准入。
```

推荐写法：

- “该判断由 QE `INPUT_PW` 支持，用于核对 `occupations/smearing/degauss` 的字段语义，不用于给出材料无关参数值。”
- “该字段是 version-sensitive，使用前应核对当前官方 `INPUT_*`。”
- “该结论是 Boundary，用于限制解释范围，不作为定量推荐。”
- “该教程用于 workflow 学习顺序，不用于参数定义。”
- “该文献支持方法边界，不替代工具官方文档。”

## input 模板来源标注

每个 input 模板必须说明来源类型，不能只给模板本身。

推荐标签：

- `来源类型：官方文档改写`：根据 QE 官方 reference 或 guide 整理。
- `来源类型：公开教程改写`：从公开教程学习流程后重写，参数含义仍回到官方文档。
- `来源类型：自建学习模板`：为说明参数位置、文件链或 review 步骤而构造。

模板至少说明：

- 对应 QE 程序，例如 `pw.x`、`ph.x`、`q2r.x`、`matdyn.x`。
- 模板意图，例如 SCF、relax、DOS、phonon 或 post-processing。
- 参数定义核对入口，例如 QE 官方 `INPUT_*`。
- 下游 output review 入口。

模板不得声称“推荐参数”“通用设置”或“最佳配置”。如需给出实践建议，必须写清适用范围、来源和反例边界。

## 工具和教程导读规则

`references/tutorial-sites/` 和 `references/tools/` 的页面是导读页，不是外部资料复刻。

教程导读页应写清：

- 该教程适合回答什么学习问题。
- 它适合放在学习路径的哪个阶段。
- 哪些结论必须回到 QE 官方文档核对。
- 哪些内容属于教学简化或特定环境选择。

工具导读页应写清：

- 工具在 QE workflow 中帮助解决什么问题。
- 工具不能替代什么，例如 QE input 理解、output review、收敛判断或物理解释。
- 使用工具时需要核对哪些原始工具文档。
- 工具页不是推荐榜，不按流行度排序。

## Canonical literature 规则

论文和方法来源使用 [references/canonical-literature.md](../references/canonical-literature.md) 的 A0/A1/A2/B1/B2/C 分级。

- A0/A1/A2 应保持小而稳定。
- 新增 A 级来源前，必须说明它改变哪个 output review、`PASS / WARN / BLOCK` 或 physics judgement。
- 不确定 DOI、卷页、作者顺序或版本信息时，不写入 [canonical.bib](../references/canonical.bib)；先在维护报告中列 TODO。
- canonical literature 支持方法边界，不支持当前工具版本字段。

## 新增页面 source checklist

新增页面或大幅修改页面前，检查：

- 是否有参数定义、默认值、输入语法或程序行为断言；若有，是否回到官方文档。
- 是否有 workflow 顺序或文件链断言；若有，是否回到官方 guide、教程导读或已有 workflow 页面。
- 是否有模型边界或物理判断；若有，是否回到 canonical literature 或 physics-judgement 页面。
- 是否有工具接口或高级方法；若有，是否回到工具官方文档。
- 是否有本地私有路径、未公开文件、tracking URL 或无法复查来源。
- 来源条目是否说明“用于支持什么判断”。
- 页面末尾是否集中列出来源。

## 资料来源

- [References Source Index](../references/source-index.md)：公开来源总入口。
- [Canonical Literature](../references/canonical-literature.md)：论文级 source spine。
- [Reading Maintenance Policy](../references/reading-maintenance-policy.md)：文献维护和分级规则。
- [References README](../references/README.md)：教程页和工具页导读边界。
