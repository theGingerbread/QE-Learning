# Phase 1 Entry Realignment Report

## Scope

本轮只执行 `PROJECT_BACKFILL_PRIORITY_ROADMAP.md` 的 Phase 1：入口和目录 README 的最小范围修正。修改集中在项目入口、学习路径入口、workflow 入口、最低理论入口、物理判断入口和 standards 入口，目标是让新读者进入仓库时立即理解本项目是 QE 计算参考手册与 DFT / DFPT / 固体计算知识体系。

本轮不进入主线 workflow 正文回填，不改写 theory-minimum 主题页，不扩写 physics-judgement 主题页，也不整理 source-index 或 canonical literature 的正文内容。

## Files changed

- `README.md`
- `learn/README.md`
- `learn/00-start-here.md`
- `workflows/README.md`
- `theory-minimum/README.md`
- `physics-judgement/README.md`
- `standards/README.md`
- `PHASE1_ENTRY_REALIGNMENT_REPORT.md`

`references/source-index.md` 和 `references/canonical-literature.md` 已复读。当前入口边界足够清楚，本轮没有修改。

## Main alignment decisions

- QE reference handbook：根 README 改为更直接的一句话定位，说明 QE-Learning 是面向科研计算的 QE 中文参考手册，而不仅是学习笔记。
- DFT knowledge system：根 README 和 `theory-minimum/README.md` 明确本仓库同时提供 DFT / DFPT / 固体计算的必要理论背景，但理论页只服务 QE input/output 和 workflow 准入。
- Input/output review：`learn/README.md`、`learn/00-start-here.md` 和 `workflows/README.md` 强调每个阶段必须通过 output review、收敛记录和 `PASS / WARN / BLOCK` 判断来证明掌握。
- Convergence：入口层只说明收敛是学习主线和下游准入条件，不在本轮给出具体参数或阈值。
- Result credibility：`physics-judgement/README.md` 明确该目录是结果可信度判断参考层，并将风险类型归为数值误差、模型误差、赝势误差、边界条件误差、后处理误差和 workflow 传播误差。
- Reproducibility：`standards/README.md` 强调 standards 服务个人学习记录、科研计算记录、output review、source boundary、文件命名和 QA，不保存具体计算数据。

## What was intentionally not changed

- 没有做 workflow 正文大回填。
- 没有做 theory-minimum 正文大扩写。
- 没有做 physics-judgement 正文大扩写。
- 没有引入外部执行系统、工具接口规范或非手册型工程内容。
- 没有加入材料绑定算例、真实 input/output 文件或固定参数答案。
- 没有把高级工具写入基础学习路径。
- 没有修改 `references/source-index.md` 和 `references/canonical-literature.md`，因为本轮复读后未发现入口错位需要立即修正。

## Follow-up

下一步进入 Phase 2：主线 workflow 回填。优先处理 `workflows/ground-state/`、`workflows/electronic/` 和 `workflows/phonon/` 中影响下游准入的页面，重点补强 QE 程序链、关键 input 字段、workflow-specific output review、收敛要求、`PASS / WARN / BLOCK` 和来源边界。
