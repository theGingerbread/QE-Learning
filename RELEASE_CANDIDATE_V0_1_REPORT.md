# Release Candidate v0.1 Report

## Scope

本轮只做 handbook release-readiness 导航整合：新增总索引、把入口 README 回链到索引，并补充 v0.1 release notes。没有继续扩写 workflow、theory-minimum 或 physics-judgement 正文。

## Subagents used

| Subagent | Role | Target pages | Output |
|---|---|---|---|
| I1 Style Integrator | 统一入口导航和页面职责 | `README.md`, directory README files | 最小回链到 handbook index |
| I2 Source Integrator | 检查来源边界是否需要调整 | `references/` source spine | 未发现需要修改 source spine |
| I3 Final QA Runner | 执行链接、范围和高风险表述检查 | 全仓库 Markdown | 验证结果记录在本报告 |

## Navigation changes

- 新增 [HANDBOOK_INDEX.md](HANDBOOK_INDEX.md)，按读者目标组织入口：学习路径、workflow 审阅、理论回查、physics judgement、source/record。
- 在根 [README.md](README.md)、[learn/README.md](learn/README.md)、[workflows/README.md](workflows/README.md)、[theory-minimum/README.md](theory-minimum/README.md)、[physics-judgement/README.md](physics-judgement/README.md) 加入最小索引回链。
- 保持各目录 README 原有职责边界：`learn/` 负责能力路径，`workflows/` 负责 QE 原生命令行 workflow，`theory-minimum/` 负责最低理论回查，`physics-judgement/` 负责可信度判断，`references/` 负责 source spine，`standards/` 负责记录和 QA。

## Source boundary

本轮没有新增 canonical literature 或工具来源。`HANDBOOK_INDEX.md` 只引用仓库内部页面；外部来源仍由 [references/source-index.md](references/source-index.md)、[references/canonical-literature.md](references/canonical-literature.md) 和 [standards/citation-and-source-policy.md](standards/citation-and-source-policy.md) 维护。

## Validation results

- `git diff --check`: PASS.
- Markdown local links: PASS, `OK local markdown links checked: 147 files`.
- Private path / document residue scan: PASS for touched files.
- Project-scope drift scan: PASS; scope terms appear only in exclusion or QA wording.
- Fixed material case scan: PASS; no concrete material examples added.
- Universal parameter scan: PASS; hits appear only in "not included" or QA wording.
- High-risk overclaim scan: PASS; no new high-risk overclaim added.
- Forbidden directory check: PASS.

## Remaining gaps

- 本索引是 v0.1 参考手册入口，不替代后续逐页专家审阅。
- `physics-judgement/` 中编号页和快速判断页仍有双轨结构，后续可做维护性去重。
- 外部链接和 BibTeX metadata 仍适合在独立 source verification pass 中抽查。

## Final QA Gate

| Gate | Result | Evidence |
|---|---|---|
| Physics accuracy | PASS | 本轮只新增导航和 release notes，没有新增物理断言。 |
| Style consistency | PASS | 入口回链为简短说明，未改变各目录正文风格。 |
| Source boundary | PASS | 未新增外部来源；source spine 仍由 `references/` 和 citation policy 维护。 |
| Output-review framing | PASS | 总索引保留 output review、收敛记录和下游准入作为查阅路径。 |
| PASS/WARN/BLOCK preservation | PASS | 总索引和 README 回链继续引用 `PASS / WARN / BLOCK` 作为判断 gate。 |
| Local links | PASS | `OK local markdown links checked: 147 files`. |
| Private path / document residue | PASS | Touched-file scan found no private path or local research-document path residue. |
| Project-scope drift | PASS | 未引入 runtime、MCP、VibeDFT 或自动化 workflow engine 内容。 |
| Fixed material case scan | PASS | 未新增具体材料案例。 |
| Universal parameter scan | PASS | 未新增固定 cutoff、kmesh、smearing、U、vacuum 或 grid 推荐。 |
| High-risk overclaim scan | PASS | 未新增把 DFT/QE 结果写成无边界物理结论的表述。 |
| Merge recommendation | READY | Batch G 可作为 v0.1 release-readiness PR 合并。 |
