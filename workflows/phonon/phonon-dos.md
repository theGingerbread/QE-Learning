# Phonon DOS workflow

## 本页解决什么问题

Phonon DOS 描述声子频率在 q-space 中的态密度分布，用于审阅振动谱整体频率范围、低频区域、热力学输入数据和与 dispersion 的一致性。它来自 q-grid dynamical matrices 经 `q2r.x` 得到的 force constants，再由 `matdyn.x` 在 DOS q mesh 上采样或积分。Phonon DOS 不是单条 high-symmetry q-path，也不能用平滑曲线替代 dispersion 和虚频 triage。

## 上游依赖

- 已通过 [phonon dispersion DFPT workflow](phonon-dispersion-dfpt.md) 中的 q-grid、dyn 文件、`q2r.x` 和 IFC 审阅。
- `flfrc` 来自当前结构、当前 SCF 和当前 q-grid，不混用旧 force constants。
- 低频、虚频、ASR 和 acoustic branches 已在 dispersion 或 debugging 页面中记录。
- 如果用于热力学或自由能下游，q-grid 和 DOS mesh 需要按目标 observable 做进一步收敛审阅。

## 计算图

```text
final static SCF
  -> ph.x ldisp=.true. on <q_grid>
  -> q2r.x -> <system>.fc
  -> matdyn.x with dos=.true. on <dos_q_mesh>
  -> phonon DOS
  -> output review
```

## 关键 QE 输入对象

```fortran
&INPUT
  flfrc = '<system>.fc',
  asr = '<asr_scheme>',
  dos = .true.,
  nk1 = <dos_nk1>,
  nk2 = <dos_nk2>,
  nk3 = <dos_nk3>,
  deltaE = <frequency_step_cm_minus_1>,
  fldos = 'phonon-dos.<system>.dat',
  flfrq = 'phonon-dos.<system>.freq',
/
```

| 字段 | 程序 | 判断意义 | 联动对象 | output 中如何验证 |
|---|---|---|---|---|
| `flfrc` | `matdyn.x` | 读取 real-space IFC | `q2r.x` 输出 | `matdyn.x` header 中读取的文件 |
| `dos` | `matdyn.x` | 启用 phonon DOS 模式 | `nk1/nk2/nk3` | output 是否进入 DOS 计算 |
| `nk1/nk2/nk3` | `matdyn.x` | DOS q mesh | 频率采样、热学下游 | output 中 q mesh 和 DOS 文件 |
| `deltaE` | `matdyn.x` | DOS 频率步长，单位按 QE 文档记录 | `fldos` 曲线分辨率 | DOS 文件频率间隔 |
| `fldos` | `matdyn.x` | phonon DOS 输出文件 | 记录和绘图 | 输出文件路径和列定义 |
| `asr` | `matdyn.x` | DOS 计算中的 ASR 处理 | 低频 DOS、acoustic modes | ASR 设置和低频区域变化 |

## 命令与文件边界

```bash
matdyn.x -in matdyn.dos.<system>.in > matdyn.dos.<system>.out
```

`matdyn.x` 的 DOS 模式读取 `flfrc`，不直接重新计算 DFPT perturbations。若 `flfrc` 源自不完整 q-grid、不可信 `q2r.x` 或混用结构，phonon DOS 不能用于下游。建议将 dispersion line-mode 和 DOS-mode 的 `flfrq`、`fldos` 文件名分开，避免旧文件覆盖。

## Output review

| 检查项 | 从哪里看 | 能证明什么 | 不能证明什么 |
|---|---|---|---|
| IFC 来源 | `matdyn.x` output 中 `flfrc` | DOS 使用了指定 force constants | IFC 来自可信上游 |
| DOS q mesh | `nk1/nk2/nk3` 和 output | DOS 采样网格被记录 | mesh 对目标性质已收敛 |
| frequency range | `fldos` 与 `flfrq` | DOS 覆盖的频率范围 | dispersion 中所有软模已解释 |
| negative frequencies | DOS 文件、频率文件、dispersion review | 低频/负频风险是否进入记录 | 虚频来源已被判定 |
| broadening / step | `deltaE`、绘图记录 | 曲线处理可复查 | 平滑程度代表物理可信 |
| warnings | `matdyn.x` output | 程序边界或输入异常 | 上游没有 warning |

## 收敛与可靠性

- Phonon DOS 依赖 q-grid、IFC 截断、DOS q mesh 和 `matdyn.x` 积分方式。
- DOS 曲线平滑不说明 phonon dispersion 可信；必须回查 acoustic branches、关键 q-path 和虚频。
- `matdyn.x` 的 DOS mesh 不是 `ph.x` DFPT q-grid；二者都需要记录。
- 若用于热力学自由能、零点能或谱密度比较，低频区域和 imaginary modes 的处理必须明确。

## PASS / WARN / BLOCK

| 状态 | 条件 | 是否允许进入下游 |
|---|---|---|
| PASS | `flfrc` 来自 PASS 的 q-grid phonon；DOS q mesh、`deltaE`、ASR 和 frequency range 已记录；无未解释 imaginary modes | 可用于 phonon DOS 图件、初步热学输入和与 dispersion 的交叉审阅 |
| WARN | DOS mesh 或 q-grid 尚未完成目标收敛；低频区域存在可追踪小异常；broadening/step 只适合探索 | 可用于诊断和敏感性测试，不应给定量热学结论 |
| BLOCK | IFC 不可信或混用；imaginary modes 未解释；`matdyn.x` 读取错误 `flfrc`；用平滑 DOS 掩盖 dispersion 问题 | 不允许进入热学、稳定性声明、EPC 或发表图件 |

## 常见误区

- 用 band q-path 的频率文件当作 phonon DOS。
- 只看 DOS 曲线平滑，不审阅 `ph.x -> q2r.x -> matdyn.x` 文件链。
- 负频区域被绘图处理隐藏后仍写成稳定体系。
- 未记录 `deltaE`、DOS q mesh 或 ASR。
- 用未收敛 q-grid 支持热力学或自由能结论。

## 下游影响

Phonon DOS 可作为热力学、自由能、谱密度和低频振动分析的输入。它不能替代 [phonon dispersion workflow](phonon-dispersion-dfpt.md) 和 [phonon debugging workflow](phonon-debugging.md)。如果下游是 EPC 或超导，phonon DOS 只能作为辅助检查，不能替代电子-声子矩阵元和 dense k/q 数据链。

## 来源与边界

- Stable: `matdyn.x` 的 `dos`、`nk1/nk2/nk3`、`deltaE`、`fldos`、`flfrq`、`asr` 以 QE `INPUT_MATDYN` 为准。
- Boundary: 本页不规定固定 DOS q mesh；是否足够取决于目标 observable 和低频区域稳定性。
- Internal standard: phonon DOS review 应写入 [output-review-checklist.md](../../standards/output-review-checklist.md) 和 calculation record。

## 资料来源

- QE INPUT_MATDYN reference: <https://www.quantum-espresso.org/Doc/INPUT_MATDYN.html>
- QE INPUT_Q2R reference: <https://www.quantum-espresso.org/Doc/INPUT_Q2R.html>
- QE PHonon user guide: <https://www.quantum-espresso.org/Doc/ph_user_guide/>
- 本仓库：[theory-minimum/dfpt-phonons.md](../../theory-minimum/dfpt-phonons.md)、[physics-judgement/09-phonons-soft-modes-and-dynamical-stability.md](../../physics-judgement/09-phonons-soft-modes-and-dynamical-stability.md)
