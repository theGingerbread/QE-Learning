# Pranab Das QE Tutorial

## 它适合解决什么学习问题？

按 workflow 学习 QE hands-on：SCF、convergence、relax、bands、DOS、PDOS、phonon、Wannier、SOC、DFT+U 和 Jupyter 后处理。

## 覆盖哪些 QE workflow？

- SCF
- cutoff/k-point convergence
- relax
- bands
- DOS
- PDOS
- phonon
- Wannier90
- SOC / DFT+U

## 适合跟读的部分

- SCF、convergence、relax、bands、DOS、PDOS 页面可用于理解文件链和命令顺序。
- phonon 页面适合理解 `pw.x -> ph.x -> q2r.x -> matdyn.x` 的程序链。
- Jupyter notebook 相关内容适合作为绘图和后处理参考。

## 只适合作为参考的部分

- 高级分支应在掌握基础 workflow 后阅读。
- repository 中的脚本适合学习命令串联，不等同于本仓库的记录规范。

## 与本仓库页面的对应关系

- [learn/02-first-scf-loop.md](../../learn/02-first-scf-loop.md)
- [learn/03-convergence-loop.md](../../learn/03-convergence-loop.md)
- [learn/05-electronic-structure-loop.md](../../learn/05-electronic-structure-loop.md)
- [learn/06-phonon-dfpt-loop.md](../../learn/06-phonon-dfpt-loop.md)
- [workflows/ground-state/scf.md](../../workflows/ground-state/scf.md)
- [workflows/electronic/bands.md](../../workflows/electronic/bands.md)
- [workflows/phonon/phonon-dispersion-dfpt.md](../../workflows/phonon/phonon-dispersion-dfpt.md)

## 局限

教程以 hands-on 文件和命令为中心，workflow graph、provenance、PASS / WARN / BLOCK gate 需要在本仓库 standards 中补足。

## 原始链接

- [主页](https://pranabdas.github.io/espresso/)
- [SCF](https://pranabdas.github.io/espresso/hands-on/scf)
- [phonon](https://pranabdas.github.io/espresso/hands-on/phonon/)
- [Jupyter setup](https://pranabdas.github.io/espresso/setup/jupyter)
- [GitHub repository](https://github.com/pranabdas/espresso)
