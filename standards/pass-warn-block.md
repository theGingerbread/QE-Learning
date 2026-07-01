# PASS / WARN / BLOCK

## 1. 为什么需要这个标准？

QE output 里出现 `JOB DONE` 只说明程序结束，不说明结果可以进入下游。PASS / WARN / BLOCK 用来把“运行结束”转化为“科学计算状态”。

## 2. 状态定义

| 状态 | 含义 | 是否允许下游 |
|---|---|---|
| PASS | 证据足以支撑当前目标允许的下游或当前层级结论 | 允许进入记录中列出的下游 |
| WARN | 程序完成或结果可用于学习、趋势判断、参数摸底或排错，但存在明确边界，不能写成最终结论 | 只允许进入低风险探索或诊断下游 |
| BLOCK | 关键证据缺失、数据链不一致、收敛失败、模型边界未说明或存在不可接受风险 | 不允许进入依赖该结果的下游 |

`PASS / WARN / BLOCK` 是下游准入 gate，不是情绪标签。每个状态必须写出理由、output 证据和允许或禁止的下游。`JOB DONE`、`convergence has been achieved` 或某一个后处理文件生成成功，都只能作为证据的一部分，不能单独决定最终状态。

SCF convergence 也不等于所有 observable convergence。cutoff、k-point、smearing、force、stress、phonon、work function、Wannier interpolation 或 EPC 等下游目标仍需要各自的 output review 和收敛证据。

## 3. 常见 PASS 条件

- input 来源清楚。
- structure、pseudopotential、cutoff、k-points、smearing 有记录。
- output 中与当前目标相关的 convergence 达标。
- 没有未解释的 warning。
- `record.md` 写清 `Status`、`Reason`、`Evidence`、`Downstream allowed` 和 `Uncertainty statement`。

## 4. 常见 WARN 条件

- 参数只做了初步测试。
- phonon 有小负频但尚未完成收敛排查。
- 结构来源可信但残余力偏高。
- HPC restart 发生过，但结果可追踪。
- 模型边界已记录，但 functional、pseudopotential、U、SOC、vdW 或 boundary sensitivity 尚未完成。
- 当前结果可用于学习或趋势，但不能支撑定量 claim。

## 5. 常见 BLOCK 条件

- SCF 未收敛。
- `prefix/outdir` 混用旧数据。
- 赝势来源不明或泛函混用。
- phonon 输入结构未 relax。
- output 与 input/command 对不上。
- `JOB DONE` 被当作唯一证据。
- 上游为 `BLOCK`，但下游仍继续做 bands、DOS、phonon、work function、Wannier、EPC 或 free-energy 结论。
- Kohn-Sham gap、PDOS、ASR、Wannier spread、coarse-grid EPC 或 total energy 被写成超出当前 evidence level 的物理结论。

## 6. GitHub 记录要求

每个 `record.md` 必须写状态和理由：

```markdown
## Review status

- Status: PASS / WARN / BLOCK
- Reason:
- Evidence:
- Downstream allowed:
- Uncertainty statement:
```

`Status` 是最终审阅状态，不等同于某一个收敛项。`SCF convergence`、cutoff convergence、k-point convergence、phonon convergence 等可以作为 `Evidence` 的一部分，但最终仍需写成一个明确的 `Status` 和下游准入。

`Uncertainty statement` 至少说明 numerical uncertainty、model uncertainty、pseudopotential uncertainty、finite-size/boundary uncertainty 和 workflow propagation uncertainty 中哪些已检查，哪些仍是 WARN 边界。

## 7. 最小审阅句式

建议在每个 record 中使用同一类句式：

```markdown
- Status: PASS
- Reason: 当前目标是 <workflow/objective>；output 中 <evidence> 支持该目标，且 <required convergence/source boundary> 已记录。
- Evidence: <output file>: <key lines or values>
- Downstream allowed: <specific downstream workflows>
- Downstream blocked: <workflows or claims not supported>
- Uncertainty statement: <numerical/model/PP/boundary/workflow limits>
```

如果无法写清 `Evidence` 或 `Downstream allowed`，状态不能写成 `PASS`。

## 8. 来源与版本边界

`PASS / WARN / BLOCK` 的状态理由必须说明证据来源。不同来源支持的判断层级不同：

| 来源类型 | 可支持的判断 | 不能替代什么 | 记录要求 |
|---|---|---|---|
| QE official `INPUT_*` / package docs | 字段含义、程序行为、文件链和 version-sensitive 语法 | 目标物理量是否收敛、模型是否适合体系 | 写明查了哪个官方入口或 package guide |
| QE output / post-processing output | 当前 run 的实际输入回显、收敛状态、warning 和结果文件 | 文献级物理解释或跨模型结论 | 写明 output 文件、关键行或关键数值 |
| canonical literature | DFT/DFPT/PP/Wannier/EPC/excited-state/reproducibility 的方法边界 | 当前 QE 版本字段定义 | 链接到 [canonical-literature.md](../references/canonical-literature.md) 或具体文献骨架 |
| tutorial / tool docs | 学习路径、工具接口和 workflow 辅助理解 | 官方参数定义或最终物理可信度 | 写明只作为教程或工具边界 |
| internal judgement | 本仓库的 `workflow`、`theory-minimum`、`physics-judgement` 和 `standards` 规则 | 外部公开来源 | 写明这是 Boundary / workflow gate，而不是外部定量结论 |

Version-sensitive 字段和程序行为必须以当前官方文档为准。若状态判断依赖 `HUBBARD`、SOC、hybrid、vdW、PHonon、EPW、Wannier90、Yambo 或 post-processing 接口，record 中应写明版本边界；未核对版本时，最多进入 `WARN`。

相关规范：

- [output-review-checklist.md](output-review-checklist.md)
- [calculation-record-template.md](calculation-record-template.md)
- [citation-and-source-policy.md](citation-and-source-policy.md)
- [references/source-index.md](../references/source-index.md)
