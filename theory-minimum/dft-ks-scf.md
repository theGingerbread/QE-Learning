# DFT, Kohn-Sham and SCF

## QE 中对应的问题

SCF 是 `pw.x` 的基础计算问题：在给定结构、赝势、cutoff 和 k 点下求自洽电子密度、总能和 Kohn-Sham 本征值。它决定后续 relax、bands、DOS、PDOS、phonon 和 pp.x 后处理能否读取可信 ground state。

## 常见错误

- 只看 `JOB DONE`，没有检查自洽是否达到阈值。
- 把 Kohn-Sham eigenvalues 直接当作实验准粒子能带解释。
- 忽略 `prefix/outdir`，导致下游读取旧 scratch。
- SCF 振荡时只重复提交，不检查 mixing、smearing、结构或赝势。

## 输入字段

| 字段 | 所属程序 | 物理/数值含义 | 常见误用 |
|---|---|---|---|
| `calculation` | pw.x | 选择 SCF、NSCF、relax 等计算模式 | 用错误 calculation 类型生成下游依赖 |
| `conv_thr` | pw.x | 电子自洽收敛阈值 | 阈值过松却进入 phonon 或力敏感 workflow |
| `mixing_beta` | pw.x | 电荷密度混合强度 | 金属或大胞中设得过大导致振荡 |
| `electron_maxstep` | pw.x | 最大电子迭代步数 | 迭代耗尽后仍把结果当收敛 |
| `prefix/outdir` | pw.x and downstream programs | SCF scratch 数据边 | 不同 workflow 混用或读取旧数据 |

## output review

- `convergence has been achieved` 是否出现。
- SCF iteration 的 total energy 和 `estimated scf accuracy` 是否稳定。
- Fermi energy、occupation 和 warning 是否与物理判断一致。
- output header 中的 calculation type、cutoff、k-points、pseudopotential 是否与 input 一致。

## 最低掌握深度

能解释 SCF input 中 `CONTROL/SYSTEM/ELECTRONS` 的作用，能从 output 判断自洽是否可信，并能决定是否允许进入 relax、bands、DOS 或 phonon。

## 对应 workflow

- [workflows/ground-state/scf.md](../workflows/ground-state/scf.md)
- [workflows/ground-state/relax.md](../workflows/ground-state/relax.md)
- [workflows/electronic/bands.md](../workflows/electronic/bands.md)
- [workflows/phonon/phonon-dispersion-dfpt.md](../workflows/phonon/phonon-dispersion-dfpt.md)

## 资料来源

- QE INPUT_PW reference: <https://www.quantum-espresso.org/Doc/INPUT_PW.html>
- QE documentation: <https://www.quantum-espresso.org/documentation/>
- Pranab Das SCF tutorial: <https://pranabdas.github.io/espresso/hands-on/scf>
