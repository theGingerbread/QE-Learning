# AiiDA-QE Optional Reference

## 它适合解决什么学习问题？

作为高级 workflow/provenance 参考，理解计算图、输入输出追踪、restart 和 scheduler 集成。

## 覆盖哪些 QE workflow？

- SCF/relax/bands/DOS wrappers
- provenance graph
- scheduler integration
- restart management

## 适合跟读的部分

- 在能手动完成 QE 原生命令行 workflow 后，再阅读 AiiDA-QE tutorials 或 workchain 文档。

## 只适合作为参考的部分

- database、daemon、profile、remote computer 和 scheduler 概念只作为自动化系统设计参考。

## 与本仓库页面的对应关系

- [learn/08-hpc-and-reproducibility.md](../../learn/08-hpc-and-reproducibility.md)
- [standards/calculation-record-template.md](../../standards/calculation-record-template.md)
- [standards/citation-and-source-policy.md](../../standards/citation-and-source-policy.md)

## 局限

AiiDA 组织和追踪 workflow，不替代物理判断、收敛测试和 output review。

## 原始链接

- [AiiDA-QE tutorials](https://aiida-quantumespresso.readthedocs.io/en/latest/tutorials/)
- [AiiDA-QE PwBandsWorkChain](https://aiida-quantumespresso.readthedocs.io/en/latest/howto/run_pwbands.html)
- [AiiDA-QE workflow logic](https://aiida-quantumespresso.readthedocs.io/en/latest/topics/workflow_logic.html)
- [AiiDA-QE protocols](https://aiida-quantumespresso.readthedocs.io/en/latest/topics/protocol.html)
