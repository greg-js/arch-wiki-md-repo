**Note:** [https://julialang.org/](https://julialang.org/) has beautiful and open-source documentation, non-Arch-specific information should be contributed there.

[Julia](https://julialang.org/) is a high-level, high-performance dynamic programming language for numerical computing. It provides a sophisticated compiler, distributed parallel execution, numerical accuracy, and an extensive mathematical function library.

## Contents

*   [1 Installation](#Installation)
*   [2 IJulia](#IJulia)
*   [3 Package build errors](#Package_build_errors)
    *   [3.1 Arpack](#Arpack)
*   [4 Integration with editors](#Integration_with_editors)
    *   [4.1 Vim](#Vim)
        *   [4.1.1 Syntax highlighting and more](#Syntax_highlighting_and_more)
        *   [4.1.2 Linting](#Linting)
*   [5 Performance](#Performance)

## Installation

[Install](/index.php/Install "Install") the [julia](https://www.archlinux.org/packages/?name=julia) package. To learn and use Julia, please read [upstream documents](https://docs.julialang.org/en/latest/).

## IJulia

If attempting to install [ijulia](https://github.com/JuliaLang/IJulia.jl) by running `Pkg.add("IJulia")` gives the warning `MbedTLS had build errors.` you might need to install the [mbedtls](https://www.archlinux.org/packages/?name=mbedtls) package.

## Package build errors

### Arpack

Building the Arpack package can result in an error like shown below (stacktrace omitted):

 `julia> Pkg.build("Arpack")` 
```
  Building Arpack → `~/.julia/packages/Arpack/UiiMc/deps/build.log`
┌ Error: Error building `Arpack`:
│ ERROR: LoadError: LibraryProduct(nothing, ["libarpack"], :libarpack, "Prefix(~/.julia/packages/Arpack/UiiMc/deps/usr)") is not satisfied, cannot generate deps.jl!
```

[An issue has been filed](https://github.com/JuliaLinearAlgebra/Arpack.jl/issues/5).

Arpack packages its own `libarpack.so` that requires the DSO `libopenblas64_.so.0` to be present on the system:

 `$ ldd ~/.julia/packages/Arpack/UiiMc/deps/usr/lib/libarpack.so | grep 'not found'`  `        libopenblas64_.so.0 => not found` 

The `UiiMc` part of the path may be different on your system. As shown, the required DSO is not present on the system, causing the build error. A [workaround](https://github.com/JuliaLinearAlgebra/Arpack.jl/issues/5#issuecomment-437869878) to this problem is to create a symbolic link to the DSO file provided by the [openblas](https://www.archlinux.org/packages/?name=openblas) package, i.e.

```
# ln -s /usr/lib/libopenblas.so /usr/lib/libopenblas64_.so.0

```

and then rebuild the Arpack package in Julia. However, it is in unclear whether the DSO `/usr/lib/libopenblas.so` from the package [openblas](https://www.archlinux.org/packages/?name=openblas) can function as a stable drop-in replacement, since [the 64 suffix seems to be used to indicate a difference in interface](https://github.com/xianyi/OpenBLAS/issues/1763) and [the 64 suffix does indicate a different version rather than a difference in target architecture](http://numpy-discussion.10968.n7.nabble.com/Linking-Numpy-with-parallel-OpenBLAS-td41590.html).

## Integration with editors

### Vim

#### Syntax highlighting and more

[julia-vim](https://github.com/JuliaEditorSupport/julia-vim)

#### Linting

The [julialint](https://github.com/zyedidia/julialint.vim) plugin combined with the [Lint.jl](https://github.com/tonyhffong/Lint.jl) package can provide linting.

## Performance

It is [recommended](https://discourse.julialang.org/t/multithreaded-libraries/) that you use a multithreaded BLAS implementation, such as [openblas](https://www.archlinux.org/packages/?name=openblas). This can lead to speedups of 10-50x for certain matrix operations.