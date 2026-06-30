# Kyoto University QE Phonon DokuWiki

## 它适合解决什么学习问题？

作为 DFPT phonon 的专家笔记参考，学习 Gamma phonon、finite-q phonon、q-grid dispersion、phonon DOS、ASR、`epsil`、Born effective charge、dielectric tensor 和 negative frequency 判断。

## 覆盖哪些 QE workflow？

- Gamma phonon
- finite-q phonon
- phonon dispersion
- phonon DOS
- dielectric tensor / Born effective charge
- phonon debugging

## 适合跟读的部分

- Gamma `ph.x` 输入、`tr2_ph`、`prefix`、`epsil`、`fildyn` 的组织方式。
- `ldisp=.true.`、`nq1/nq2/nq3`、`q2r.x`、`matdyn.x` 的串联。
- ASR 和 acoustic branch 的输出比较。

## 只适合作为参考的部分

- 金属体系电场响应、轻微偏移 q 点、负频判断等专家经验需要结合本仓库 workflow 的 PASS / WARN / BLOCK 记录。

## 与本仓库页面的对应关系

- [learn/06-phonon-dfpt-loop.md](../../learn/06-phonon-dfpt-loop.md)
- [workflows/phonon/gamma-phonon.md](../../workflows/phonon/gamma-phonon.md)
- [workflows/phonon/phonon-dispersion-dfpt.md](../../workflows/phonon/phonon-dispersion-dfpt.md)
- [workflows/phonon/phonon-dos.md](../../workflows/phonon/phonon-dos.md)
- [workflows/phonon/dielectric-born-effective-charge.md](../../workflows/phonon/dielectric-born-effective-charge.md)
- [workflows/phonon/phonon-debugging.md](../../workflows/phonon/phonon-debugging.md)

## 局限

页面假设读者已有 QE 和 DFPT 背景，不提供统一项目记录模板。

## 原始链接

- [phonon calculation DokuWiki](https://www2.yukawa.kyoto-u.ac.jp/~koudai.sugimoto/dokuwiki/doku.php?id=quantumespresso%3Aphonon%3A%E3%83%95%E3%82%A9%E3%83%8E%E3%83%B3%E3%81%AE%E8%A8%88%E7%AE%97)
- [phonon DOS and dispersion DokuWiki](https://www2.yukawa.kyoto-u.ac.jp/~koudai.sugimoto/dokuwiki/doku.php?id=quantumespresso%3A%E3%83%95%E3%82%A9%E3%83%8E%E3%83%B3%E3%81%AE%E7%8A%B6%E6%85%8B%E5%AF%86%E5%BA%A6%E3%81%A8%E5%88%86%E6%95%A3)
