# QE Project Layout

这是个人计算项目建议结构，不是本仓库目录结构。它用于把结构来源、赝势来源、输入输出、脚本、记录和图像分开，方便复查和迁移。

```text
<project>/
  README.md
  structures/
  pseudo-source.md
  inputs/
  outputs/
  scripts/
  records/
  figures/
  notes.md
```

最低要求：每次可复查计算都应有 input、output、record、赝势来源、运行命令和 output review。对于 scratch、wavefunction、restart 等大文件，应在记录中说明位置和保留策略，不必全部纳入文档仓库。
