# Pseudopotentials

## QE 中对应的问题

赝势决定 valence 空间、泛函一致性、relativistic/SOC 能力和 cutoff 需求。QE input 通过 `pseudo_dir` 与 `ATOMIC_SPECIES` 指向 UPF 文件。

## 常见错误

- PBE、PBEsol、LDA 等泛函族混用。
- SOC 计算使用非 fully relativistic 赝势。
- 换赝势后不重做 cutoff/k 点/目标性质收敛。
- 只记录文件名，不记录库、版本、泛函和来源 URL。

## 输入字段

| 字段 | 所属程序 | 物理/数值含义 | 常见误用 |
|---|---|---|---|
| `pseudo_dir` | pw.x | 赝势文件目录 | 目录中同名文件来源不明 |
| `ATOMIC_SPECIES` | pw.x | 元素、质量和 UPF 文件映射 | 元素顺序或文件名错误 |
| `input_dft` | pw.x | 交换关联泛函设置，通常应与赝势一致 | 手动设置与赝势生成泛函不一致 |
| `lspinorb/noncolin` | pw.x | SOC/noncollinear 分支依赖合适赝势 | 赝势能力不足 |

## output review

- output 中 pseudopotential 段是否加载了预期文件。
- PP type、valence electrons、relativistic 信息是否符合目标。
- warning 是否提示泛函或赝势不一致。

## 最低掌握深度

能为每次计算记录赝势来源、版本、泛函、PP 类型、推荐 cutoff，并知道更换赝势等于重新验证数值策略。

## 对应 workflow

- [workflows/ground-state/scf.md](../workflows/ground-state/scf.md)
- [workflows/advanced/noncollinear-soc.md](../workflows/advanced/noncollinear-soc.md)
- [workflows/advanced/pseudopotential-generation-overview.md](../workflows/advanced/pseudopotential-generation-overview.md)

## 资料来源

- QE INPUT_PW reference: <https://www.quantum-espresso.org/Doc/INPUT_PW.html>
- QE pseudopotentials page: <https://www.quantum-espresso.org/pseudopotentials/>
