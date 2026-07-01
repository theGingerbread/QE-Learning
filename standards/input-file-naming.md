# QE 文件命名规范

## 1. 命名目标

QE workflow 依赖许多 side-effect 文件。命名规范让文件名直接表达：

- 使用哪个 QE 程序。
- 属于哪个计算阶段。
- 对应哪个体系。
- 是 input、output 还是中间数据。

文件名服务人类复查；`prefix/outdir` 服务 QE 程序之间读取 scratch 数据。二者可以相关，但不能互相替代。文件名清楚并不能证明 `prefix/outdir` 没有混用；`prefix/outdir` 一致也不能替代 input/output 文件的人工记录。

## 2. 基本格式

```text
<program-or-postproc>.<stage>.<system>.<ext>
```

其中：

- `<program-or-postproc>`：`pw`、`ph`、`q2r`、`matdyn`、`dynmat`、`dos`、`projwfc`、`bands`、`pp`
- `<stage>`：`scf`、`relax`、`vc-relax`、`bands`、`nscf`、`dos`、`pdos`、`phonon`、`density`，也可以在后处理程序名已经唯一表达 stage 时省略重复词
- `<system>`：短体系标识，例如 `<system>`、`<system_phase>`、`<system_variant>`
- `<ext>`：`in`、`out`、`dat`、`freq`、`fc`、`dyn`

## 3. 推荐命名

```text
pw.scf.<system>.in
pw.scf.<system>.out
pw.relax.<system>.in
pw.relax.<system>.out
pw.vc-relax.<system>.in
pw.vc-relax.<system>.out
pw.nscf.<system>.in
pw.nscf.<system>.out
pw.bands.<system>.in
pw.bands.<system>.out
bands.<system>.in
bands.<system>.out
bands.<system>.dat
dos.<system>.in
dos.<system>.out
dos.<system>.dat
projwfc.<system>.in
projwfc.<system>.out
ph.<system>.in
ph.<system>.out
q2r.<system>.in
q2r.<system>.out
matdyn.<system>.in
matdyn.<system>.out
dynmat.<system>.in
dynmat.<system>.out
pp.density.<system>.in
pp.density.<system>.out
pp.potential.<system>.in
pp.potential.<system>.out
pp.elf.<system>.in
pp.elf.<system>.out
```

说明：`pw.*` 文件通常需要同时写出 `program` 和 `stage`，例如 `pw.scf.<system>.in`。`bands.x`、`dos.x`、`projwfc.x`、`q2r.x`、`matdyn.x`、`dynmat.x` 等后处理程序名已经表达 stage，文件名可以写成 `bands.<system>.in` 或 `matdyn.<system>.in`，也可以按项目需要写成 `bands.bands.<system>.in` 这类更冗余但更机器可分的格式。无论采用哪种风格，record 中必须能反查程序、stage、上游文件链和 `prefix/outdir`。

如果同一 `<system>` 存在不同结构状态、functional、pseudopotential、SOC、U、vdW、charge state 或 slab boundary，不要只靠同一个短名区分。应在 `<system>` 或子目录中加入稳定、可读的状态标识，并在 calculation record 中写清对应设置。文件名不应写成材料专属算例；这里的 `<system>` 只是占位符。

## 4. 目录建议

```text
calculations/
  <system>/
    00-structure/
    01-scf/
    02-convergence/
    03-relax/
    04-electronic/
      bands/
      dos/
      pdos/
    05-phonon/
      gamma/
      dispersion/
    06-postprocessing/
    record.md
```

这个目录建议是以 workflow 阶段为中心的细分布局；[project-layout.md](project-layout.md) 给出的是个人项目顶层布局。二者可以嵌套使用：顶层 `inputs/outputs/records/` 保存长期证据，`calculations/<system>/01-scf/` 等子目录用于组织某个体系或某轮计算的具体文件。不要把同一次计算的 record 拆散到两个互不引用的位置；若使用嵌套布局，应在项目 `README.md` 或 record 中写明索引关系。

## 5. `prefix` 与文件名的关系

`prefix` 是 QE scratch 数据的逻辑标识，文件名是 GitHub 记录的可读标识。二者可以相同，但不要混淆：

- 文件名用于人和 Git 追踪。
- `prefix/outdir` 用于 QE 程序之间读取数据。

建议：

- 探索性计算用独立 `prefix/outdir`。
- 生产计算不要复用旧 scratch，除非明确是 restart。
- 下游 workflow 的 `record.md` 必须写清楚读取的是哪个 SCF 的 `prefix/outdir`。
- relax/vc-relax 后进入 bands、DOS、phonon、work function 或 advanced workflow 前，应给 final static SCF 使用可追踪的文件名和 `prefix/outdir`，避免直接沿用优化过程中的临时数据。
- NSCF、DOS、PDOS、Fermi surface、q2r、matdyn、dynmat 等后处理文件应能从文件名或 record 中反查上游 SCF/NSCF/ph.x 数据链。

## 6. 命名错误的 PASS / WARN / BLOCK 后果

文件命名本身不决定物理可信度，但它会决定 output review 是否可复查。命名和 `prefix/outdir` 记录不足时，状态应按数据链风险降级：

| 状态 | 命名与文件链条件 | 下游影响 |
|---|---|---|
| PASS | input、output、后处理文件、`prefix/outdir` 和 record 能一一对应；不同结构状态、functional、PP、SOC、U、vdW 或 boundary 分支可区分 | 可进入记录中列出的下游 |
| WARN | 文件名可读但缺少部分模型/结构状态标识；record 能补足来源和下游读取关系 | 只能进入低风险探索或补充审阅 |
| BLOCK | output 无法对应 input/command；旧 scratch 或旧后处理文件可能混入；不同模型或结构状态文件名不可区分且 record 不能补救 | 停止下游，重建文件链或重新运行 |

典型 `BLOCK` 情况包括：`pw.scf.*.out` 实际来自另一个 input、DOS 文件读取了旧 `prefix/outdir`、relax 后的 final static SCF 没有独立命名、SOC/U/vdW 分支覆盖了无 SOC/无 U/无 vdW 输出。此类问题不是物理误差，而是 workflow provenance 失效。

## 资料来源

- [calculation-record-template.md](calculation-record-template.md)：支持把文件名、`prefix/outdir` 和 output evidence 写入 record；不替代实际 output review。
- [project-layout.md](project-layout.md)：支持把命名规范放进个人项目结构；不规定本仓库保存具体计算文件。
- [QE INPUT_PW](https://www.quantum-espresso.org/Doc/INPUT_PW.html)：支持 `prefix/outdir`、`pseudo_dir` 等 QE 字段含义核对；不规定人类可读文件名。
