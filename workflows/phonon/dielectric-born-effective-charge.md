# Dielectric tensor and Born effective charge workflow

## 本页解决什么问题

Dielectric tensor 和 Born effective charge 是 DFPT response quantities，用于描述绝缘体在电场和原子位移扰动下的响应。它们常用于 LO-TO splitting、non-analytic correction、IR activity 和极性材料 phonon 解释。它们不是普通 ground-state scalar output，也不能在未满足物理条件或未审阅 perturbation convergence 时直接解释。

## 上游依赖

- final static SCF 为 PASS，并且 occupation、smearing、k mesh、cutoff 适合 response 目标。
- 体系按绝缘体或可定义电场响应的问题处理；金属或未明确带隙边界的体系应进入 WARN/BLOCK。
- `ph.x` 在 Gamma limit 运行，并开启 `epsil=.true.`。
- 若用于 `matdyn.x` non-analytic correction，`fildyn`、Born charge、dielectric tensor、ASR 和 `flfrc` 文件链必须一致。

## 计算图

```text
final static SCF
  -> ph.x at Gamma with epsil=.true.
  -> dielectric tensor + Born effective charge tensors
  -> dynmat.x / matdyn.x with non-analytic correction when valid
  -> LO-TO / IR boundary review
```

## 关键 QE 输入对象

```fortran
&INPUTPH
  prefix = '<system>',
  outdir = '<scratch_dir>',
  tr2_ph = <phonon_threshold>,
  trans = .true.,
  epsil = .true.,
  fildyn = '<system>.dynG',
/
0.0 0.0 0.0
```

| 字段 | 程序 | 判断意义 | 联动对象 | output 中如何验证 |
|---|---|---|---|---|
| `epsil` | `ph.x` | 请求 dielectric tensor 和 Born effective charge | Gamma limit、绝缘体条件 | `ph.x` 输出张量段落 |
| `trans` | `ph.x` | 计算 phonon perturbations | `epsil`、`fildyn` | perturbation convergence |
| `tr2_ph` | `ph.x` | response 自洽阈值 | SCF `conv_thr` | electric-field 和 atomic perturbation 收敛 |
| `fildyn` | `ph.x` | 保存 Gamma dynamical matrix 和响应信息 | `dynmat.x` / `matdyn.x` | 后处理是否读取当前文件 |
| `asr` / `zasr` | `dynmat.x` / `q2r.x` / `matdyn.x` | acoustic 或 charge-neutrality 相关约束 | Born charge、LO-TO | 后处理输出和频率变化 |

## 命令与文件边界

```bash
ph.x -in ph.epsil.<system>.in > ph.epsil.<system>.out
```

`epsil=.true.` 的输出只在适用物理条件下解释。若后续 `matdyn.x` 使用 non-analytic correction，应把 dielectric tensor、Born effective charge、IFC 和 ASR 设置写入同一条计算记录。不要把来自不同结构、泛函、赝势或 q-grid 的 response tensors 与当前 phonon dispersion 混合。

## Output review

| 检查项 | 从哪里看 | 能证明什么 | 不能证明什么 |
|---|---|---|---|
| `epsil` 分支执行 | `ph.x` input echo 和 response 段落 | 请求并产生电场响应输出 | 该响应在当前物理体系一定可解释 |
| perturbation 收敛 | `ph.x` 每个 perturbation convergence | 线性响应方程完成 | 张量对 cutoff/k mesh 已收敛 |
| dielectric tensor | `ph.x` tensor 输出 | 介电响应被写出 | 张量物理合理或可与实验直接比较 |
| Born effective charge | `ph.x` 各原子 tensor | 有效电荷张量被写出 | 异常值一定是物理强极化 |
| tensor symmetry | 张量分量、结构对称性记录 | 与结构对称性是否一致 | 对称性异常来源已判定 |
| LO-TO / non-analytic | `dynmat.x` 或 `matdyn.x` 设置 | polar correction 是否有来源 | 所有方向的 splitting 都已正确解释 |
| warnings | `ph.x` output | 金属、电场响应或收敛警告 | warning 不影响结论 |

## 收敛与可靠性

- Dielectric tensor 和 Born effective charge 对泛函、赝势、带隙、k mesh、cutoff、结构和 SCF/DFPT 阈值敏感。
- Born charge 异常可能来自真实极性、近金属性、赝势/投影问题、结构问题或 response 未收敛；不能只凭数值大小定性。
- `epsil` 分支不替代 q-grid phonon dispersion；它为 Gamma limit 和 non-analytic correction 提供额外响应信息。
- 在金属或 occupation 边界不清的体系中，电场响应和 Born charge 解释应停止或降级。

## PASS / WARN / BLOCK

| 状态 | 条件 | 是否允许进入下游 |
|---|---|---|
| PASS | 体系条件满足；`epsil=.true.` 输出完整 dielectric/Born 张量；response perturbations 收敛；张量 symmetry 和文件链已记录 | 可用于 LO-TO splitting、IR 分析和 polar phonon correction |
| WARN | 小带隙、近金属、tensor symmetry 需复查、或张量对参数敏感但已记录 | 可进入敏感性测试或定性说明，不应给强定量结论 |
| BLOCK | response 未收敛；金属条件下解释 Born charge；张量缺失；后处理 polar correction 来源不明；文件链混用 | 不允许进入 LO-TO、IR/Raman 或极性材料结论 |

## 常见误区

- 把 Born effective charge 当作静态离子价态。
- 在金属或 occupation 不清的体系中解释 dielectric/Born 张量。
- 未审阅 tensor symmetry 就比较张量分量。
- 将不同 SCF 或不同结构的 response tensors 用于当前 `matdyn.x`。
- 不记录 non-analytic correction 的方向和设置。

## 下游影响

本页为 [Gamma phonon workflow](gamma-phonon.md)、[IR and Raman workflow](ir-raman.md) 和 [phonon dispersion workflow](phonon-dispersion-dfpt.md) 中的 polar correction 提供判断边界。若 dielectric/Born 分支为 WARN 或 BLOCK，LO-TO splitting、IR 强度和极性声子解释必须同步降级。

## 来源与边界

- Stable: `epsil`、`trans`、`fildyn`、`tr2_ph` 以 QE `INPUT_PH` 为准。
- Version-sensitive: non-analytic correction、Raman 分支和低维极性处理需核对当前 QE 版本文档。
- Boundary: 本页不把 response 张量作为实验量直接对照；比较前需说明泛函、温度、谐近似和数值收敛边界。

## 资料来源

- QE INPUT_PH reference: <https://www.quantum-espresso.org/Doc/INPUT_PH.html>
- QE INPUT_DYNMAT reference: <https://www.quantum-espresso.org/Doc/INPUT_DYNMAT.html>
- QE INPUT_MATDYN reference: <https://www.quantum-espresso.org/Doc/INPUT_MATDYN.html>
- QE PHonon user guide: <https://www.quantum-espresso.org/Doc/ph_user_guide/>
- Gonze and Lee, dynamical matrices, Born effective charges and dielectric permittivity tensors.
- 本仓库：[theory-minimum/dielectric-born-charge.md](../../theory-minimum/dielectric-born-charge.md)、[physics-judgement/10-dfpt-response-and-polar-materials.md](../../physics-judgement/10-dfpt-response-and-polar-materials.md)
