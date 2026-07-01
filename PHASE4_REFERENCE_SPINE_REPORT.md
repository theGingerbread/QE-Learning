# Phase 4 Reference Spine Report

## Scope

本轮只处理 `references/source-index.md`、`references/canonical-literature.md`、`references/canonical.bib`、`standards/citation-and-source-policy.md`，并最小更新 `references/tutorial-sites/official-qe-docs.md`。目标是把前面 Phase 1-3 使用过的官方文档、工具文档和 canonical literature 统一成可维护 source spine。

本轮没有大规模改写 `workflows/`、`theory-minimum/`、`physics-judgement/` 正文，也没有新增工具教程或材料绑定算例。

## Files changed

- `references/source-index.md`
- `references/canonical-literature.md`
- `references/canonical.bib`
- `references/tutorial-sites/official-qe-docs.md`
- `standards/citation-and-source-policy.md`
- `PHASE4_REFERENCE_SPINE_REPORT.md`

## Source index changes

- 将 `source-index.md` 从单一链接表重组为按用途组织的 source spine。
- 新增使用规则，明确：
  - 参数定义优先 QE official `INPUT_*`。
  - 程序链优先 QE official docs / package docs。
  - canonical literature 进入 `canonical-literature.md`。
  - 工具文档只说明边界，不替代 QE 原生命令行 workflow。
  - version-sensitive 字段必须查当前官方文档。
- 将来源分为：
  - QE official documentation；
  - QE workflow tutorials；
  - Tool documentation；
  - Canonical literature spine。
- 官方文档表补齐 `INPUT_DOS`、`INPUT_PROJWFC`、`INPUT_DYNMAT` 等 electronic / phonon workflow 需要的入口。
- 工具文档按用途拆分为 structure/k-path/visualization、phonon、Wannier/EPC/excited-state、workflow/provenance advanced reference。

## Canonical literature changes

- 保留 A0/A1/A2/B1/B2/C 分级，并强化每级用途。
- 保留 Fast Core Loop 20 篇上限。
- 将文献骨架按主题分组：
  - DFT foundations；
  - Exchange-correlation and DFT errors；
  - Pseudopotential / plane-wave / k-point / smearing；
  - QE software and reproducibility；
  - DFPT / phonons / response；
  - DFT+U and U provenance；
  - vdW and low-dimensional systems；
  - Wannier；
  - EPC；
  - Excited states / GW / BSE；
  - Thermodynamics and uncertainty。
- 每条文献都补充“支持的判断”“对应仓库页面”“备注”，避免论文清单化。
- 新增条目：
  - PBEsol：作为 functional sensitivity 专题入口。
  - QE toward exascale：作为 QE 能力演化背景。
  - Dion vdW-DF 与 Tkatchenko-Scheffler：作为 vdW model boundary 入口。
  - Souza / Marzari / Vanderbilt entangled bands 与 MLWF review：作为 Wannier window / validation 支撑。
  - EPW code paper：作为 EPC data chain 和 EPW 工具边界支撑。
- 没有删除既有 Fast Core Loop 条目。
- Timrov / Marzari / Cococcioni DFPT Hubbard parameter 文献和 QHA / anharmonic thermodynamics 文献保留为维护 TODO，未强行提升为 A 级。

## BibTeX changes

- 在 `canonical.bib` 中新增已能稳定识别的条目：
  - `Perdew2008PBEsol`
  - `Giannozzi2020QE`
  - `Dion2004VDWDF`
  - `Tkatchenko2009`
  - `Souza2001Disentanglement`
  - `Marzari2012MLWFReview`
  - `Ponce2016EPW`
- 未加入 metadata 未精核的 Timrov / DFPT-U 与 QHA / thermodynamics 条目。
- 未编造 DOI、版本号或工具 metadata。
- 本轮仅做新增和去重检查，没有对既有 BibTeX 作者列表做全文级校订。

## Source policy changes

- 将 `standards/citation-and-source-policy.md` 重写为可执行的来源政策。
- 新增来源类型矩阵：
  - official docs；
  - official examples；
  - canonical literature；
  - tool docs；
  - tutorial websites；
  - internal judgement；
  - personal inference。
- 新增断言类型与来源优先级矩阵，区分参数定义、程序链、output review、physical judgement、teaching convenience 和 tool boundary。
- 强化 version-sensitive 规则，覆盖 QE `INPUT_*`、PHonon、EPW、Wannier90、Yambo、Hubbard syntax、SOC/noncollinear 和 tool interface。
- 增加写作模板：
  - “该判断由 X 支持，用于 Y，不用于 Z。”
  - “该字段是 version-sensitive，使用前应核对当前官方 `INPUT_*`。”
  - “该结论是 Boundary，用于限制解释范围，不作为定量推荐。”
- 明确教程、工具页和 canonical literature 的不同边界，防止用教程替代官方字段定义。

## What was intentionally not changed

- 没有大改 workflow 正文。
- 没有大改 theory-minimum 或 physics-judgement 正文。
- 没有新增大批文献。
- 没有写工具教程。
- 没有写材料绑定算例。
- 没有把工具文档写成基础学习路径。
- 没有把 source map 写成 bibliography dump。

## Follow-up

建议下一阶段进入 Phase 5：standards / QA / final integration。重点是：

- 统一 `standards/` 中的 PASS/WARN/BLOCK、output review、calculation record 和 source policy 术语。
- 做全仓库 Markdown link audit、source back-link audit 和 forbidden wording audit。
- 检查 phase reports 与 README / directory index 是否一致。
- 准备合并前 final checklist。

如果需要更细的文献维护，可开 Phase 4-B：reference link audit and metadata review，专门核对 BibTeX metadata、Timrov / DFPT-U、QHA / thermodynamics 和工具文档版本。
