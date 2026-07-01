# QE-Learning v0.1 Reference Handbook Release Notes

## Scope

v0.1 将 QE-Learning 固化为 Quantum ESPRESSO 中文参考手册和 DFT / DFPT / 固体计算知识体系的基础版本。它面向科研人员学习 QE 原生命令行 workflow、阅读 input/output、做数值收敛、判断结果可信度和维护可复查科研记录。

## What is included

- 项目入口、学习路径、目录职责和 handbook index。
- Ground-state、electronic、phonon / DFPT 三条主线 workflow 的 output review 和下游准入框架。
- `theory-minimum/` 的 DFT、倒空间、能带/DOS、赝势、cutoff、smearing、DFPT phonon、Born charge、磁性/SOC/DFT+U 等最低理论回查层。
- `physics-judgement/` 的 band gap、泛函、赝势、U、SOC、vdW、work function、Wannier、EPC、激发态、free energy 和 uncertainty 判断边界。
- `references/` source spine 和 `standards/` 中的 PASS/WARN/BLOCK、output review、calculation record、citation/source policy。

## What is not included

- 具体材料案例库。
- 可直接复制的万能 input 模板。
- 固定 cutoff、kmesh、smearing、q-grid、vacuum、Wannier window 或 U 值推荐。
- 自动化 agent runtime、MCP schema、VibeDFT 工具文档或 workflow engine。
- 完整 Wannier、EPW、GW/BSE、MD、NEB 或 finite-temperature 教程。

## Major content areas

- `learn/`：按能力目标和可验证输出组织学习路径。
- `workflows/`：按 QE 原生命令行程序链组织 input/output 审阅。
- `theory-minimum/`：解释 workflow 准入所需的最低理论。
- `physics-judgement/`：把异常 output 和高风险结论转化为可信度判断。
- `references/`：维护官方文档、工具文档和 canonical literature 的入口。
- `standards/`：统一记录、命名、引用和 QA 标准。
- [HANDBOOK_INDEX.md](HANDBOOK_INDEX.md)：按读者目标快速定位仓库页面。

## Validation performed

Release-candidate PR 应在合并前完成：

- `git diff --check`
- 全仓库 Markdown 本地链接检查
- 私有路径和本地研究文档路径残留扫描
- agent/runtime/MCP/VibeDFT scope drift 扫描
- 固定材料案例和万能参数扫描
- 高风险 overclaim 扫描
- forbidden directory 检查

## Known limitations

- 部分 physics-judgement 编号页与快速判断页仍有双轨维护成本。
- canonical bibliography metadata 仍适合后续抽样核验。
- 外部链接可在后续 source verification pass 中做在线抽查。
- 新增理论深度页面仍需要逐页专家审阅，而不是一次性宣称最终完备。

## Future work

- 继续 Issue #4 风格的小范围专家精修：每次只处理 1-2 个高风险页面。
- 做 readability pass，减少重复边界说明并提高连续阅读体验。
- 做 external source verification，抽查官方文档、工具文档和 canonical literature 链接。
- 根据使用反馈补充 handbook navigation 和 glossary。

## Release recommendation

如果 release-candidate PR 的 Final QA Gate 通过，建议打 tag：

```text
v0.1-reference-handbook
```
