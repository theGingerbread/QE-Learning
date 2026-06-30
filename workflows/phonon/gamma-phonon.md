# Gamma phonon workflow

## 页面定位

- 对应学习路线：[learn/06-phonon-dfpt-loop.md](../../learn/06-phonon-dfpt-loop.md)
- 上游依赖：relaxed structure + strict SCF
- 下游用途：Gamma modes / dielectric-Born branch / IR-Raman
- 规范入口：[standards/calculation-record-template.md](../../standards/calculation-record-template.md)、[standards/pass-warn-block.md](../../standards/pass-warn-block.md)

## 计算目标

在 q=0 计算 Gamma 点声子模式，审阅声学支、模式频率和可能的介电/Born effective charge 分支。

## 输入前提

- `<structure>`、`<pseudo>`、`<system>` 和上游 workflow 已记录。
- cutoff、k 点、occupation、收敛阈值和物理模型与本 workflow 目标一致。
- 已明确本 workflow 的目标性质、准入条件和下游用途。

## 计算图

```text
<relaxed structure + strict SCF>
  -> ph.x, `dynmat.x`
  -> <intermediate_state>
  -> <reviewed_output>
```

## 需要的 QE 程序

`ph.x`, `dynmat.x`

## 通用输入模板

```text
<program>.<workflow>.<system>.in

<namelist_or_cards>
  calculation_or_task = 'gamma-phonon'
  prefix = '<system>'
  outdir = '<scratch_dir>'
  <input_dependency> = '<upstream_output>'
  <key_parameter> = <value>
```

## 输入字段说明

| 字段 | 所属程序 | 作用 | 常见风险 | 输出中如何验证 |
|---|---|---|---|---|
| `tr2_ph` | ph.x | DFPT 响应收敛阈值 | 过松导致频率漂移 | ph output 每个 perturbation 收敛 |
| `epsil` | ph.x | 请求介电张量和 Born effective charges | 在不适用物理条件下开启 | output 中 dielectric/Born 段落 |
| `fildyn` | ph.x/dynmat.x | dynamical matrix 文件 | 文件前缀不一致 | dynmat.x 是否读取成功 |

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

- QE INPUT_PH reference: <https://www.quantum-espresso.org/Doc/INPUT_PH.html>
- QE INPUT_DYNMAT reference: <https://www.quantum-espresso.org/Doc/INPUT_DYNMAT.html>
- Kyoto phonon DokuWiki: <https://www2.yukawa.kyoto-u.ac.jp/~koudai.sugimoto/dokuwiki/doku.php?id=quantumespresso%3Aphonon%3A%E3%83%95%E3%82%A9%E3%83%8E%E3%83%B3%E3%81%AE%E8%A8%88%E7%AE%97>
