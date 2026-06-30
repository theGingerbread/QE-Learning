# NSCF workflow

## 页面定位

- 对应学习路线：[learn/05-electronic-structure-loop.md](../../learn/05-electronic-structure-loop.md)
- 上游依赖：SCF ground state
- 下游用途：DOS / PDOS / Fermi surface / dense eigenvalue analysis
- 规范入口：[standards/calculation-record-template.md](../../standards/calculation-record-template.md)、[standards/pass-warn-block.md](../../standards/pass-warn-block.md)

## 计算目标

在已收敛 SCF 基础上，用更密的 k 网格或更多能带生成电子态数据，供 DOS、PDOS、费米面或其他后处理读取。

## 输入前提

- `<structure>`、`<pseudo>`、`<system>` 和上游 workflow 已记录。
- cutoff、k 点、occupation、收敛阈值和物理模型与本 workflow 目标一致。
- 已明确本 workflow 的目标性质、准入条件和下游用途。

## 计算图

```text
<SCF ground state>
  -> pw.x
  -> <intermediate_state>
  -> <reviewed_output>
```

## 需要的 QE 程序

`pw.x`

## 通用输入模板

```text
<program>.<workflow>.<system>.in

<namelist_or_cards>
  calculation_or_task = 'nscf'
  prefix = '<system>'
  outdir = '<scratch_dir>'
  <input_dependency> = '<upstream_output>'
  <key_parameter> = <value>
```

## 输入字段说明

| 字段 | 所属程序 | 作用 | 常见风险 | 输出中如何验证 |
|---|---|---|---|---|
| `calculation` | pw.x | 设置为 'nscf'，读取 SCF 电荷密度并在指定 k 点求本征值 | 把 NSCF 当作新的 SCF ground state | output 显示 non self-consistent calculation |
| `nbnd` | pw.x | 控制计算能带数 | 导带范围不足导致 DOS/PDOS 截断 | output 显示 number of Kohn-Sham states |
| `K_POINTS` | pw.x | 通常使用比 SCF 更密的 uniform mesh | 沿 bands path 做 DOS | output 显示 k 点数量和不可约 k 点 |

## 通用输出审阅模板

```markdown
## Output Review

- Program:
- Calculation type:
- QE version:
- Input dependency:
- Structure summary:
- Pseudopotentials loaded:
- Cutoff reported:
- K-points reported:
- Convergence status:
- Main numerical result:
- Warnings:
- Scratch / restart status:
- PASS / WARN / BLOCK:
- Reason:
- Allowed downstream workflows:
```

## 输出判断标准

- 程序正常结束只代表执行完成；还需要检查关键输出、warning 和上游依赖是否一致。
- 结果进入下游前，应能说明本 workflow 的目标量、数值设置和物理模型没有互相冲突。
- PASS / WARN / BLOCK 判断必须引用 output 中的具体证据。

## 收敛性要求

- 上游 SCF 或结构优化应满足本 workflow 的目标精度。
- cutoff、k 点、smearing、q-grid 或高级模型参数需要围绕目标量检查敏感性。
- 如果本页只是高级边界页，应记录哪些收敛测试必须在专门 workflow 中完成。

## 常见错误与诊断

| 现象 | 可能原因 | 优先排查 |
|---|---|---|
| 程序完成但结果不可解释 | 上游依赖、参数或物理模型记录不足 | 先核对 input、output header、scratch 和 record |
| 下游读取失败 | `prefix/outdir`、文件前缀或中间文件不一致 | 检查文件名、路径和 output 中的读取信息 |
| 数值趋势不稳定 | cutoff、k 点、smearing、q-grid 或模型参数未收敛 | 回到对应 convergence workflow |

## 通用学习模板

使用 `<system>`、`<structure>`、`<pseudo>`、`<workflow>`、`<upstream_output>` 等占位符记录个人学习任务。本仓库只提供通用审阅框架，不保存具体计算结果。

## 记录模板

```text
<program>.<workflow>.<system>.in
<program>.<workflow>.<system>.out
record.md
```

## 与其他 workflow 的关系

- 上游 workflow 决定本页输入是否可信。
- 本页输出只有通过 output review 后才能进入下游。
- 与收敛性相关的问题应回到 `workflows/ground-state/` 或 `workflows/phonon/` 的专门页面处理。

## 后续完善重点

- 补充该 workflow 的 output 段落定位说明。
- 补充 PASS / WARN / BLOCK 判断的通用审阅表。
- 补充与相邻 workflow 的数据依赖检查清单。

## 资料来源

- QE INPUT_PW reference: <https://www.quantum-espresso.org/Doc/INPUT_PW.html>
- QE PostProc documentation: <https://www.quantum-espresso.org/Doc/pp_user_guide/>
