# QE 快速学习路线图

## 1. 这条路线解决什么问题？

目标不是在最短时间内背下所有 QE 参数，而是尽快形成可靠的计算闭环：能构造 input，能运行，能读 output，能判断是否可信，能知道下一步是否允许继续。

QE 学习最危险的误区是只复制 tutorial input。input 文件能跑通，只说明语法和环境没有立即失败；它不能说明赝势合适、cutoff 收敛、k 点足够、smearing 合理、结构稳定，或 phonon 结果有物理意义。

## 2. 1 周内应该掌握什么？

第一周只追求一个目标：能把一个简单晶体的 `pw.x scf` 跑成可解释的结果。

必须动手跑：

- 读取一个结构，手写或改写 `pw.scf.<system>.in`。
- 选择同一来源、同一泛函族的赝势。
- 设置 `ecutwfc`、`ecutrho`、`K_POINTS automatic`。
- 跑一次 SCF，读懂总能、电荷密度收敛、Fermi energy、k 点数量、赝势加载信息。
- 改变 `ecutwfc` 和 k 点，观察总能变化。

必须理解：

- SCF 是 Kohn-Sham 方程与电子密度之间的自洽过程。
- `conv_thr` 是电子自洽阈值，不是结构优化阈值。
- `ecutwfc` 控制波函数平面波基组，`ecutrho` 控制电荷密度/势的表示。
- k 点采样影响总能、DOS、金属性判断和力。
- 金属体系不能随便使用绝缘体 occupation；smearing 会影响能量、力和收敛。

可以后置：

- DFPT 细节、Wannier90、AiiDA、EPW、缺陷热力学、复杂 HPC 自动化。

## 3. 2-4 周应该掌握什么？

第二阶段要从“单个 SCF”扩展到“结构优化与电子结构 workflow”。

必须动手跑：

- `ecutwfc / ecutrho` 收敛性测试。
- k 点收敛性测试。
- `relax` 与 `vc-relax`，并比较优化前后的力、应力、晶格参数。
- `SCF -> bands -> bands.x`。
- `SCF -> NSCF -> dos.x / projwfc.x`。

必须理解：

- `relax` 优化原子位置，`vc-relax` 还优化晶胞；低维材料不能无脑放开所有晶胞自由度。
- bands 的高对称路径和 DOS 的均匀 k 网格不是同一种采样。
- `nbnd`、smearing、k 点密度会影响 bands/DOS/PDOS 的可解释性。
- `prefix` 和 `outdir` 是 workflow 的数据边，不是随便填的字符串。

常见错误路线：

- 只用 tutorial 默认 cutoff，不做任何收敛测试。
- 用 bands 路径去算 DOS。
- 用未 relax 的结构直接解释 phonon 虚频。
- output 里看到 `JOB DONE` 就认为科学结果可用。

## 4. 1-2 个月应该掌握什么？

第三阶段进入 DFPT、后处理、HPC 和可复现记录。

必须动手跑：

- `SCF -> ph.x` 的 Gamma 点 phonon。
- `SCF -> ph.x(ldisp) -> q2r.x -> matdyn.x` 的 phonon dispersion。
- `pp.x` 输出 charge density / potential 等后处理数据。
- 在本地或集群上跑带 `prefix/outdir`、日志、脚本和记录模板的完整小项目。

必须理解：

- phonon 不是普通后处理，而是 DFPT 线性响应计算，依赖高质量 SCF 和接近平衡的结构。
- Gamma 点 phonon 与 q-grid phonon 的目标不同。
- `ph.x` 生成 dynamical matrices，`q2r.x` 转换为 real-space IFC，`matdyn.x` 插值色散或 DOS，`dynmat.x` 更偏 Gamma 点模式分析。
- ASR 可以修正声学支在 Gamma 附近的数值漂移，但不能替代收敛性和结构稳定性。
- negative frequency 可能是真实结构不稳定，也可能来自未收敛结构、cutoff/k/q 网格不足、SCF 阈值太松或低维体系处理错误。

可以后置：

- EPW、电声耦合超导、Wannier 插值、AiiDA 高通量、缺陷形成能完整修正。

## 5. 理论最低补充顺序

优先补会直接影响 input/output 的理论：

1. Kohn-Sham DFT 与 SCF。
2. 平面波基组、`ecutwfc`、`ecutrho`。
3. 赝势类型、来源、transferability。
4. Brillouin zone、Monkhorst-Pack k 点、高对称路径。
5. smearing 与金属体系。
6. SCF mixing 与数值收敛。
7. symmetry、primitive/conventional cell、k-path 标准化。
8. DFPT 与 phonon。

## 6. 后续资料

- 本地调研：`Quantum ESPRESSO as a Modern Research Stack.md`
- 本地调研：`Quantum ESPRESSO Tutorial Website Ecosystem.md`
- QE `pw.x` input reference: <https://www.quantum-espresso.org/Doc/INPUT_PW.html>
- QE `ph.x` input reference: <https://www.quantum-espresso.org/Doc/INPUT_PH.html>

