**Note:** [https://julialang.org/](https://julialang.org/) 有美丽而且开源的文档，不是和arch特定相关的问题应该被贡献到这里.

[Julia](https://julialang.org/) 是一种高水平、高性能的针对数字计算的动态编程语言。它提供了复杂的编译器、分布式平行执行方式、数字的精准性和广泛的数学函数库。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 IJulia](#IJulia)
*   [3 带编辑器的集成](#.E5.B8.A6.E7.BC.96.E8.BE.91.E5.99.A8.E7.9A.84.E9.9B.86.E6.88.90)
    *   [3.1 Vim](#Vim)
        *   [3.1.1 句法高亮和更多](#.E5.8F.A5.E6.B3.95.E9.AB.98.E4.BA.AE.E5.92.8C.E6.9B.B4.E5.A4.9A)
        *   [3.1.2 代码查错](#.E4.BB.A3.E7.A0.81.E6.9F.A5.E9.94.99)
*   [4 性能](#.E6.80.A7.E8.83.BD)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [julia](https://www.archlinux.org/packages/?name=julia) 包. 学和用Julia请参阅 [上游文献](https://julia-cn.readthedocs.io/zh_CN/latest/).

## IJulia

如果装 [ijulia](https://github.com/JuliaLang/IJulia.jl) 是用的 `Pkg.add("IJulia")`并给出了警告 `MbedTLS had build errors.` 你可能需要安装 [mbedtls](https://www.archlinux.org/packages/?name=mbedtls) 包.

## 带编辑器的集成

### Vim

#### 句法高亮和更多

[julia-vim](https://github.com/JuliaEditorSupport/julia-vim)

#### 代码查错

[julialint](https://github.com/zyedidia/julialint.vim) 插件和 [Lint.jl](https://github.com/tonyhffong/Lint.jl) 包结合起来可以提供代码查错功能.

## 性能

非常 [建议](https://discourse.julialang.org/t/multithreaded-libraries/) 你用一个多线程的BLAS实现，比如[openblas](https://www.archlinux.org/packages/?name=openblas). 这能让特定矩阵操作提速10-50x.