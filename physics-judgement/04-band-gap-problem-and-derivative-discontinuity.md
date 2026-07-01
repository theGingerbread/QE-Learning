# Band Gap Problem and Derivative Discontinuity

## 1. 这个主题解决什么判断问题？

本页帮助判断 QE bands/DOS 中的 Kohn-Sham gap 能解释什么，不能解释什么。重点是把 DFT-level band gap、fundamental gap、optical gap 和 quasiparticle/excited-state 结论分开，避免从普通 bands 或 DOS 图直接推出超出证据层级的结论。

## 物理图像

Kohn-Sham band structure 给出的是辅助单粒子方程的 eigenvalue dispersion。它对理解价带、导带、能带色散和金属性很有用，但 Kohn-Sham gap 不是一般意义上的 fundamental gap。Fundamental gap 对应加一个电子和移走一个电子所需能量之差，通常与 quasiparticle addition/removal energy 相关；optical gap 对应光吸收中的最低允许激发，还可能受到电子-空穴相互作用和激子效应影响。普通 bands/DOS 图只处在 DFT-level electronic structure 这一层。

Derivative discontinuity 是 band-gap problem 的核心概念之一。精确 DFT 的 exchange-correlation potential 在电子数跨过整数时存在不连续项，Kohn-Sham gap 加上这个不连续贡献才与 fundamental gap 对应。常见 semilocal functional 对这个贡献处理不足，同时还可能有 self-interaction 和 delocalization error，使电子态过度离域、gap 偏小或态位置不合理。

这并不意味着某个方向的误差可以机械套用到所有体系。小带隙体系、磁性体系、含 SOC 的体系、DFT+U/hybrid 模型和 GW/BSE 结果都可能改变 gap 解释。QE 用户需要把 band plot、DOS、Fermi level、occupation、SOC/U/functional、k path、uniform mesh、`nbnd` 和 energy zero 放在同一证据链里，而不是只从一张图读出一个无边界数字。

## 3. DFT/QE 中的近似来源

误差来自 exchange-correlation approximation、有限 k mesh、SOC、DFT+U/hybrid/GW 模型选择、DOS 展宽、`nbnd` 覆盖不足和能量零点处理。数值误差会让 VBM/CBM 搜索、DOS 边缘或 Fermi crossing 不稳定；模型误差会让 DFT-level gap 与 fundamental/optical gap 的关系发生系统偏差。

## 4. 相关 QE 输入字段

| 字段 | 程序 | 判断意义 | 常见误用 |
|---|---|---|---|
| input_dft | pw.x | 定义交换关联或近似模型 | 把模型选择当作单纯数值收敛 |
| ecutwfc/ecutrho | pw.x | 确认基组误差不会主导判断 | 换物理模型后沿用旧 cutoff |
| `K_POINTS crystal_b/tpiba_b` | `pw.x bands` | high-symmetry path 是否能展示目标 dispersion | 用路径 gap 代替全 BZ gap |
| `K_POINTS automatic` | `pw.x nscf` | DOS/uniform mesh 是否支撑 BZ 统计和 band edge 线索 | 用 bands path 替代 DOS mesh |
| occupations/smearing/degauss | pw.x/dos.x | 控制占据和费米面附近积分 | 用过大 smearing 解释物理趋势 |
| nbnd | pw.x | 未占据带是否足以覆盖目标能区 | 带数不足却解释导带 |
| dos.x Emin/Emax/DeltaE | dos.x | 能量窗和分辨率是否足够 | DOS 能量零点不清 |
| Fermi level / VBM / CBM / energy zero | output / plot script | gap 读数和能量对齐是否可复查 | 混用零点后比较 gap 或峰位 |

## 5. output review 中的迹象

| output 迹象 | 可能含义 | 需要回查 |
|---|---|---|
| functional / pseudopotential 回显 | 模型是否与记录一致 | input、UPF、source record |
| SCF / perturbation convergence | 数值解是否达到当前目标 | conv_thr、tr2_ph、mixing |
| warning / symmetry / occupation 信息 | 物理模型或边界条件可能不一致 | workflow record 和 output review |
| bands gap 与 DOS gap 不一致 | k-path、mesh、smearing 或能量零点问题 | bands/DOS workflow |
| VBM/CBM 只来自路径图 | 可能漏掉路径外 extrema | NSCF mesh、DOS 边缘、k-path 来源 |
| 导带窗口被截断 | `nbnd` 不足，CBM 或高能特征不可审阅 | NSCF/bands output 中 band 数量 |
| 小带隙随 SOC 或泛函改变符号 | 拓扑/半金属判断敏感 | SOC、functional、k sampling |
| DFT gap 与实验差距大 | Kohn-Sham gap 解释边界 | hybrid/GW/BSE 或实验对照 |

