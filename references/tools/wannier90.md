# Wannier90

## 它适合解决什么学习问题？

学习 QE 电子结构到 Wannier interpolation 的数据边界，用于能带插值、Berry 相关量和输运前置分析。

## 覆盖哪些 QE workflow？

- QE -> pw2wannier90.x -> Wannier90
- bands interpolation
- advanced transport pre-processing

## 适合跟读的部分

- 理解 projections、disentanglement、frozen window 和 `pw2wannier90.x` 接口。

## 只适合作为参考的部分

- Wannierization 质量不能只看流程完成，需要检查插值 bands 与 QE bands 对照。

## 与本仓库页面的对应关系

- [workflows/advanced/wannier90-overview.md](../../workflows/advanced/wannier90-overview.md)
- [workflows/electronic/bands.md](../../workflows/electronic/bands.md)

## 局限

Wannier90 是高级电子结构工具，不替代 QE 基础 bands/DOS 学习。

## 原始链接

- [Wannier90](https://wannier.org/)
- [Wannier90 documentation](https://wannier90.readthedocs.io/)
- [QE INPUT_pw2wannier90](https://www.quantum-espresso.org/Doc/INPUT_pw2wannier90.html)
