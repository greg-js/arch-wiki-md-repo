[Jupyter](https://en.wikipedia.org/wiki/Project_Jupyter "wikipedia:Project Jupyter") is a project which produces browser-based interactive environments for programming, mathematics, and data science. It supports a number of languages via plugins ("kernels"), such as Python, Ruby, Haskell, R, Scala and Julia.

Jupyter Notebook is the traditional and most stable application. [JupyterLab](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) has a new interface and is more suitable for working with larger projects consisting of multiple files. JupyterLab is considered "ready for daily use" since [version 0.33](https://github.com/jupyterlab/jupyterlab/blob/master/CHANGELOG.md#v0330).

## Contents

*   [1 Installation](#Installation)
*   [2 Running](#Running)
*   [3 Kernels](#Kernels)
    *   [3.1 Haskell](#Haskell)
    *   [3.2 Julia](#Julia)
    *   [3.3 Python](#Python)
    *   [3.4 R](#R)
    *   [3.5 Sage math](#Sage_math)
    *   [3.6 Octave](#Octave)
*   [4 See also](#See_also)

## Installation

For Jupyter Notebook, [install](/index.php/Install "Install") the [jupyter-notebook](https://www.archlinux.org/packages/?name=jupyter-notebook) package.

For JupyterLab, [install](/index.php/Install "Install") the [jupyterlab](https://www.archlinux.org/packages/?name=jupyterlab) package.

After installation, run the following to enable interactive Javascript widgets in the notebooks; otherwise, widgets will be disabled.

```
# jupyter nbextension enable --py --sys-prefix widgetsnbextension

```

## Running

To start the notebook server run:

```
$ jupyter notebook

```

To start JupyterLab run:

```
$ jupyter lab

```

Navigate to the URL given on the standard output if a web browser does not automatically open.

## Kernels

### Haskell

Install the [ihaskell-git](https://aur.archlinux.org/packages/ihaskell-git/) package. Then run `ihaskell install`.

### Julia

Install the [julia](https://www.archlinux.org/packages/?name=julia) package and run `julia` to get a REPL prompt. Then run:

```
Pkg.add("IJulia")

```

See the [Julia manual](http://docs.julialang.org/en/release-0.4/manual/packages/) for more details on package management.

### Python

Install the [python2-ipykernel](https://www.archlinux.org/packages/?name=python2-ipykernel) package for Python 2 support. Python 3 support (via [python-ipykernel](https://www.archlinux.org/packages/?name=python-ipykernel)) is included when installing [jupyter-notebook](https://www.archlinux.org/packages/?name=jupyter-notebook).

### R

Follow the installation instructions in [IR Kernel](https://github.com/IRkernel/IRkernel).

### Sage math

Install the [sagemath-jupyter](https://www.archlinux.org/packages/?name=sagemath-jupyter) package.

### Octave

Install the [jupyter-octave_kernel](https://aur.archlinux.org/packages/jupyter-octave_kernel/) package.

## See also

*   [Official website](http://jupyter.org/)