[SageMath](http://www.sagemath.org) (formerly **Sage**) is a program for numerical and symbolic mathematical computation that uses [Python](/index.php/Python "Python") as its main language. It is meant to provide an alternative for commercial programs such as Maple, Matlab, and Mathematica.

SageMath provides support for the following:

*   **Calculus**: using [Maxima](https://en.wikipedia.org/wiki/Maxima_(software) and [SymPy](https://en.wikipedia.org/wiki/SymPy "wikipedia:SymPy").
*   **Linear Algebra**: using the [GSL](https://en.wikipedia.org/wiki/GNU_Scientific_Library "wikipedia:GNU Scientific Library"), [SciPy](https://en.wikipedia.org/wiki/SciPy "wikipedia:SciPy") and [NumPy](https://en.wikipedia.org/wiki/NumPy "wikipedia:NumPy").
*   **Statistics**: using [R](https://en.wikipedia.org/wiki/R_(programming_language) (through RPy) and SciPy.
*   **Graphs**: using [matplotlib](https://en.wikipedia.org/wiki/matplotlib "wikipedia:matplotlib").
*   An **interactive shell** using [IPython](https://en.wikipedia.org/wiki/IPython "wikipedia:IPython").
*   Access to **Python modules** such as [PIL](https://en.wikipedia.org/wiki/Python_Imaging_Library "wikipedia:Python Imaging Library"), [SQLAlchemy](https://en.wikipedia.org/wiki/SQLAlchemy "wikipedia:SQLAlchemy"), etc.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 SageMath command-line](#SageMath_command-line)
    *   [2.2 Sage Notebook](#Sage_Notebook)
    *   [2.3 Jupyter Notebook](#Jupyter_Notebook)
    *   [2.4 Cantor](#Cantor)
*   [3 Optional additions](#Optional_additions)
    *   [3.1 SageTeX](#SageTeX)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 TeX Live does not recognize SageTex](#TeX_Live_does_not_recognize_SageTex)
*   [5 See also](#See_also)

## Installation

*   [sagemath](https://www.archlinux.org/packages/?name=sagemath) contains the command-line version;
*   [sagemath-doc](https://www.archlinux.org/packages/?name=sagemath-doc) for HTML documentation and inline help from the command line.
*   [sage-notebook](https://www.archlinux.org/packages/?name=sage-notebook) includes the browser-based notebook interface.

**Note:** Most if not all of the [standard sage packages](http://doc.sagemath.org/html/en/installation/standard_packages.html) are available as [optional dependencies](/index.php/Pacman#Installing_packages "Pacman") of the [sagemath](https://www.archlinux.org/packages/?name=sagemath) package, therefore they have to be installed additionally as normal Arch packages in order to take advantage of their features. Note that there is no need to install them with `sage -i`, in fact this command will not work if you installed SageMath with pacman.

## Usage

SageMath mainly uses Python as a scripting language with a few [modifications](http://doc.sagemath.org/html/en/tutorial/afterword.html#section-mathannoy) to make it better suited for mathematical computations.

### SageMath command-line

SageMath can be started from the command-line:

```
$ sage

```

For information on the SageMath command-line see [this page](http://doc.sagemath.org/reference/repl/index.html).

The command-line is based on the IPython shell so you can use all its [tricks](http://doc.sagemath.org/html/en/tutorial/interactive_shell.html) with SageMath. For an extensive tutorial on IPython see the community maintained [IPython Cookbook](http://wiki.ipython.org/Cookbook).

Note, however, that it is not very comfortable for some uses such as plotting. When you try to plot something, for example:

```
sage: plot(sin,(x,0,10))

```

SageMath opens the plot in an external application.

### Sage Notebook

**Note:** The SageMath Flask notebook is currently in maintenance mode and will be deprecated in favour of the Jupyter notebook. The Jupyter notebook is recommended for all new worksheets. You can use the [sage-notebook-exporter](https://www.archlinux.org/packages/?name=sage-notebook-exporter) application to convert your Flask notebooks to Jupyter

A better suited interface for advanced usage in SageMath is the Notebook. To start the Notebook server from the command-line, execute:

```
$ sage -n

```

The notebook will be accessible in the browser from [http://localhost:8080](http://localhost:8080) and will require you to login.

However, if you only run the server for personal use, and not across the internet, the login will be an annoyance. You can instead start the Notebook without requiring login, and have it automatically pop up in a browser, with the following command:

```
$ sage -c "notebook(automatic_login=True)"

```

For a more comprehensive tutorial on the Sage Notebook see the [Sage documentation](http://doc.sagemath.org/html/en/reference/notebook/index.html). For more information on the `notebook()` command see [this page](http://doc.sagemath.org/html/en/reference/notebook/sagenb/notebook/notebook.html).

### Jupyter Notebook

SageMath also provides a kernel for the [Jupyter](https://jupyter.org/) notebook in package [sagemath-jupyter](https://www.archlinux.org/packages/?name=sagemath-jupyter). To use it, install [ipython2-notebook](https://www.archlinux.org/packages/?name=ipython2-notebook) and [mathjax](https://www.archlinux.org/packages/?name=mathjax), launch the notebook with the command

```
$ jupyter notebook

```

and choose "SageMath" in the drop-down "New..." menu. The SageMath Jupyter notebook supports [LaTeX](/index.php/LaTeX "LaTeX") output via the `%display latex` command and 3D plots if [jmol](https://www.archlinux.org/packages/?name=jmol) is installed.

### Cantor

[Cantor](http://edu.kde.org/applications/mathematics/cantor/) is an application included in the KDE Edu Project. It acts as a front-end for various mathematical applications such as Maxima, SageMath, Octave, Scilab, etc. See the [Cantor page](http://wiki.sagemath.org/Cantor) on the Sage wiki for more information on how to use it with SageMath.

Cantor can be installed with the [cantor](https://www.archlinux.org/packages/?name=cantor) package or as part of the [kde-applications](https://www.archlinux.org/groups/x86_64/kde-applications/) or [kdeedu](https://www.archlinux.org/groups/x86_64/kdeedu/) groups, available in the [official repositories](/index.php/Official_repositories "Official repositories").

## Optional additions

### SageTeX

If you have [TeX Live](/index.php/TeX_Live "TeX Live") installed on your system, you may be interested in [using SageTeX](http://doc.sagemath.org/html/en/tutorial/sagetex.html), a package that makes the inclusion of SageMath code in LaTeX files possible. TeX Live is made aware of SageTeX automatically so you can start using it straight away.

As a simple example, here is how you include a Sage 2D plot in your TEX document (assuming you use `pdflatex`):

*   include the `sagetex` package in the preamble of your document with the usual

```
\usepackage{sagetex}

```

*   create a `sagesilent` environment in which you insert your code:

```
\begin{sagesilent}
dob(x) = sqrt(x^2 - 1) / (x * arctan(sqrt(x^2 - 1)))
dpr(x) = sqrt(x^2 - 1) / (x * log( x + sqrt(x^2 - 1)))
p1 = plot(dob,(x, 1, 10), color='blue')
p2 = plot(dpr,(x, 1, 10), color='red')
ptot = p1 + p2
ptot.axes_labels(['$\\xi$','$\\frac{R_h}{\\max(a,b)}$'])
\end{sagesilent}

```

*   create the plot, e.g. inside a `float` environment:

```
\begin{figure}
\begin{center}
\sageplot[width=\linewidth]{ptot}
\end{center}
\end{figure}

```

*   compile your document with the following procedure:

```
$ pdflatex <doc.tex>
$ sage <doc.sage>
$ pdflatex <doc.tex>

```

*   you can have a look at your output document.

The full documentation of SageTeX is available on [CTAN](http://www.ctan.org/pkg/sagetex).

## Troubleshooting

### TeX Live does not recognize SageTex

If your TeX Live installation does not find the SageTex package, you can try the following procedure (as root or use a local folder):

*   Copy the files to the texmf directory:

```
# cp /opt/sage/local/share/texmf/tex/* /usr/share/texmf/tex/

```

*   Refresh TeX Live:

```
# texhash /usr/share/texmf/
texhash: Updating /usr/share/texmf/.//ls-R... 
texhash: Done.

```

## See also

*   [Official Website](http://www.sagemath.org/)
*   [SageMath Documentation](http://doc.sagemath.org/)
*   [Planet Sage](http://planet.sagemath.org/)
*   [SageMath Wiki](http://wiki.sagemath.org/)
*   [Software Used by SageMath](http://www.sagemath.org/links-components.html)