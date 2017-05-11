[R](http://www.r-project.org/) is a "free software environment for statistical computing and graphics ([http://www.r-project.org/](http://www.r-project.org/))."

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Basic package](#Basic_package)
    *   [1.2 Initial configuration](#Initial_configuration)
    *   [1.3 Variables](#Variables)
        *   [1.3.1 R_ENVIRON](#R_ENVIRON)
        *   [1.3.2 R_PROFILE](#R_PROFILE)
*   [2 Installing R packages](#Installing_R_packages)
    *   [2.1 Upgrading R packages](#Upgrading_R_packages)
        *   [2.1.1 Within a R session](#Within_a_R_session)
        *   [2.1.2 Within a shell](#Within_a_shell)
        *   [2.1.3 Automatically after R upgrades](#Automatically_after_R_upgrades)
*   [3 Configuration files](#Configuration_files)
    *   [3.1 .Renviron](#.Renviron)
    *   [3.2 Rprofile](#Rprofile)
*   [4 Adding a graphical frontend to R](#Adding_a_graphical_frontend_to_R)
    *   [4.1 R Commander frontend](#R_Commander_frontend)
    *   [4.2 RKWard frontend](#RKWard_frontend)
*   [5 Editors IDEs and notebooks with R support](#Editors_IDEs_and_notebooks_with_R_support)
    *   [5.1 Rstudio IDE](#Rstudio_IDE)
    *   [5.2 Rstudio server](#Rstudio_server)
    *   [5.3 Emacs Speaks Statistics](#Emacs_Speaks_Statistics)
    *   [5.4 Nvim-R](#Nvim-R)
    *   [5.5 Cantor](#Cantor)
    *   [5.6 Jupyter notebook](#Jupyter_notebook)
*   [6 Optimized packages](#Optimized_packages)
    *   [6.1 OpenBLAS](#OpenBLAS)
    *   [6.2 Intel MKL](#Intel_MKL)
    *   [6.3 intel-advisor-xe](#intel-advisor-xe)
*   [7 See also](#See_also)

## Installation

### Basic package

[Install](/index.php/Install "Install") the [r](https://www.archlinux.org/packages/?name=r) package. The installation of external packages within the R environment may require [gcc-fortran](https://www.archlinux.org/packages/?name=gcc-fortran).

### Initial configuration

Please refer to [Initialization at Start of an R Session](http://stat.ethz.ch/R-manual/R-devel/library/base/html/Startup.html) to get a detailed understanding of startup process. The home directory of the `R` installation is `/usr/lib/R`. Base packages are found in `/usr/lib/R/library/base` and **site** configuration files in `/etc/R/`. Aspects of the [Locale](/index.php/Locale "Locale") are accessed by the functions `Sys.getlocale` and `Sys.localeconv` within the `R` session. Locales will be the one defined in your system.

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

*   Tired of R's verbose startup message ? Then start `R` with the `--quiet` command-line option (`$ R --quiet`). You can `alias R="R --quiet"` in one of your [Startup files](/index.php/Startup_files "Startup files").
*   Running `R` from the command line will set R's working directory to the current directory. Opening the R GUI will set R's working directory to $HOME, unless explicitly defined in your configuration files (`.Renviron` or `.Rprofile`).
*   To colorize R output, first install the `colorout` package (first do `install.packages("devtools")` if `devtools` package is not installed)...

```
> devtools::install_github('jalvesaq/colorout')

```

...and then add the following to your `.Rprofile` (by default, located in `$HOME/.Rprofile`; create it if it does not exist).

```
# $HOME/.Rprofile 

if (interactive()) {
  # Everything in here is only run if R is in "interactive" (as opposed to batch/script) mode
  library(colorout)
}

```

### Variables

`R` can be confusing when it comes to [environment variables](/index.php/Environment_variables "Environment variables"), as they are large and duplicated following the **site** or **user** sides. There are two sorts of files used in startup: *environment files*, defined by `$R_ENVIRON` and *profile files*, defined by `$R_PROFILE`.

Most important variables can be found on [Environment Variables R Documentation](http://stat.ethz.ch/R-manual/R-devel/library/base/html/EnvVar.html).

#### R_ENVIRON

At startup, `R` search at early stage for **site** and **user** `.Renviron` files to process for setting [environment variables](/index.php/Environment_variables "Environment variables"). The **site** file is located in `/etc/R`, and generated by configure.

The name of the user file can be specified by the `R_ENVIRON_USER` environment variable. If you do not specify any file, `R` will automatically read `.Renviron` in your home directory if there is one. In case you want to use another emplacement for this file, append this line `export R_ENVIRON_USER ="path/to/.Renviron"` in one of your [startup files](/index.php/Startup_files "Startup files"). This is the place to set all kind of environment variables using the **R syntax**.

#### R_PROFILE

Then `R` searches for the **site-wilde** `Rprofile.site` defined by the `R_PROFILE` environment variable. This file does not exist after a fresh installation. Finally, `R` seraches for **user** `R_PROFILE_USER`. if unset, a file called `.Rprofile` is searched for in the current directory, returned by the `R` command `> getwd()` or in the user's home directory. This is the place to put all your custom `R` code.

## Installing R packages

There are many add-on `R` packages, which can be browsed on [The R Website.](http://cran.r-project.org/web/packages/available_packages_by_date.html). They can be installed from within `R` using the `**install.packages(c("pkgname"))**` command. `R` can install its packages locally as **per user** local settings or **system wide**.

**Note:**

*   `**install.packages()**` requires [tk](https://www.archlinux.org/packages/?name=tk) to be [installed](/index.php/Installed "Installed") for selecting mirrors. Try installing this package if you see:

`Error: .onLoad failed in loadNamespace() for 'tcltk', details (...)`

Within your `R` session, run this command to check that your user library exists and is set correctly:

 `> Sys.getenv("R_LIBS_USER")`  `[1] "/path/to/directory/R/packages"` 

Installation within your `R` session is the safest way and will not conflict with the [pacman](/index.php/Pacman "Pacman") package management, but there is another method to install packages. Run the following command in your terminal:

 `$ R CMD INSTALL -l $R_LIBS_USER *pkg1 pkg2 ...*` 

### Upgrading R packages

#### Within a R session

```
> update.packages(ask=FALSE)

```

Or when you also need to rebuild packages which were built for an older version:

```
> update.packages(ask=FALSE,checkBuilt=TRUE)

```

**Tip:** upgrading packages from your **R** session can quickly be a pain if you have too many loaded packages at start up. For packages to be upgraded, they need to be *not loaded*. Best practice is to start a new clean R session this way: `R --vanilla` then run the upgrade.

#### Within a shell

First, [Install](/index.php/Install "Install") [littler](https://aur.archlinux.org/packages/littler/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). This package allows direct execution of **R** commands and can be seen as a scripting front-end. Then, visit [dirk.eddelbuettel](http://dirk.eddelbuettel.com/code/littler.examples.html) webiste about **littler**. Below is the script to run packages updates:

```
#!/usr/bin/env r 
#
# a simple example to update packages in /usr/local/lib/R/site-library
# parameters are easily adjustable

repos <- "[http://cran.rstudio.com](http://cran.rstudio.com)"

lib.loc <- Sys.getenv("R_LIBS_USER")

update.packages(repos=repos, ask=FALSE, lib.loc=lib.loc)

```

Put this script in your favorite place and make it executable. Of course, feel free to modify the repo URL and the library location.

**Warning:** when using [zsh](/index.php/Zsh "Zsh"), **r** is a builtin command. You will have to either use an explicit path `/usr/bin/r` or create an alias under a different name.

#### Automatically after R upgrades

R packages may not be compatible between R versions. You may want to automatically upgrade them and rebuild them if necessary when R upgrades. This can be accomplished with a pacman hook:

 `/etc/pacman.d/hooks/r-upgrade.hook` 
```
[Trigger]
Operation = Upgrade
Type = Package
Target = r

[Action]
Description = Updates R packages and rebuilds them if necessary after R upgrade
# Depends is optional if this should depend on another package
Depends = 
When = PostTransaction
Exec = Rscript -e 'update.packages(checkBuilt = TRUE, ask = FALSE)'

```

## Configuration files

The two user configuration files you want in your home folder are `.Renviron` and `Rprofile.r`. If you want to keep your `$HOME` directory as clean as possible, a good practice will be to make the `~/.config/r` directory, put the `Rprofile.r` file at the root of the directory and append all your `R` code in this file.

### .Renviron

Lines in `Renviron` file should be either comment lines starting with **#** or lines of the form *name=value*.Here is a very basic `.Renviron` you can start with:

 `.Renviron` 
```

R_HOME_USER = /path/to/your/r/directory
R_PROFILE_USER = ${HOME}/.config/r/Rprofile.r
R_LIBS_USER = /path/to/your/r/library
R_HISTFILE = /path/to/your/filename.Rhistory                                             # Do not forget to append the **.Rhistory**
R_DEFAULT_PACKAGES = 'datasets,utils,grDevices,graphics,stats,methods,rJava,colorout'    # load some default packages at start up
MYSQL_HOME = /var/lib/mysql                  

```

### Rprofile

The file `.Rprofile` contains R code that is run automatically at the beginning of each R session. These files are read in the following order of preference (only one file is loaded):

1\. `.Rprofile` in the current working directory.

2\. User `.Rprofile`, typically in `$HOME/.Rprofile`.

3\. Site `.Rprofile`, typically in `/etc/.Rprofile`.

Here is an example `.Rprofile` that defines some useful settings:

 `~/.Rprofile` 
```
# The .First function is called after everything else in .Rprofile is executed
.First <- function() {
  # Print a welcome message
  message("Welcome back ", Sys.getenv("USER"),"!
","working directory is:", getwd())
}

# Always load the 'methods' package
library(methods)

# Load the devtools and colorout packages if in interactive mode
if (interactive()) {
  library(devtools)
  library(colorout)
}

options(prompt = paste(paste(Sys.info()[c("user", "nodename")], collapse = "@"),"[R] "))            # customize your R prompt with username and hostname in this format: user@hostname [R]
options(digits = 12)                                                                                # number of digits to print. Default is 7, max is 15
options(stringsAsFactors = FALSE)                                                                   # Disable default conversion of character strings to factors
options(show.signif.stars = FALSE)                                                                  # Don't show stars indicating statistical significance in model outputs
error <- quote(dump.frames("${R_HOME_USER}/testdump", TRUE))                                        # post-mortem debugging facilities

```

You can add more [global options](http://stat.ethz.ch/R-manual/R-devel/library/base/html/options.html) to customize your `R` environment. See this [post](http://stackoverflow.com/questions/1189759/expert-r-users-whats-in-your-rprofile) for more examples of user configurations.

## Adding a graphical frontend to R

R does not include a point-and-click graphical user interface for statistics or data manipulation. However, third-party user interfaces for R are available, such as R commander and RKWard.

### R Commander frontend

R Commander is a popular user interface to R. There is no Arch linux package available to install R commander, but it is an R package so it can be installed easily from within R. R Commander requires [tk](https://www.archlinux.org/packages/?name=tk) to be [installed](/index.php/Installed "Installed").

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

[emacs](https://www.archlinux.org/packages/?name=emacs) users can interact with R via the [emacs-ess](https://aur.archlinux.org/packages/emacs-ess/) package.

### Nvim-R

The [nvim-r](https://aur.archlinux.org/packages/nvim-r/) package allows [vim](https://www.archlinux.org/packages/?name=vim) and [neovim](https://www.archlinux.org/packages/?name=neovim) users to code in R, including editing and rendering of R markdown (Rmd) files, execution of R code in a separate pane, inspection of variables, and integrated help panes.

### Cantor

[cantor](https://www.archlinux.org/packages/?name=cantor) is a notebook application developed by KDE that includes support for R.

### Jupyter notebook

[jupyter-notebook](https://www.archlinux.org/packages/?name=jupyter-notebook) is a browser based notebook with support for many programming languages. R support can be added by installing the [IRkernel](https://github.com/IRkernel/IRkernel).

## Optimized packages

The numerical libraries that comes with the R (generic [blas](https://www.archlinux.org/packages/?name=blas), LAPACK) do not have multithreading capabilities. Replacing the reference [blas](https://www.archlinux.org/packages/?name=blas) package with an optimized BLAS can produce dramatic speed increases for many common computations in R. However the available optimized BLAS packages all have drawbacks such as requiring a commercial license or [potentially interfering with the standard R functionality for parallel processing](http://blog.revolutionanalytics.com/2015/10/edge-cases-in-using-the-intel-mkl-and-parallel-programming.html). If you really need faster linear algebra in R you may consider the following options.

### OpenBLAS

[openblas](https://aur.archlinux.org/packages/openblas/) can be installed from the [AUR](/index.php/AUR "AUR"), replacing the reference [blas](https://www.archlinux.org/packages/?name=blas) from extra. If you are using the regular [r](https://www.archlinux.org/packages/?name=r) package from extra no further configuration is needed; R is configured to use the system BLAS and will use OpenBLAS once it is installed.

### Intel MKL

**If your processors are Intel**, it is strongly advised to use the [Intel math Kernel Library](http://software.intel.com/en-us/intel-mkl). The **MKL**, beyond the capabilities of multithreading, also has specific optimizations for Intel processors, with performance far superior to traditional libraries.

Please first [Install](/index.php/Install "Install") the [intel-mkl](https://aur.archlinux.org/packages/intel-mkl/) package available from [AUR](/index.php/AUR "AUR"), then the [r-mkl](https://aur.archlinux.org/packages/r-mkl/) package.

**Note:**

*   if you install the [r-mkl](https://aur.archlinux.org/packages/r-mkl/) with **R** already installed, you will be prompted to remove **R**. Once **r-mkl** is installed, please run on **R** console the following command :

`> update.packages(checkBuilt=TRUE)`

*   here are elapsed time in sec from computing 15 tests with default GCC build and icc/MKL build: *274.93 sec* for GCC build, *21.01 sec* for icc/MKL build. See [this post](https://stat.ethz.ch/pipermail/r-help/2014-September/421574.html) for more information.

### intel-advisor-xe

[intel-advisor](http://software.intel.com/en-us/intel-advisor-xe) delivers top application performance with C, C++ and Fortran compilers, libraries and analysis tools.

Install the [intel-advisor-xe](https://aur.archlinux.org/packages/intel-advisor-xe/) package.

## See also

*   [RSeek](http://www.rseek.org/) A search engine for R related material.