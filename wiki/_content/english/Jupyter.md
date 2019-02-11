[Jupyter](https://en.wikipedia.org/wiki/Project_Jupyter "wikipedia:Project Jupyter") is a project which produces browser-based interactive environments for programming, mathematics, and data science. It supports a number of languages via plugins ("kernels"), such as Python, Ruby, Haskell, R, Scala and Julia.

Jupyter Notebook is the traditional and most stable application. [JupyterLab](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) has a new interface and is more suitable for working with larger projects consisting of multiple files. JupyterLab is considered "ready for daily use" since [version 0.33](https://jupyterlab.readthedocs.io/en/stable/getting_started/changelog.html#v0-33-0).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

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

To install third-party Jupyter Notebook extensions for the current user, use the `--user` option instead of `--sys-prefix` while executing `jupyter nbextension install`. To do the same for [installation of JupyterLab extensions](https://jupyterlab.readthedocs.io/en/stable/user/extensions.html?highlight=advanced%20usage#advanced-usage), set the environment variable

```
$ export JUPYTERLAB_DIR=$HOME/.local/share/jupyter/lab

```

and verify it by running `jupyter lab paths`. Then onwards follow usual installation instructions.

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
using Pkg
Pkg.add("IJulia")

```

See the [Julia manual](https://docs.julialang.org/en/v1.0/stdlib/Pkg/#Getting-Started-1) for more details on package management.

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