## 6. 对 workflow 的影响

- [workflows/electronic/bands.md](../workflows/electronic/bands.md)
- [workflows/electronic/dos.md](../workflows/electronic/dos.md)
- [workflows/advanced/hybrid-functional-overview.md](../workflows/advanced/hybrid-functional-overview.md)

## 7. PASS / WARN / BLOCK 判断

| 状态 | 条件 | 允许进入的下游 |
|---|---|---|
| PASS | 已明确这是 DFT-level / KS-level gap 或 metallicity statement；bands path、DOS uniform mesh、`nbnd`、Fermi level、VBM/CBM、energy zero、SOC/smearing 和模型边界均可复查 | 进入带边界的带隙趋势、相对比较或 workflow 交叉解释 |
| WARN | gap 对 k mesh、SOC、泛函、U、smearing、`nbnd` 或 path 覆盖敏感；缺少 GW/BSE/实验对照 | 只作为趋势、筛选或内部判断 |
| BLOCK | 把普通 DFT KS gap 当定量实验 gap、quasiparticle gap 或 optical gap；用 bands path 漏采样结果直接下结论；energy zero 不明 | 停止正式 gap 解释 |

## 8. 常见误区

- 把 Kohn-Sham gap 当作实验 fundamental gap
- 把 Kohn-Sham gap 当作 quasiparticle gap 或 optical gap
- 用 DOS smearing 造成的尾态判断金属性
- 忽略 SOC 对小带隙的影响
- 用 bands path 漏掉真实 VBM/CBM
- 忽略 `nbnd` 不足导致的导带窗口截断
- 把 scissor 当作自洽物理修正

## 9. 与前沿常识的关系

普通 DFT gap 常可作趋势；定量光谱或准粒子 gap 通常需要 hybrid、GW/BSE 或实验对照。小带隙和拓扑判断必须额外审阅 SOC、k mesh 和对称性。

## 10. 最低掌握深度

- 能区分 Kohn-Sham gap、fundamental gap 和 optical gap。
- 能检查 bands path 是否可能漏掉 VBM/CBM，DOS dense mesh 是否支持 gap 判断，以及 `nbnd` 是否覆盖目标导带窗口。
- 能说明普通 DFT gap 何时只适合作为趋势，何时需要 hybrid、GW/BSE 或实验对照。
- 能识别 smearing、SOC 和小带隙体系对 gap 判断的风险。

## 11. 对应仓库页面

- [theory-minimum/kpoints-symmetry-kpath.md](../theory-minimum/kpoints-symmetry-kpath.md)
- [theory-minimum/band-structure-and-dos.md](../theory-minimum/band-structure-and-dos.md)
- [theory-minimum/magnetism-soc-dftu.md](../theory-minimum/magnetism-soc-dftu.md)
- [workflows/electronic/bands.md](../workflows/electronic/bands.md)
- [workflows/electronic/dos.md](../workflows/electronic/dos.md)
- [workflows/advanced/hybrid-functional-overview.md](../workflows/advanced/hybrid-functional-overview.md)
- [standards/output-review-checklist.md](../standards/output-review-checklist.md)
- [standards/pass-warn-block.md](../standards/pass-warn-block.md)
- [references/source-index.md](../references/source-index.md)


## 结论强度

- Strong：本页中由 DFT/DFPT 基础理论、经典方法论文或 QE 官方文档直接支撑的判断。
- Moderate：本页中由综述、方法摘要或多个来源共同支持，但细节需要回到正文或官方文档核验的判断。
- Boundary：本页中用于限制解释范围的判断，不作为定量结论。
- Version-sensitive：涉及 QE、PHonon、Wannier90、EPW、Yambo 或其他工具字段和行为的判断，必须按当前官方文档复查。

## 12. 资料来源

- [Perdew, Parr, Levy and Balduz, Phys. Rev. Lett. 49, 1691 (1982)](https://doi.org/10.1103/PhysRevLett.49.1691)
- Mori-Sanchez, Cohen and Yang, Current limitations of density functional theory.
- [Onida, Reining and Rubio, Rev. Mod. Phys. 74, 601 (2002)](https://doi.org/10.1103/RevModPhys.74.601)
- [QE INPUT_PW](https://www.quantum-espresso.org/Doc/INPUT_PW.html)
