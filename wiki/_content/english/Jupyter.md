[Jupyter](https://en.wikipedia.org/wiki/Project_Jupyter "wikipedia:Project Jupyter") is a project which produces browser-based interactive environments for programming, mathematics, and data science. It supports a number of languages via plugins ("kernels"), such as [Python](/index.php/Python "Python"), [Ruby](/index.php/Ruby "Ruby"), [Haskell](/index.php/Haskell "Haskell"), [R](/index.php/R "R"), [Scala](/index.php/Scala "Scala") and [Julia](/index.php/Julia "Julia").

JupyterLab is "Jupyter’s Next-Generation Notebook Interface", while Jupyter Notebook is the original. See the [Jupyter website](https://jupyter.org/) for a comparison.

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
    *   [3.7 Maxima](#Maxima)
*   [4 See also](#See_also)

## Installation

*   For JupyterLab, [install](/index.php/Install "Install") the [jupyterlab](https://www.archlinux.org/packages/?name=jupyterlab) package.
*   For Jupyter Notebook, [install](/index.php/Install "Install") the [jupyter-notebook](https://www.archlinux.org/packages/?name=jupyter-notebook) package.

After installation, run the following to enable interactive JavaScript widgets in the notebooks; otherwise, widgets will be disabled.

```
# jupyter nbextension enable --py --sys-prefix widgetsnbextension

```

To install third-party Jupyter Notebook extensions for the current user, use the `--user` option instead of `--sys-prefix` while executing `jupyter nbextension install`. To do the same for [installation of JupyterLab extensions](https://jupyterlab.readthedocs.io/en/stable/user/extensions.html?highlight=advanced%20usage#advanced-usage), set the environment variable

```
$ export JUPYTERLAB_DIR=$HOME/.local/share/jupyter/lab

```

and verify it by running `jupyter lab paths`. Then onwards follow usual installation instructions.

## Running

To start JupyterLab run:

```
$ jupyter lab

```

To start Jupyter Notebook run:

```
$ jupyter notebook

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

Python 3 kernel is used by default via [python-ipykernel](https://www.archlinux.org/packages/?name=python-ipykernel). For legacy Python 2 support install [python2-ipykernel](https://www.archlinux.org/packages/?name=python2-ipykernel).

### R

Follow the [installation instructions](/index.php/R#Jupyter_notebook "R") in [IR Kernel](https://github.com/IRkernel/IRkernel).

### Sage math

Install the [sagemath-jupyter](https://www.archlinux.org/packages/?name=sagemath-jupyter) package.

### Octave

Install the [jupyter-octave_kernel](https://aur.archlinux.org/packages/jupyter-octave_kernel/) package.

### Maxima

Install the [maxima-jupyter-git](https://aur.archlinux.org/packages/maxima-jupyter-git/) package.

## See also

*   [Official website](https://jupyter.org/)