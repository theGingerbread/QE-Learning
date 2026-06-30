# SeeK-path

## 它适合解决什么学习问题？

为标准化结构生成 high-symmetry k-path，服务 bands workflow 的路径来源记录。

## 覆盖哪些 QE workflow？

- bands
- k-path source recording
- structure standardization boundary

## 适合跟读的部分

- 用已检查的 `<structure>` 生成 primitive cell 与 high-symmetry path，并记录 cell convention。

## 只适合作为参考的部分

- 结构构建细节放在独立 Structure-Learning 项目；本仓库只记录 QE k-path 使用要求。

## 与本仓库页面的对应关系

- [workflows/electronic/bands.md](../../workflows/electronic/bands.md)
- [theory-minimum/kpoints-symmetry-kpath.md](../../theory-minimum/kpoints-symmetry-kpath.md)

## 局限

SeeK-path 生成路径不等于 bands 结果可信；SCF、赝势和收敛仍需独立审阅。

## 原始链接

- [SeeK-path documentation](https://seekpath.readthedocs.io/en/latest/maindoc.html)
