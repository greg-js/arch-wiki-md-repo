[Jupyter](http://jupyter.org/) is a browser-based interactive notebook for programming, mathematics, and data science. It supports a number of languages via plugins ("kernels"), such as Python, Ruby, Haskell, R, Scala and Julia.

## Contents

*   [1 Installation](#Installation)
*   [2 Running](#Running)
*   [3 Kernels](#Kernels)
    *   [3.1 Haskell](#Haskell)
    *   [3.2 Julia](#Julia)
    *   [3.3 Python](#Python)
    *   [3.4 R](#R)
    *   [3.5 Sage math](#Sage_math)

## Installation

Install [jupyter](https://www.archlinux.org/packages/?name=jupyter). For the browser-based notebook, also install [jupyter-notebook](https://www.archlinux.org/packages/?name=jupyter-notebook).

## Running

Run

```
jupyter notebook

```

to start the notebook server. Then open a browser and navigate to [localhost:8888](http://localhost:8888).

## Kernels

### Haskell

Install [ihaskell-git](https://aur.archlinux.org/packages/ihaskell-git/) from the AUR. Then run `ihaskell install`.

### Julia

Install [julia](https://www.archlinux.org/packages/?name=julia) and run `julia` to get a REPL prompt. Then run:

```
Pkg.add("IJulia")

```

See the [Julia manual](http://docs.julialang.org/en/release-0.4/manual/packages/) for more details on package management.

### Python

Install [ipython2-notebook](https://www.archlinux.org/packages/?name=ipython2-notebook) for Python 2\. Python 3 support (via [python-ipykernel](https://www.archlinux.org/packages/?name=python-ipykernel)) is included when installing [jupyter](https://www.archlinux.org/packages/?name=jupyter).

### R

Follow the installation instructions in [IR Kernel](https://github.com/IRkernel/IRkernel).

### Sage math

Install [sagemath](https://www.archlinux.org/packages/?name=sagemath) and [sagemath-jupyter](https://www.archlinux.org/packages/?name=sagemath-jupyter).