[Julia](https://julialang.org/) is a high-level, high-performance dynamic programming language for numerical computing. It provides a sophisticated compiler, distributed parallel execution, numerical accuracy, and an extensive mathematical function library.

## Contents

*   [1 Installation](#Installation)
*   [2 Integration with editors](#Integration_with_editors)
    *   [2.1 Vim](#Vim)
        *   [2.1.1 Syntax highlighting and more](#Syntax_highlighting_and_more)
        *   [2.1.2 Linting](#Linting)
*   [3 Performance](#Performance)

## Installation

[Install](/index.php/Install "Install") the [julia](https://www.archlinux.org/packages/?name=julia) package. To learn and use Julia, please read [upstream documents](https://docs.julialang.org/en/stable/).

## Integration with editors

### Vim

#### Syntax highlighting and more

[julia-vim](https://github.com/JuliaEditorSupport/julia-vim)

#### Linting

The [julialint](https://github.com/zyedidia/julialint.vim) plugin combined with the [Lint.jl](https://github.com/tonyhffong/Lint.jl) package can provide linting.

## Performance

It is [recommended](https://discourse.julialang.org/t/multithreaded-libraries/) that you use a multithreaded BLAS implementation, such as [openblas](https://aur.archlinux.org/packages/openblas/). This can lead to speedups of 10-50x for certain matrix operations.