**Note:** [https://julialang.org/](https://julialang.org/) 有美丽而且开源的文档，不是和arch特定相关的问题应该被贡献到这里.

[Julia](https://julialang.org/) 是一种高水平、高性能的针对数字计算的动态编程语言。它提供了复杂的编译器、分布式平行执行方式、数字的精准性和广泛的数学函数库。

## Contents

*   [1 安装](#安装)
*   [2 IJulia](#IJulia)
*   [3 构建包时出错](#构建包时出错)
    *   [3.1 Arpack](#Arpack)
*   [4 带编辑器的集成](#带编辑器的集成)
    *   [4.1 Vim](#Vim)
        *   [4.1.1 句法高亮和更多](#句法高亮和更多)
        *   [4.1.2 代码查错](#代码查错)
*   [5 性能](#性能)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [julia](https://www.archlinux.org/packages/?name=julia) 包. 学和用Julia请参阅 [上游文献](https://julia-cn.readthedocs.io/zh_CN/latest/).

## IJulia

如果装 [ijulia](https://github.com/JuliaLang/IJulia.jl) 是用的 `Pkg.add("IJulia")`并给出了警告 `MbedTLS had build errors.` 你可能需要安装 [mbedtls](https://www.archlinux.org/packages/?name=mbedtls) 包.

## 构建包时出错

### Arpack

构建Arpack包时可能产生下面的错误 (堆栈追踪省略了):

 `julia> Pkg.build("Arpack")` 
```
  Building Arpack → `~/.julia/packages/Arpack/UiiMc/deps/build.log`
┌ Error: Error building `Arpack`:
│ ERROR: LoadError: LibraryProduct(nothing, ["libarpack"], :libarpack, "Prefix(~/.julia/packages/Arpack/UiiMc/deps/usr)") is not satisfied, cannot generate deps.jl!
```

[一个问题已经提出了](https://github.com/JuliaLinearAlgebra/Arpack.jl/issues/5).

Arpack 包自己的 `libarpack.so` 需要 DSO `libopenblas64_.so.0` 才能展现在系统上:

 `$ ldd ~/packages/Arpack/UiiMc/deps/usr/lib/libarpack.so | grep 'not found'`  `        libopenblas64_.so.0 => not found` 
```
路径的`UiiMc`部分可能和你的系统上的不一样. 向上面显示的那样, 需要的DSO没在系统上,导致了构建错误.

```

DSO `/usr/lib/libopenblas.so` 来自 [openblas](https://www.archlinux.org/packages/?name=openblas)包， 可能不能稳定的作为插入式替代起作用, 因为 [64后缀好像被用来表示接口差异](https://github.com/xianyi/OpenBLAS/issues/1763) 和 [64后缀被用来表示版本差异而不是目标架构差异](http://numpy-discussion.10968.n7.nabble.com/Linking-Numpy-with-parallel-OpenBLAS-td41590.html).

## 带编辑器的集成

### Vim

#### 句法高亮和更多

[julia-vim](https://github.com/JuliaEditorSupport/julia-vim)

#### 代码查错

[julialint](https://github.com/zyedidia/julialint.vim) 插件和 [Lint.jl](https://github.com/tonyhffong/Lint.jl) 包结合起来可以提供代码查错功能.

## 性能

非常 [建议](https://discourse.julialang.org/t/multithreaded-libraries/) 你用一个多线程的BLAS实现，比如[openblas](https://www.archlinux.org/packages/?name=openblas). 这能让特定矩阵操作提速10-50x.