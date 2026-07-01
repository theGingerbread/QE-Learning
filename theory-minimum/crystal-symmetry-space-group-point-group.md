# Crystal symmetry, space group and point group

## 本页解决什么问题

QE 会根据输入结构、晶胞、原子坐标、磁性、SOC、约束和数值容差识别或使用对称性。对称性影响 irreducible k-points、band degeneracy、phonon irreducible representations、selection rules、Berry/Wannier 分析和许多 output 的可解释性。本页给出空间群、点群、小群和倒空间对称性的最低背景，帮助读者知道什么时候应信任 symmetry reduction，什么时候需要重新审阅结构和路径。

## 物理图像

晶体对称性描述哪些操作会把晶体映射回自身。平移对称性给出晶格；点群描述旋转、镜面、反演等不含平移的点操作；空间群把点操作与平移或分数平移部分组合起来，包括螺旋轴和滑移面等 nonsymmorphic 操作。电子和声子的本征态会按这些对称性分类，因此对称性不仅节省计算量，也决定简并、选择定则和 band/path 标记。

三组概念需要分清：

- 空间群：当前晶体结构的完整实空间对称性，依赖晶胞、原子坐标、元素/占位和识别容差；磁性构型、SOC、noncollinear 设置和 symmetry flags 会改变 QE 在当前 Hamiltonian 中实际可用的 symmetry branch 和小群解释。
- 点群：空间群操作去掉平移信息后保留下来的点操作集合，常用于理解张量、选择定则和高对称方向。
- 小群：对某个具体 `k` 点或 `q` 点而言，把该点映射回自身等价点的对称操作集合；它不是整块晶体的全局标签，而是沿 band path 或 phonon q-point 逐点变化的分类对象。

倒空间继承实空间对称性。某个 `k` 点在对称操作下可能被映射到另一个等价 `k` 点；QE 可以只计算 irreducible wedge 中的代表点，再用 weights 完成 BZ integration。沿 high-symmetry path 画 bands 时，路径上的端点和线段通常对应高对称点、轴或面；这些标签只有在结构 convention 和 symmetry 与 path 来源一致时才有意义。

小群的操作含义是：在当前 Hamiltonian 和当前结构下，找出所有满足 `R k = k + G` 的对称操作，并用这些操作给该 `k` 点上的本征态分类。高对称点的小群通常大于一般路径点的小群，因此更容易出现 symmetry-protected degeneracy 或可标记的 irreducible representations；沿线段离开端点后，小群可能降低，简并也可能允许打开。`bands.x lsym` 给出的 `filband.rap` 是这类小群分类的程序证据，但它只说明 QE 在该输入和该波函数数据链上完成了 representation classification，不自动证明 band crossing 的拓扑性质、实验归属或路径标签本身有效。SOC、noncollinear magnetism、磁性构型或结构畸变会改变可用小群，因此同一条 path 在不同模型下不能机械复用解释。

## 最低数学结构

一个空间群操作可以概念性写成：

```text
r -> R r + tau
```

其中 `R` 是旋转、镜面或反演等点操作，`tau` 是平移部分。倒空间中 `k` 的等价性来自 `R k` 与 `k + G` 的关系。若某个操作把 `k` 映射回等价点，它属于该 `k` 点的小群；若只能把 `k` 映射到另一个不同的等价采样点，它可用于 BZ reduction，但不能直接作为该点的 irreducible-representation 分类操作。

## QE 中的对应对象

| 对象 | QE 位置 | 含义 | output 证据 |
|---|---|---|---|
| `ibrav` / `CELL_PARAMETERS` | `pw.x` input | 定义晶胞与对称性识别基础 | cell、symmetry operations |
| `ATOMIC_POSITIONS` | `pw.x` input | 原子坐标决定实际 symmetry | equivalent atoms、symmetry summary |
| `nosym` / `noinv` | `&SYSTEM` | 控制 symmetry 使用 | irreducible k-points、symmetry section |
| spin / SOC settings | `nspin`、`noncolin`、`lspinorb` | 改变 time-reversal、spin rotation 和可用 symmetry | spin/SOC output、symmetry reduction |
| `bands.x lsym` | `bands.x` | 按当前 `k` 点小群给 bands 做 irreps / small-group classification | `filband.rap` |
| phonon irreps | `ph.x` / `dynmat.x` | Gamma 或 q-point 模式分类 | irreducible representations、mode labels |

## Output 中的可见证据

- `pw.x` setup 中的 symmetry operations 和 equivalent atoms 显示 QE 识别到的结构对称性。
- irreducible k-points 与 full mesh 的比例显示 symmetry reduction 是否生效。
- `bands.x` 在 `lsym=.true.` 时会把 bands 按 `k` 点小群的 irreducible representations 分类，并写出 `filband.rap`；这是分类证据，不是 band ordering、拓扑诊断或实验 assignment 的独立证明。
- `ph.x` 的 irreps 和 mode symmetry 支持 Gamma modes、IR/Raman activity 或 mode assignment 的最低审阅。
- SOC/noncollinear 输出和 warning 必须与 symmetry 使用一起审阅。

