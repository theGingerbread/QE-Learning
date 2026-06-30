# DFPT and phonons

## 它在 QE 中对应什么问题？

QE phonon workflow 用 DFPT 计算对原子位移或电场扰动的线性响应。q-grid phonon 还需要 `q2r.x` 和 `matdyn.x` 完成 IFC 和插值。

## 不理解它会造成什么错误？

- 只算 Gamma phonon 却解释 dispersion。
- q-grid dyn 文件不完整就运行 `q2r.x`。
- 把 ASR 当作修复未收敛结构的工具。
- SCF 或 relax 质量不足时直接解释 negative frequency。

## 相关 QE 输入字段

| 字段 | 所属程序 | 物理/数值含义 | 常见误用 |
|---|---|---|---|
| `tr2_ph` | ph.x | phonon 响应收敛阈值 | 过松导致频率漂移 |
| `ldisp/nq1/nq2/nq3` | ph.x | 启用并定义 uniform q-grid | 想要 dispersion 却只算 Gamma |
| `fildyn` | ph.x/q2r.x | dynamical matrix 文件前缀 | 文件链不一致 |
| `flfrc/zasr` | q2r.x | real-space force constants 和 ASR | dyn 不全或 ASR 误用 |
| `asr/q_in_band_form/flfrq` | matdyn.x | 插值、路径和输出频率 | 路径或 ASR 设置未记录 |

## output 中如何发现问题？

- 每个 q 点和 perturbation 是否收敛。
- dyn 文件数量是否完整。
- `q2r.x` 是否读全 dynamical matrices。
- Gamma acoustic branches、negative frequency 和 warning 是否已审阅。

## 最低掌握深度

能画出 `pw.x scf -> ph.x -> q2r.x -> matdyn.x` 数据链，并知道每一步失败会在什么 output 暴露。

## 与 workflow 页面的对应关系

- [workflows/phonon/gamma-phonon.md](../workflows/phonon/gamma-phonon.md)
- [workflows/phonon/phonon-dispersion-dfpt.md](../workflows/phonon/phonon-dispersion-dfpt.md)
- [workflows/phonon/phonon-dos.md](../workflows/phonon/phonon-dos.md)
- [workflows/phonon/phonon-debugging.md](../workflows/phonon/phonon-debugging.md)

## 资料来源

- QE INPUT_PH reference: <https://www.quantum-espresso.org/Doc/INPUT_PH.html>
- QE INPUT_Q2R reference: <https://www.quantum-espresso.org/Doc/INPUT_Q2R.html>
- QE INPUT_MATDYN reference: <https://www.quantum-espresso.org/Doc/INPUT_MATDYN.html>
- QE PHonon user guide: <https://www.quantum-espresso.org/Doc/ph_user_guide/>
- Kyoto phonon DokuWiki: <https://www2.yukawa.kyoto-u.ac.jp/~koudai.sugimoto/dokuwiki/doku.php?id=quantumespresso%3Aphonon%3A%E3%83%95%E3%82%A9%E3%83%8E%E3%83%B3%E3%81%AE%E8%A8%88%E7%AE%97>
