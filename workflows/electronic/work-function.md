# Work Function Workflow

## 计算目标

基于 slab 静电势平台和 Fermi level 判断功函数。

## QE 程序 / 外部工具

`pp.x`, `average.x`

## 输入前提

- 已有清楚的 `<structure>`、`<pseudo>`、`<system>` 和上游 workflow 记录。
- 相关 cutoff、k 点、occupation、收敛阈值和物理模型已经记录。
- 已明确本 workflow 的目标性质、准入条件和下游用途。

## 计算图

```text
<upstream_workflow>
  -> <workflow_input>
  -> work-function
  -> <reviewed_output>
  -> <downstream_workflow>
```

## 通用输入模板

```text
<program>.<workflow>.<system>.in

<namelist_or_cards>
  <key_parameter> = <value>
  <input_dependency> = <upstream_output>
```

## 输入字段说明

- `<system>`：个人记录中的体系标识。
- `<workflow>`：当前计算阶段，例如 `nscf`、`dos`、`phonon` 或高级分支名称。
- `<upstream_output>`：上游 SCF、NSCF、relax 或 phonon 数据边。
- `<key_parameter>`：影响物理结果或数值稳定性的关键参数。

## 通用输出审阅模板

```markdown
## Output Review

- Program:
- Calculation type:
- QE version:
- Upstream dependency:
- Key input parameters:
- Output files generated:
- Convergence / completion status:
- Physical quantity reviewed:
- Warnings:
- PASS / WARN / BLOCK:
- Reason:
- Allowed downstream workflows:
```

## 输出判断标准

- 程序正常结束只代表执行完成，还需要检查关键物理量和 warning。
- output 中报告的上游依赖、关键参数和生成文件应与 input 记录一致。
- PASS/WARN/BLOCK 判断应写明证据，不能只写“正常结束”。
- 进入下游前应确认该 workflow 的目标性质已经达到当前学习或科研问题的精度要求。

## 记录模板

```text
<program>.<workflow>.<system>.in
<program>.<workflow>.<system>.out
record.md
```

`record.md` 应记录输入来源、运行命令、环境、关键输出、warning、PASS/WARN/BLOCK 状态和下一步决策。

## 推荐参考资料

- QE INPUT_PW / INPUT_PP / PostProc documentation
