# SageMath

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Matlab](/index.php/Matlab "Matlab")
*   [Octave](/index.php/Octave "Octave")
*   [Mathematica](/index.php/Mathematica "Mathematica")

[SageMath](http://www.sagemath.org) (formerly **Sage**) is a program for numerical and symbolic mathematical computation that uses [Python](/index.php/Python "Python") as its main language. It is meant to provide an alternative for commercial programs such as Maple, Matlab, and Mathematica.

SageMath provides support for the following:

*   **Calculus**: using [Maxima](https://en.wikipedia.org/wiki/Maxima_(software) "wikipedia:Maxima (software)") and [SymPy](https://en.wikipedia.org/wiki/SymPy "wikipedia:SymPy").
*   **Linear Algebra**: using the [GSL](https://en.wikipedia.org/wiki/GNU_Scientific_Library "wikipedia:GNU Scientific Library"), [SciPy](https://en.wikipedia.org/wiki/SciPy "wikipedia:SciPy") and [NumPy](https://en.wikipedia.org/wiki/NumPy "wikipedia:NumPy").
*   **Statistics**: using [R](https://en.wikipedia.org/wiki/R_(programming_language) "wikipedia:R (programming language)") (through RPy) and SciPy.
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
    *   [2.5 Documentation](#Documentation)
*   [3 Optional additions](#Optional_additions)
    *   [3.1 SageTeX](#SageTeX)
*   [4 Install Sage package](#Install_Sage_package)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 TeX Live does not recognize SageTex](#TeX_Live_does_not_recognize_SageTex)
    *   [5.2 Starting Sage Notebook Server throws an ImportError](#Starting_Sage_Notebook_Server_throws_an_ImportError)
    *   [5.3 sage -i doesn't work](#sage_-i_doesn.27t_work)
    *   [5.4 3D plot fails in notebook](#3D_plot_fails_in_notebook)
*   [6 See also](#See_also)

## Installation

SageMath can be [installed](/index.php/Pacman "Pacman") from the [official repositories](/index.php/Official_repositories "Official repositories"):

*   [sagemath](https://www.archlinux.org/packages/?name=sagemath) contains the command-line version;
*   [sagemath-doc](https://www.archlinux.org/packages/?name=sagemath-doc) for HTML documentation and inline help from the command line.
*   [sage-notebook](https://www.archlinux.org/packages/?name=sage-notebook) includes the browser-based notebook interface.

The [sagemath](https://www.archlinux.org/packages/?name=sagemath) package has number of [optional dependencies](/index.php/Pacman#Installing_packages "Pacman") for various features that will be disabled if the needed packages are missing.

## Usage

SageMath mainly uses Python as a scripting language with a few [modifications](http://www.sagemath.org/doc/tutorial/afterword.html#section-mathannoy) to make it better suited for mathematical computations.

### SageMath command-line

SageMath can be started from the command-line:

```
$ sage

```

For information on the SageMath command-line see [this page](http://www.sagemath.org/doc/reference/cmd/index.html).

The command-line is based on the IPython shell so you can use all its [tricks](http://www.sagemath.org/doc/tutorial/interactive_shell.html) with SageMath. For an extensive tutorial on IPython see the community maintained [IPython Cookbook](http://wiki.ipython.org/Cookbook).

Note, however, that it is not very comfortable for some uses such as plotting. When you try to plot something, for example:

```
sage: plot(sin,(x,0,10))

```

SageMath opens a browser window with the Sage Notebook.

### Sage Notebook

A better suited interface for advanced usage in SageMath is the Notebook. To start the Notebook server from the command-line, execute:

```
$ sage -n

```

The notebook will be accessible in the browser from [http://localhost:8080](http://localhost:8080) and will require you to login.

However, if you only run the server for personal use, and not across the internet, the login will be an annoyance. You can instead start the Notebook without requiring login, and have it automatically pop up in a browser, with the following command:

```
$ sage -c "notebook(automatic_login=True)"

```

For a more comprehensive tutorial on the Sage Notebook see the [Sage documentation](http://www.sagemath.org/doc/reference/notebook/index.html). For more information on the `notebook()` command see [this page](http://www.sagemath.org/doc/reference/notebook/sagenb/notebook/notebook.html).

### Jupyter Notebook

SageMath also provides a kernel for the [Jupyter](https://jupyter.org/) notebook. To use it, install [ipython2-notebook](https://www.archlinux.org/packages/?name=ipython2-notebook) and [mathjax](https://www.archlinux.org/packages/?name=mathjax), launch the notebook with the command

```
$ jupyter notebook

```

and choose "SageMath" in the drop-down "New..." menu. The SageMath Jupyter notebook supports [LaTeX](/index.php/LaTeX "LaTeX") output via the `%display latex` command and 3D plots if [jmol](https://www.archlinux.org/packages/?name=jmol) is installed.

### Cantor

[Cantor](http://edu.kde.org/applications/mathematics/cantor/) is an application included in the KDE Edu Project. It acts as a front-end for various mathematical applications such as Maxima, SageMath, Octave, Scilab, etc. See the [Cantor page](http://wiki.sagemath.org/Cantor) on the Sage wiki for more information on how to use it with SageMath.

Cantor can be installed with the [cantor](https://www.archlinux.org/packages/?name=cantor) package or as part of the [kde-applications](https://www.archlinux.org/groups/x86_64/kde-applications/) or [kdeedu](https://www.archlinux.org/groups/x86_64/kdeedu/) groups, available in the [official repositories](/index.php/Official_repositories "Official repositories").

### Documentation

For local documentation, one can compile it into multiple formats such as HTML or PDF. To build the whole SageMath reference, execute the following command (as root):

```
# sage --docbuild reference html

```

This builds the HTML documentation for the whole _reference_ tree (may take longer than an hour). An option is to build a smaller part of the documentation tree, but you would need to know what it is you want. Until then, you might consider just browsing the [online reference](http://www.sagemath.org/doc/).

For a list of documents see `sage --docbuild --documents` and for a list of supported formats see `sage --docbuild --formats`.

## Optional additions

### SageTeX

If you have installed [TeX Live](/index.php/TeX_Live "TeX Live") on your system, you may be interested in [using SageTeX](http://www.sagemath.org/doc/tutorial/sagetex.html), a package that makes the inclusion of SageMath code in LaTeX files possible. TeX Live is made aware of SageTeX automatically so you can start using it straight away.

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

## Install Sage package

[![Tango-user-trash-full.png](/images/e/ee/Tango-user-trash-full.png)](/index.php/File:Tango-user-trash-full.png)

[![Tango-user-trash-full.png](/images/e/ee/Tango-user-trash-full.png)](/index.php/File:Tango-user-trash-full.png)

**This article or section is being considered for deletion.**

**Reason:** [#Installation](#Installation) now mentions optional dependencies (Discuss in [Talk:SageMath#](https://wiki.archlinux.org/index.php/Talk:SageMath))

If you installed sagemath from the official repositories, it is not possible to install sage packages using the sage option `sage -i packagename`.

Instead, you should install the required packages system-wide. For example, if you need `jmol` (for 3D plots):

```
$ sudo pacman -S jmol

```

An alternative would be to have a local installation of sagemath and to manage optional packages manually.

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

### Starting Sage Notebook Server throws an ImportError

The Sage Notebook Server is in an extra package [sage-notebook](https://www.archlinux.org/packages/?name=sage-notebook). So, if you get an ImportError when launching

```
 % sage --notebook
 ┌────────────────────────────────────────────────────────────────────┐
 │ Sage Version 6.4.1, Release Date: 2014-11-23                       │
 │ Type "notebook()" for the browser-based notebook interface.        │
 │ Type "help()" for help.                                            │
 └────────────────────────────────────────────────────────────────────┘
 Please wait while the Sage Notebook server starts...
 Traceback (most recent call last):
   File "/usr/bin/sage-notebook", line 180, in <module>
     launcher(unknown)
   File "/usr/bin/sage-notebook", line 58, in __init__
     from sagenb.notebook.notebook_object import notebook
 ImportError: No module named sagenb.notebook.notebook_object

```

you most likely do not have the package [sage-notebook](https://www.archlinux.org/packages/?name=sage-notebook) installed.

### sage -i doesn't work

[![Tango-user-trash-full.png](/images/e/ee/Tango-user-trash-full.png)](/index.php/File:Tango-user-trash-full.png)

[![Tango-user-trash-full.png](/images/e/ee/Tango-user-trash-full.png)](/index.php/File:Tango-user-trash-full.png)

**This article or section is being considered for deletion.**

**Reason:** [#Installation](#Installation) now mentions optional dependencies (Discuss in [Talk:SageMath#](https://wiki.archlinux.org/index.php/Talk:SageMath))

If you have installed Sage from the official repositories, then you have to install your additional packages system-wide. See [Install Sage package](/index.php/SageMath#Install_Sage_package "SageMath")

### 3D plot fails in notebook

[![Tango-user-trash-full.png](/images/e/ee/Tango-user-trash-full.png)](/index.php/File:Tango-user-trash-full.png)

[![Tango-user-trash-full.png](/images/e/ee/Tango-user-trash-full.png)](/index.php/File:Tango-user-trash-full.png)

**This article or section is being considered for deletion.**

**Reason:** [#Installation](#Installation) now mentions optional dependencies (Discuss in [Talk:SageMath#](https://wiki.archlinux.org/index.php/Talk:SageMath))

If you get the following error while trying to plot a 3D object:

```
  /usr/lib/python2.7/site-packages/sage/repl/rich_output/display_manager.py:570: RichReprWarning: Exception in _rich_repr_ while displaying
  object: Jmol failed to create file
  '/home/nicolas/.sage/temp/archimede/3188/dir_cCpcph/preview.png', see
  '/home/nicolas/.sage/temp/archimede/3188/tmp_JVpSqF.txt' for details
    RichReprWarning,
  Graphics3d Object

```

then you probably miss the jmol package. See [Install Sage package](/index.php/SageMath#Install_Sage_package "SageMath") to install it.

## See also

*   [Official Website](http://www.sagemath.org/)
*   [SageMath Documentation](http://www.sagemath.org/doc/)
*   [Planet Sage](http://planet.sagemath.org/)
*   [SageMath Wiki](http://wiki.sagemath.org/)
*   [Software Used by SageMath](http://www.sagemath.org/links-components.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=SageMath&oldid=416341](https://wiki.archlinux.org/index.php?title=SageMath&oldid=416341)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Mathematics and science](/index.php/Category:Mathematics_and_science "Category:Mathematics and science")

Hidden category:

*   [Pages or sections flagged with Template:Deletion](/index.php/Category:Pages_or_sections_flagged_with_Template:Deletion "Category:Pages or sections flagged with Template:Deletion")