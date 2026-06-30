# QE Learning

这是一套面向科研计算流程的 Quantum ESPRESSO（QE）中文学习笔记。包含普通教程的翻译、input文件合集，并且把 QE 的实际使用过程整理成可复习、可扩展、可追溯的 workflow 文档。

本仓库当前处于“从占位到细节”的第一轮迭代：先建立稳定目录、统一写作模板、核心学习路线和少数关键 workflow 初稿；后续再逐篇补充官方文档、教程案例和真实计算记录。

## 解决什么问题

很多 QE 学习材料按 `pw.x`、`ph.x`、`dos.x`、`bands.x` 这样的程序逐个展开，容易让初学者误以为“会改 input 文件”等于会做计算。本仓库采用另一条主线：

```text
结构文件 / CIF
  -> 结构检查与标准化
  -> 赝势选择
  -> pw.x SCF
  -> cutoff / k-point / smearing 收敛性测试
  -> relax / vc-relax
  -> bands / DOS / PDOS
  -> phonon / DFPT / q2r / matdyn
  -> charge density / potential / visualization
  -> HPC 批量运行 / restart / provenance
```

每一篇笔记都尽量回答四个问题：

- 这一步解决什么物理或数值问题？
- QE 中对应哪些程序、输入参数和中间文件？
- 输出文件应该怎么看？
- 什么条件下结果才可以被继续用于下游 workflow？

## 推荐阅读顺序

1. [00-learning-roadmap.md](docs/qe/00-learning-roadmap.md)：先建立 1 周、2-4 周、1-2 个月的学习路线。
2. [01-qe-ecosystem.md](docs/qe/01-qe-ecosystem.md)：理解 QE 原生模块和外部工具在 workflow 中的位置。
3. `02-theory-minimum/`：只补“会影响 input/output 判断”的最低理论。
4. `03-core-input-structure/`：系统读懂 `pw.x` 输入文件。
5. `04-workflows/`：按 SCF、收敛性、relax、bands、DOS、phonon 等真实计算链学习。
6. `06-convergence-and-debugging/`：把“算完了”升级为“结果可信”。
7. `09-templates-and-checklists/`：用命名规范、记录模板和 checklist 固化习惯。

## 文档结构

```text
docs/
  qe/
    README.md
    00-learning-roadmap.md
    01-qe-ecosystem.md
    02-theory-minimum/
    03-core-input-structure/
    04-workflows/
    05-postprocessing/
    06-convergence-and-debugging/
    07-hpc-and-reproducibility/
    08-tools-and-ecosystem/
    09-templates-and-checklists/
```

## 当前资料基础

本仓库第一版主要来自两份本地调研材料：

- `/Users/paquette/Downloads/Quantum ESPRESSO as a Modern Research Stack.md`
- `/Users/paquette/Downloads/Quantum ESPRESSO Tutorial Website Ecosystem.md`

后续逐篇补充时，应优先核对：

- [Quantum ESPRESSO official documentation](https://www.quantum-espresso.org/documentation/)
- [QE input reference](https://www.quantum-espresso.org/Doc/INPUT_PW.html)
- [PHonon user guide / input docs](https://www.quantum-espresso.org/Doc/INPUT_PH.html)
- Pranab Das QE tutorial
- Kyoto University QE DokuWiki
- AiiDA Quantum ESPRESSO plugin docs
- Phonopy QE interface
- Materials Cloud / QE school materials

## 维护原则

- 不接受只有 input 文件、没有判断标准的笔记。
- 不把 phonon 当作普通后处理；它是 DFPT workflow，对 SCF、结构和收敛性更敏感。
- 每个 workflow 必须写清楚输入前提、中间文件、输出判断和下游依赖。
- 每次真实计算都应留下 calculation record，包括结构来源、赝势来源、命令、环境、输出摘要、收敛状态和下一步。

