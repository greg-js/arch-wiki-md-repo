**Note:** [https://julialang.org/](https://julialang.org/) has beautiful and open-source documentation, non-Arch-specific information should be contributed there.

[Julia](https://julialang.org/) is a high-level, high-performance dynamic programming language for numerical computing. It provides a sophisticated compiler, distributed parallel execution, numerical accuracy, and an extensive mathematical function library.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

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
│ ERROR: LoadError: LibraryProduct(nothing, ["libarpack"], :libarpack, "Prefix(~/.julia/packages/Arpack/UiiMc/deps/usr)") is not satisfied, cannot generate deps.jl!
```

Use the instructions [here](https://github.com/JuliaLinearAlgebra/Arpack.jl/pull/69) to resolve the issue.

## Integration with editors

### Vim

#### Syntax highlighting and more

[julia-vim](https://github.com/JuliaEditorSupport/julia-vim)

#### Linting

The [julialint](https://github.com/zyedidia/julialint.vim) plugin combined with the [Lint.jl](https://github.com/tonyhffong/Lint.jl) package can provide linting.

## Performance

It is [recommended](https://discourse.julialang.org/t/multithreaded-libraries/) that you use a multithreaded BLAS implementation, such as [openblas](https://www.archlinux.org/packages/?name=openblas). This can lead to speedups of 10-50x for certain matrix operations.