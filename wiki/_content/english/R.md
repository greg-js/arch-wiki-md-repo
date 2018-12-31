Related articles

*   [R package guidelines](/index.php/R_package_guidelines "R package guidelines")
*   [Intel C++](/index.php/Intel_C%2B%2B "Intel C++")

[R](https://en.wikipedia.org/wiki/R_(programming_language) is a "free software environment for statistical computing and graphics."[[1]](https://www.r-project.org/)

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
    *   [3.1 Environment](#Environment)
    *   [3.2 Profile](#Profile)
    *   [3.3 Locale](#Locale)
*   [4 Managing R packages](#Managing_R_packages)
    *   [4.1 With pacman](#With_pacman)
    *   [4.2 With R](#With_R)
        *   [4.2.1 Upgrading R packages](#Upgrading_R_packages)
            *   [4.2.1.1 Within a R session](#Within_a_R_session)
            *   [4.2.1.2 Within a shell](#Within_a_shell)
    *   [4.3 Makevars](#Makevars)
*   [5 Adding a graphical frontend to R](#Adding_a_graphical_frontend_to_R)
    *   [5.1 R Commander frontend](#R_Commander_frontend)
    *   [5.2 RKWard frontend](#RKWard_frontend)
*   [6 Editors IDEs and notebooks with R support](#Editors_IDEs_and_notebooks_with_R_support)
    *   [6.1 Rstudio IDE](#Rstudio_IDE)
    *   [6.2 Rstudio server](#Rstudio_server)
    *   [6.3 Emacs Speaks Statistics](#Emacs_Speaks_Statistics)
    *   [6.4 Nvim-R](#Nvim-R)
    *   [6.5 Cantor](#Cantor)
    *   [6.6 Jupyter notebook](#Jupyter_notebook)
*   [7 Tips and tricks](#Tips_and_tricks)
    *   [7.1 Optimized packages](#Optimized_packages)
        *   [7.1.1 OpenBLAS](#OpenBLAS)
        *   [7.1.2 Intel MKL](#Intel_MKL)
        *   [7.1.3 intel-advisor-xe](#intel-advisor-xe)
    *   [7.2 Set CRAN mirror across R sessions](#Set_CRAN_mirror_across_R_sessions)
*   [8 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [r](https://www.archlinux.org/packages/?name=r) package. The installation of external packages within the R environment may require [gcc-fortran](https://www.archlinux.org/packages/?name=gcc-fortran).

## Usage

To start a `R` session, open your terminal and type this command:

```
$ R

```

**Note:**

*   Make sure to use a capital R for the command. Note that some shells use the lowercase `r` command to repeat the last entered command. Once in your `R` session, the prompt will change to `>`
*   **site** refers to **system-wide** in R Documentation

Run `?Startup` to read the documentation about system file configuration, `help()` for the on-line help,`help.start()` for the HTML browser interface to help, `demo()` for some demos and `q()` to close the session and quit.

When closing the session, you will be prompted : `Save workspace Image ?[y/n/c]`. The *workspace* is your current working environment and include any user-defined objects, functions. The saved image is stored in `.RData` format and will be automatically reloaded the next time `R` is started. You can manually save the workspace at any time in the session with the `save.image(image.RData)` command, save as many images as you want (eg : *image1.RData*, *image2.RData*). You can load image with the `load.image(image.RData)` command at any time of your session.

**Tip:**

*   Tired of R's verbose startup message ? Then start `R` with the `--quiet` command-line option (`$ R --quiet`). You can add `alias R="R --quiet"` in one of your [Startup files](/index.php/Startup_files "Startup files").
*   Running `R` from the command line will set R's working directory to the current directory. Opening the R GUI will set R's working directory to $HOME, unless explicitly defined in your configuration files (`.Renviron` or `.Rprofile`).

## Configuration

Whenever R starts, its configuration is controlled by several files. Please refer to [Initialization at Start of an R Session](http://stat.ethz.ch/R-manual/R-devel/library/base/html/Startup.html) to get a detailed understanding of startup process.

### Environment

R first loads **site** and **user** environment variable files. The name of the site file is controlled by the [Environment variables](/index.php/Environment_variables "Environment variables") `R_ENVIRON` if it exists, and defaults to `/etc/R/.Renviron`. The name of the user file is specified by `R_ENVIRON_USER`. If that is unset, it defaults to `.Renviron` in the curent working directory or if it exists, and `~/.Renviron` otherwise.

Most important variables can be found on [Environment Variables R Documentation](http://stat.ethz.ch/R-manual/R-devel/library/base/html/EnvVar.html).

You may disable loading environment files with `--no-environ`

Lines in `Renviron` file should be either comment lines starting with **#** or lines of the form *name=value*. Here is a very basic `.Renviron`:

 `.Renviron` 
```
R_HOME_USER = /path/to/your/r/directory
R_PROFILE_USER = ${HOME}/.config/r/.Rprofile
R_LIBS_USER = /path/to/your/r/library
R_HISTFILE = /path/to/your/filename.Rhistory                                             # Do not forget to append the **.Rhistory**
MYSQL_HOME = /var/lib/mysql
```

### Profile

R then loads an Rprofile, which contains R code that is executed. These files are read in the following order of preference (only one file is loaded):

1\. A file specified by the environment variable `R_PROFILE_USER`.

2\. `.Rprofile` in the current working directory.

3\. `$HOME/.Rprofile`.

An `.Rprofile` can contain arbitrary R code, though best practice suggests that one should not load packages at startup, as this hinders package upgrades and reproducibility.

 `~/.Rprofile` 
```
# The .First function is called after everything else in .Rprofile is executed
.First <- function() {
  # Print a welcome message
  message("Welcome back ", Sys.getenv("USER"),"!
","working directory is:", getwd())
}

options(digits = 12)                                          # number of digits to print. Default is 7, max is 15
options(stringsAsFactors = FALSE)                             # Disable default conversion of character strings to factors
options(show.signif.stars = FALSE)                            # Don't show stars indicating statistical significance in model outputs
error <- quote(dump.frames("${R_HOME_USER}/testdump", TRUE))  # post-mortem debugging facilities
```

You can add more [global options](http://stat.ethz.ch/R-manual/R-devel/library/base/html/options.html) to customize your `R` environment. See this [post](http://stackoverflow.com/questions/1189759/expert-r-users-whats-in-your-rprofile) for more examples of user configurations.

### Locale

Aspects of the [Locale](/index.php/Locale "Locale") are accessed by the functions `Sys.getlocale` and `Sys.localeconv` within the `R` session. Locales will be the one defined in your system.

## Managing R packages

There are many add-on `R` packages, which can be browsed on [The R Website.](http://cran.r-project.org/web/packages/available_packages_by_date.html).

**Note:** Some R packages link to files provided by system packages. These packages will need to be reinstalled when these files are updated.

### With pacman

There are some packages available on the [AUR](/index.php/AUR "AUR") with the prefix `r-`. You can mix and match installing R packages with pacman and through R (below), but if you do so you should let pacman manage system packages (those that reside at `/usr/lib/R/library`, and let R manage user-installed packages elsewhere (e.g. `~/R/library`).

### With R

Packages can be installed from within `R` using the `**install.packages(c("pkgname"))**` command. You should use a local library and let pacman manage files that reside under `/usr/lib/R/library`.

**Note:**

*   `**install.packages()**` requires [tk](https://www.archlinux.org/packages/?name=tk) to be [installed](/index.php/Install "Install") for selecting mirrors. Try installing this package if you see:

`Error: .onLoad failed in loadNamespace() for 'tcltk', details (...)`

Within your `R` session, run this command to check that your user library exists and is set correctly:

 `> Sys.getenv("R_LIBS_USER")`  `[1] "/path/to/directory/R/packages"` 

Alternatively, you may install from the command line like so:

 `$ R CMD INSTALL -l $R_LIBS_USER *pkg1 pkg2 ...*` 

#### Upgrading R packages

##### Within a R session

```
> update.packages(ask=FALSE)

```

Or when you also need to rebuild packages which were built for an older version:

```
> update.packages(ask=FALSE,checkBuilt=TRUE)

```

Or when you also need to select a specific mirror ([https://cran.r-project.org/mirrors.html](https://cran.r-project.org/mirrors.html)) to download the packages from (changing the url as need):

```
> update.packages(ask=FALSE,checkBuilt=TRUE,repos="[https://cran.cnr.berkeley.edu/](https://cran.cnr.berkeley.edu/)")

```

**Tip:** upgrading packages from your R session can quickly be a pain if you have too many loaded packages at start up. For packages to be upgraded, they cannot be loaded, so do not load packages from your Rprofile.

##### Within a shell

You can use `Rscript`, which comes with [r](https://www.archlinux.org/packages/?name=r) to update packages from a shell:

 `$ Rscript -e "update.packages()"` 

### Makevars

The Makevars file can be used to set the default make options when installing packages. An example optimized Makevars file is as follow:

 `~/.R/Makevars` 
```
CFLAGS=-O3 -Wall -pedantic -march=native -mtune=native -pipe
CXXFLAGS=-O3 -Wall -pedantic -march=native -mtune=native -pipe
```

## Adding a graphical frontend to R

R does not include a point-and-click graphical user interface for statistics or data manipulation. However, third-party user interfaces for R are available, such as R commander and RKWard.

### R Commander frontend

R Commander is a popular user interface to R. There is no Arch linux package available to install R commander, but it is an R package so it can be installed easily from within R. R Commander requires [tk](https://www.archlinux.org/packages/?name=tk) to be [installed](/index.php/Install "Install").

To install R Commander, run 'R' from the command line. Then type:

```
> install.packages("Rcmdr", dependencies=TRUE)

```

This can take some time.

You can then start R Commander from within R using the library command:

```
> library("Rcmdr")

```

### RKWard frontend

RKWard is an open-source frontend which allows for data import and browsing as well as running common statistical tests and plots. You can install [rkward](https://aur.archlinux.org/packages/rkward/) from [AUR](/index.php/AUR "AUR").

## Editors IDEs and notebooks with R support

### Rstudio IDE

RStudio an open-source R IDE. It includes many modern conveniences such as parentheses matching, tab-completion, tool-tip help popups, and a spreadsheet-like data viewer.

Install [rstudio-desktop-bin](https://aur.archlinux.org/packages/rstudio-desktop-bin/) (binary version from the Rstudio project website) or [rstudio-desktop-git](https://aur.archlinux.org/packages/rstudio-desktop-git/) (development version) from [AUR](/index.php/AUR "AUR").

The R library path is often configured with the R_LIBS environment variable. RStudio ignores this, so the user must set R_LIBS_USER in `~/.Renviron`, as documented above.

### Rstudio server

RStudio Server enables you to provide a browser based interface to a version of R running on a remote Linux server.

Install [rstudio-server-git](https://aur.archlinux.org/packages/rstudio-server-git/). The two main configuration files are `/etc/rstudio/rserver.conf` and `/etc/rstudio/rsession.conf`. They are not created during the install, so you will need to *create* and *edit* them. For information about configure options, please refer to [rstudio getting started](https://support.rstudio.com/hc/en-us/articles/200552306-Getting-Started) documentation.

To start the server, please [enable and start](/index.php/Systemd#Using_units "Systemd") the `rstudio-server.service` unit file provided with the package.

### Emacs Speaks Statistics

[Emacs](/index.php/Emacs "Emacs") users can interact with R via the [emacs-ess](https://aur.archlinux.org/packages/emacs-ess/) package.

### Nvim-R

The [nvim-r](https://aur.archlinux.org/packages/nvim-r/) package allows [vim](https://www.archlinux.org/packages/?name=vim) and [neovim](https://www.archlinux.org/packages/?name=neovim) users to code in R, including editing and rendering of R markdown (Rmd) files, execution of R code in a separate pane, inspection of variables, and integrated help panes.

### Cantor

[cantor](https://www.archlinux.org/packages/?name=cantor) is a notebook application developed by KDE that includes support for R.

### Jupyter notebook

[jupyter-notebook](https://www.archlinux.org/packages/?name=jupyter-notebook) is a browser based notebook with support for many programming languages. R support can be added by installing the [IRkernel](https://github.com/IRkernel/IRkernel).

## Tips and tricks

### Optimized packages

The numerical libraries that comes with the R (generic [blas](https://www.archlinux.org/packages/?name=blas), LAPACK) do not have multithreading capabilities. Replacing the reference [blas](https://www.archlinux.org/packages/?name=blas) package with an optimized BLAS can produce dramatic speed increases for many common computations in R. See these threads for an overview of the potential speed increases:

*   [https://github.com/tmolteno/necpp/issues/18](https://github.com/tmolteno/necpp/issues/18)
*   [http://blog.nguyenvq.com/blog/2014/11/10/optimized-r-and-python-standard-blas-vs-atlas-vs-openblas-vs-mkl/](http://blog.nguyenvq.com/blog/2014/11/10/optimized-r-and-python-standard-blas-vs-atlas-vs-openblas-vs-mkl/)
*   [https://freddie.witherden.org/pages/blas-gemm-bench/](https://freddie.witherden.org/pages/blas-gemm-bench/)
*   [http://nghiaho.com/?p=1726](http://nghiaho.com/?p=1726)

#### OpenBLAS

[openblas](https://www.archlinux.org/packages/?name=openblas) can replace the reference [blas](https://www.archlinux.org/packages/?name=blas). If you are using the regular [r](https://www.archlinux.org/packages/?name=r) package from [extra] no further configuration is needed; R is configured to use the system BLAS and will use OpenBLAS once it is installed.

#### Intel MKL

**If your processors are Intel**, you can use the [Intel math Kernel Library](http://software.intel.com/en-us/intel-mkl). The **MKL**, beyond the capabilities of multithreading, also has specific optimizations for Intel processors. Keep in mind that they can [potentially interfere with the standard R functionality for parallel processing](http://blog.revolutionanalytics.com/2015/10/edge-cases-in-using-the-intel-mkl-and-parallel-programming.html).

Please first [Install](/index.php/Install "Install") the [intel-mkl](https://aur.archlinux.org/packages/intel-mkl/) package available from [AUR](/index.php/AUR "AUR"), then the [r-mkl](https://aur.archlinux.org/packages/r-mkl/) package.

**Note:**

*   if you install the [r-mkl](https://aur.archlinux.org/packages/r-mkl/) with **R** already installed, you will be prompted to remove **R**. Once **r-mkl** is installed, please run on **R** console the following command :

`> update.packages(checkBuilt=TRUE)`

*   here are elapsed time in sec from computing 15 tests with default GCC build and icc/MKL build: *274.93 sec* for GCC build, *21.01 sec* for icc/MKL build. See [this post](https://stat.ethz.ch/pipermail/r-help/2014-September/421574.html) for more information.

#### intel-advisor-xe

[intel-advisor](http://software.intel.com/en-us/intel-advisor-xe) delivers top application performance with C, C++ and Fortran compilers, libraries and analysis tools.

Install the [intel-advisor-xe](https://aur.archlinux.org/packages/intel-advisor-xe/) package.

### Set CRAN mirror across R sessions

Instead of having R ask which CRAN mirror to use every time you install or update a package, you can set the mirror in the Rprofile file. [https://cloud.r-project.org/](https://cloud.r-project.org/) should be a good default for everywhere:

 `~/.Rprofile` 
```
## Set CRAN mirror:
local({
  r <- getOption("repos")
  r["CRAN"] <- "[https://cloud.r-project.org/](https://cloud.r-project.org/)"
  options(repos = r)
})
```

## See also

*   [Official website](https://www.r-project.org/)
*   [RSeek](http://www.rseek.org/) A Google Custom Search Engine for R related material.
*   [R for Data Science](http://r4ds.had.co.nz/) Online version of a CCA licensed book written by Garrett Grolemund and Hadley Wickham from RStudio, 2017.
*   [R-bloggers](https://www.r-bloggers.com/) Aggregation site for (English) blogs related to R.
*   [/r/Rlanguage on Reddit](https://www.reddit.com/r/Rlanguage/) There are several R related Subreddits, each one provides links to the others.