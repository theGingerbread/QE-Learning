# Dielectric tensor and Born effective charge

## QE 中对应的问题

介电张量和 Born effective charge 是 Gamma DFPT response 分支，用于极性材料的 non-analytic correction、LO-TO splitting 和 IR 相关分析。

## 常见错误

- 在不适用的物理条件下强行解释 `epsil` 输出。
- 没有 Gamma response 分支却期待 dielectric tensor。
- 把 Born effective charge 当作静态价态。
- 未记录 LO-TO splitting 和方向依赖条件。

## 输入字段

| 字段 | 所属程序 | 物理/数值含义 | 常见误用 |
|---|---|---|---|
| `epsil` | ph.x | 请求介电张量和 Born effective charge | 不检查适用条件 |
| `trans` | ph.x | 计算声子扰动 | 遗漏必要响应分支 |
| `fildyn` | ph.x/dynmat.x | Gamma dynamical matrix | 读取错误文件 |
| `asr` | dynmat.x/matdyn.x | 声学和规则处理 | 把数值修正当物理结论 |

## output review

- dielectric tensor 和 Born effective charge 段是否出现。
- electric-field perturbation 是否收敛。
- output 是否提示金属/绝缘体或电场相关限制。
- LO-TO 相关结果是否记录方向和前提。

## 最低掌握深度

能判断什么时候应启用 `epsil`，什么时候应给出 BLOCK 或 WARN，而不是硬解释响应张量。

## 对应 workflow

- [workflows/phonon/dielectric-born-effective-charge.md](../workflows/phonon/dielectric-born-effective-charge.md)
- [workflows/phonon/ir-raman.md](../workflows/phonon/ir-raman.md)
- [workflows/phonon/phonon-dispersion-dfpt.md](../workflows/phonon/phonon-dispersion-dfpt.md)

## 资料来源

- QE INPUT_PH reference: <https://www.quantum-espresso.org/Doc/INPUT_PH.html>
- QE INPUT_DYNMAT reference: <https://www.quantum-espresso.org/Doc/INPUT_DYNMAT.html>
- Kyoto phonon DokuWiki: <https://www2.yukawa.kyoto-u.ac.jp/~koudai.sugimoto/dokuwiki/doku.php?id=quantumespresso%3Aphonon%3A%E3%83%95%E3%82%A9%E3%83%8E%E3%83%B3%E3%81%AE%E8%A8%88%E7%AE%97>