## Band path 标签有效性证据

High-symmetry labels 不是输入文件里的装饰文本。一个 band path 标签可以用于解释前，应至少能追踪以下证据：

- current cell：band path 对应的是当前用于 final SCF / bands 的晶胞和原子坐标，而不是 relax 前或另一个分支的结构。
- standardized convention：若 path 来自 SeeK-path、spglib 或文献 convention，记录所用标准化晶胞、坐标 convention 和标签 convention。
- path source：记录 path 生成工具、文档或人工来源；若手写路径，应说明它对应哪一套 reciprocal basis。
- symmetry branch：记录 `nosym`、`noinv`、spin、SOC、noncollinear、磁性构型和约束是否与生成 path 时的 symmetry 假设一致。
- post-relax review：relax 或 vc-relax 后重新检查 cell、space-group/symmetry summary、irreducible k-points 和 high-symmetry label 是否仍匹配。

缺少这些证据时，band 曲线仍可作为能量沿某组 `k` 点的图，但高对称点名称、简并解释和 small-group labels 只能作为未确认信息。

## 对 workflow 的影响

- k-point convergence 需要记录 full mesh、shift 和 irreducible points。
- bands path 需要与结构标准化、cell convention 和 symmetry 保持一致。
- band labels 和 `filband.rap` 需要同时审阅：前者证明路径命名来源，后者证明当前数据链的 small-group classification。
- DOS/PDOS 通常更依赖 uniform mesh；symmetry 影响 weights 和投影通道。
- phonon irreps、acoustic modes、Raman/IR activity 都依赖 symmetry。
- SOC 和磁性会改变 degeneracy、path labels、Fermi surface 和 band crossing 解释。

## 常见误解

- 看到 symmetry reduction 就认为结构正确。
- cell 或原子坐标轻微变化后仍沿用旧 high-symmetry path。
- 开启 SOC 后仍用无 SOC 的简并关系解释 bands。
- 关闭 symmetry 后不记录原因，导致 k-point、DOS 或 phonon 结果不可复查。
- 把 `bands.x` symmetry label 当作可独立发表的结论。
- 把 `filband.rap` 的存在当作 path label 已经有效；它只能证明当前 `bands.x` 做过分类，不能证明路径来源和 cell convention 正确。

## 判断边界

对称性审阅的目标是确认计算对象和解释语言一致。若结构来源、cell convention、磁性、SOC 或 symmetry flags 改变，应重新检查 k-path、irreducible k-points、band degeneracy 和 phonon mode labels。若 output symmetry 与预期不符，应先进入 `WARN` 或 `BLOCK`，回到结构、坐标容差、磁性和 SOC 设置排查。

## PASS / WARN / BLOCK 关联

| 状态 | 最低证据 | 下游边界 |
|---|---|---|
| `PASS` | 当前 cell、原子坐标、spin/SOC/磁性分支和 symmetry flags 可追踪；`pw.x` symmetry summary、equivalent atoms、irreducible k-points 与目标 workflow 一致；band path 来源、standardized convention 和 post-relax review 已记录；若使用 `bands.x lsym`，`filband.rap` 与当前 bands 数据链一致 | 可进入 symmetry-aware bands、phonon irreps、selection-rule 或 label-based 解释，但结论仍限于已声明模型 |
| `WARN` | 计算完成但 path 来源、cell convention、post-relax symmetry review、SOC/磁性分支或 `filband.rap` 对齐证据不完整；symmetry reduction 与预期有差异但可继续排查 | 只允许探索性绘图和诊断；不得把高对称标签、简并关系或 irreps 当最终结论 |
| `BLOCK` | cell/path convention 错配；relax 后沿用旧 path 而未复核；`nosym`/`noinv`、spin/SOC/磁性设置与解释分支冲突；output symmetry 异常未解释；`filband.rap` 来自错误 `prefix/outdir` 或被当作拓扑/实验证明 | 不允许进入 label-based band、phonon mode 或 symmetry-protected 结论，必须先修复结构、路径或文件链 |

## 对应 workflow

- [k-point convergence](../workflows/ground-state/kpoint-convergence.md)
- [bands](../workflows/electronic/bands.md)
- [PDOS](../workflows/electronic/pdos.md)
- [Gamma phonon](../workflows/phonon/gamma-phonon.md)
- [IR/Raman](../workflows/phonon/ir-raman.md)
- [SOC and symmetry boundary](../physics-judgement/soc-and-symmetry-boundary.md)

## 资料来源

- QE INPUT_PW reference: <https://www.quantum-espresso.org/Doc/INPUT_PW.html>
- QE INPUT_BANDS reference: <https://www.quantum-espresso.org/Doc/INPUT_BANDS.html>
- QE INPUT_PH reference: <https://www.quantum-espresso.org/Doc/INPUT_PH.html>
- SeeK-path documentation: <https://seekpath.readthedocs.io/>
