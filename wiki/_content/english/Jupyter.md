[Jupyter](http://jupyter.org/) is a project which produces browser-based interactive environments for programming, mathematics, and data science. It supports a number of languages via plugins ("kernels"), such as Python, Ruby, Haskell, R, Scala and Julia.

Jupyter Notebook is the traditional and most stable application. [JupyterLab](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) has a new interface and is more suitable for working with larger projects consisting of multiple files. JupyterLab is in beta as of February 2018.

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

## Installation

For Jupyter Notebook, [install](/index.php/Install "Install") the [jupyter-notebook](https://www.archlinux.org/packages/?name=jupyter-notebook) package.

For JupyterLab, [install](/index.php/Install "Install") the [jupyterlab](https://aur.archlinux.org/packages/jupyterlab/) package.

After installation, run the following (as root) to enable interactive Javascript widgets in the notebooks (otherwise, widgets will be disabled):

```
# jupyter nbextension enable --py --sys-prefix widgetsnbextension

```

## Running

To start the notebook server, e.g. from a directory containing some *.ipynb* notebook files to be served, run:

```
$ jupyter notebook

```

To start JupyterLab, run:

```
$ jupyter lab

```

Then open a browser and navigate to [http://localhost:8888](http://localhost:8888).

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