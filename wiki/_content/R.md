# R

Related articles

*   [Intel C++](/index.php/Intel_C%2B%2B "Intel C++")

_R is a free software environment for statistical computing and graphics_ ([http://www.r-project.org/](http://www.r-project.org/)).

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
*   [3 Configuration files](#Configuration_files)
    *   [3.1 .Renviron](#.Renviron)
    *   [3.2 Rprofile.r](#Rprofile.r)
*   [4 Adding a graphical frontend to R](#Adding_a_graphical_frontend_to_R)
    *   [4.1 R Commander frontend](#R_Commander_frontend)
    *   [4.2 RKWard frontend](#RKWard_frontend)
    *   [4.3 Rstudio IDE](#Rstudio_IDE)
    *   [4.4 Rstudio server](#Rstudio_server)
    *   [4.5 Emacs Speaks Statistics](#Emacs_Speaks_Statistics)
    *   [4.6 Vim-R](#Vim-R)
*   [5 Optimized packages](#Optimized_packages)
    *   [5.1 OpenBLAS](#OpenBLAS)
    *   [5.2 Intel MKL](#Intel_MKL)
    *   [5.3 intel-advisor-xe](#intel-advisor-xe)
*   [6 See also](#See_also)

## Installation

### Basic package

[Install](/index.php/Install "Install") the [r](https://www.archlinux.org/packages/?name=r) package available in the [official repositories](/index.php/Official_repositories "Official repositories")

Some external packages may require to be compiled in Fortran as well, so [installing](/index.php/Installing "Installing") the [gcc-fortran](https://www.archlinux.org/packages/?name=gcc-fortran) can be a good idea

### Initial configuration

Please refer to [Initialization at Start of an R Session](http://stat.ethz.ch/R-manual/R-devel/library/base/html/Startup.html) to get a detailed understanding of startup process. The home directory of the `R` installation is `/usr/lib/R`. Base packages are found in `/usr/lib/R/library/base` and **site** configuration files in `/etc/R/`. Aspects of the [Locale](/index.php/Locale "Locale") are accessed by the functions `Sys.getlocale` and `Sys.localeconv` within the `R` session. Locales will be the one defined in your system.

To start a `R` session, open your terminal and type this command:

```
$ R

```

**Note:**

*   Use `Shift+u` for the command (some shells use the `r` letter to repeat the last entered command). Once in your `R` session, the prompt will change to `>`
*   **site** refers to **system-wide** in R Documentation

Run `??Startup` to read the documentation about system file configuration, `help()` for the on-line help,`help.start()` for the HTML browser interface to help, `demo()` for some demos and `q()` to close the session and quit.

When closing the session, you will be prompted : `Save workspace Image ?[y/n/c]`. The _workspace_ is your current working environment and include any user-defined objects, functions. The saved image is stored in `.RData` format and will be automatically reloaded the next time `R` is started. You can manually save the workspace at any time in the session with the `save.image(image.RData)` command, save as many images as you want (eg : _image1.RData_, _image2.RData_). You can load image with the `load.image(image.RData)` command at any time of your session.

**Tip:**

*   Tired of R's verbose startup message ? Then start `R` with the `--quiet` command-line option.

`$ R --quiet` You can `alias R ="R --quiet"` in one of your [Startup files](/index.php/Startup_files "Startup files")

*   Unless explicitly defined somewhere in your configuration files, `R` will start in your $HOME directory. If you want to start in a specific directory. first time you create the directory do this:

```
$ R
> setwd("path/to/your/directory")
> q()
Save workspace image? [y/n/c]: y

```

`R` will create a **.RData** image file of your current environment. Then, when double-clicking this file, `R` will automatically change its working directory to the file's directory.

*   colorize console output:

```
> download.file("[http://www.lepem.ufc.br/jaa/vimr/colorout_1.1-1.tar.gz](http://www.lepem.ufc.br/jaa/vimr/colorout_1.1-1.tar.gz)", destfile = "colorout_1.1-1.tar.gz")
> install.packages("colorout_1.1-1.tar.gz", type = "source", repos = NULL)

```

### Variables

`R` can be confusing when it comes to [environment variables](/index.php/Environment_variables "Environment variables"), as they are large and duplicated following the **site** or **user** sides. There are two sorts of files used in startup: _environment files_, defined by `$R_ENVIRON` and _profile files_, defined by `$R_PROFILE`.

Most important variables can be found on [Environment Variables R Documentation](http://stat.ethz.ch/R-manual/R-devel/library/base/html/EnvVar.html).

#### R_ENVIRON

At startup, `R` search at early stage for **site** and **user** `.Renviron` files to process for setting [environment variables](/index.php/Environment_variables "Environment variables"). The **site** file is located in `/etc/R`, and generated by configure.

The name of the user file can be specified by the `R_ENVIRON_USER` environment variable. If you do not specify any file, `R` will automatically read `.Renviron` in your home directory if there is one. In case you want to use another emplacement for this file, append this line `export R_ENVIRON_USER ="path/to/.Renviron"` in one of your [startup files](/index.php/Startup_files "Startup files"). This is the place to set all kind of environment variables using the **R syntax**.

#### R_PROFILE

Then `R` searches for the **site-wilde** `Rprofile.site` defined by the `R_PROFILE` environment variable. This file does not exist after a fresh installation. Finally, `R` seraches for **user** `R_PROFILE_USER`. if unset, a file called `.Rprofile` is searched for in the current directory, returned by the `R` command `> getwd()` or in the user's home directory. This is the place to put all your custom `R` code.

## Installing R packages

There are many add-on `R` packages, which can be browsed on [The R Website.](http://cran.r-project.org/web/packages/available_packages_by_date.html). They can be installed from within `R` using the `**install.packages(c("pkgname"))**` command. `R` can install its packages locally as **per user** local settings or **system wide**.

Within your `R` session, run this command to check that your user library exists and is set correctly:

 `> Sys.getenv("R_LIBS_USER")`  `[1] "/path/to/directory/R/packages"` 

Installation within your `R` session is the safest way and will not conflict with the [pacman](/index.php/Pacman "Pacman") package management, but there is another method to install packages. Run the following command in your terminal:

 `$ R CMD INSTALL -l $R_LIBS_USER _pkg1 pkg2 ..._` 

### Upgrading R packages

#### Within a R session

```
> update.packages(ask=FALSE)

```

Or when you also need to rebuild packages which were built for an older version:

```
> update.packages(ask=FALSE,checkBuilt=TRUE)

```

**Tip:** upgrading packages from your **R** session can quickly be a pain if you have too many loaded packages at start up. For packages to be upgraded, they need to be _not loaded_. Best practice is to start a new clean R session this way: `R --vanilla` then run the upgrade.

#### Within a shell

First, [Install](/index.php/Install "Install") [littler](https://aur.archlinux.org/packages/littler/)<sup><small>AUR</small></sup> from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). This package allows direct execution of **R** commands and can be seen as a scripting front-end. Then, visit [dirk.eddelbuettel](http://dirk.eddelbuettel.com/code/littler.examples.html) webiste about **littler**. Below is the script to run packages updates:

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

## Configuration files

The two user configuration files you want in your home folder are `.Renviron` and `Rprofile.r`. If you want to keep your `$HOME` directory as clean as possible, a good practice will be to make the `~/.config/r` directory, put the `Rprofile.r` file at the root of the directory and append all your `R` code in this file.

### .Renviron

Lines in `Renviron` file should be either comment lines starting with **#** or lines of the form _name=value_.Here is a very basic `.Renviron` you can start with:

 `.Renviron` 

```

R_HOME_USER = /path/to/your/r/directory
R_PROFILE_USER = ${HOME}/.config/r/Rprofile.r
R_LIBS_USER = /path/to/your/r/library
R_HISTFILE = /path/to/your/filename.Rhistory                                             # Do not forget to append the **.Rhistory**
R_DEFAULT_PACKAGES = 'datasets,utils,grDevices,graphics,stats,methods,rJava,colorout'    # load some default packages at start up
MYSQL_HOME = /var/lib/mysql                  

```

### Rprofile.r

For convenient reasons, you can put a specific `Rprofile.r` in each of your usual working directories. One facility would be to dedicate one directory per project, with its specific profile. When `R` will change to the working directory, it will then read the `Rprofile.r` file inside it.

Here is a very short list of useful options and code:

 `Rprofile.r` 

```
setwd("path/to/startup/directory")                                                                   # define a start up working directory
.First <- function(){
#welcome message
message("Welcome back ", Sys.getenv("USER"),"!\n","working directory is:", getwd())
}                                                       
options(prompt = paste(paste (Sys.info () [c ("user", "nodename")], collapse = "@"),"[R] "))         # customize your R prompt with username and hostname in this format: **user@hostname [R]**
options(digits = 12)                                                                                 # number of digits to print. Default is 7, max is 15
options(stringsAsFactors = FALSE)
options(show.signif.stars = FALSE)
error = quote(dump.frames("${R_HOME_USER}/testdump", TRUE))                                          # post-mortem debugiging facilities

```

You can add more [global options](http://stat.ethz.ch/R-manual/R-devel/library/base/html/options.html) to customize your `R` environment. See this [post](http://stackoverflow.com/questions/1189759/expert-r-users-whats-in-your-rprofile) for more user configurations.

## Adding a graphical frontend to R

The linux version of R does not include a graphical user interface. However, third-party user interfaces for R are available, such as R commander and RKWard.

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

RKWard is an open-source frontend which allows for data import and browsing as well as running common statistical tests and plots. You can install [rkward](https://aur.archlinux.org/packages/rkward/)<sup><small>AUR</small></sup> from [AUR](/index.php/AUR "AUR").

### Rstudio IDE

RStudio an open-source R IDE. It includes many modern conveniences such as parentheses matching, tab-completion, tool-tip help popups, and a spreadsheet-like data viewer.

Install [rstudio-desktop-bin](https://aur.archlinux.org/packages/rstudio-desktop-bin/)<sup><small>AUR</small></sup> (binary version from the Rstudio project website) or [rstudio-desktop-git](https://aur.archlinux.org/packages/rstudio-desktop-git/)<sup><small>AUR</small></sup> (development version) from [AUR](/index.php/AUR "AUR").

The R library path is often configured with the R_LIBS environment variable. RStudio ignores this, so the user must set R_LIBS_USER in `~/.Renviron`, as documented above.

### Rstudio server

RStudio Server enables you to provide a browser based interface to a version of R running on a remote Linux server.

Install [rstudio-server-git](https://aur.archlinux.org/packages/rstudio-server-git/)<sup><small>AUR</small></sup>. The two main configuration files are `/etc/rstudio/rserver.conf` and `/etc/rstudio/rsession.conf`. They are not created during the install, so you will need to _create_ and _edit_ them. For information about configure options, please refer to [rstudio getting started](https://support.rstudio.com/hc/en-us/articles/200552306-Getting-Started) documentation.

To start the server, please [enable and start](/index.php/Systemd#Using_units "Systemd") the `rstudio-server.service` unit file provided with the package.

### Emacs Speaks Statistics

[emacs](https://www.archlinux.org/packages/?name=emacs) users can interact with R via the [emacs-ess](https://aur.archlinux.org/packages/emacs-ess/)<sup><small>AUR</small></sup> package.

### Vim-R

The [vim-r](https://aur.archlinux.org/packages/vim-r/)<sup><small>AUR</small></sup> package allows [vim](https://www.archlinux.org/packages/?name=vim) users to code in R, including editing and rendering of R markdown (Rmd) files, execution of R code in a separate pane, inspection of variables, and integrated help panes.

## Optimized packages

The numerical libraries that comes with the R (generic [blas](https://www.archlinux.org/packages/?name=blas), LAPACK) do not have multithreading capabilities. Replacing the reference [blas](https://www.archlinux.org/packages/?name=blas) package with an optimized BLAS can produce dramatic speed increases for many common computations in R. However the available optimized BLAS packages all have drawbacks such as requiring a commercial license or [potentially interfering with the standard R functionality for parallel processing](http://blog.revolutionanalytics.com/2015/10/edge-cases-in-using-the-intel-mkl-and-parallel-programming.html). If you really need faster linear algebra in R you may consider the following options.

### OpenBLAS

[openblas](https://aur.archlinux.org/packages/openblas/)<sup><small>AUR</small></sup> can be installed from the [AUR](/index.php/AUR "AUR"), replacing the reference [blas](https://www.archlinux.org/packages/?name=blas) from extra. If you are using the regular [r](https://www.archlinux.org/packages/?name=r) package from extra no further configuration is needed; R is configured to use the system BLAS and will use OpenBLAS once it is installed.

### Intel MKL

**If your processors are Intel**, it is strongly advised to use the [Intel math Kernel Library](http://software.intel.com/en-us/intel-mkl). The **MKL**, beyond the capabilities of multithreading, also has specific optimizations for Intel processors, with performance far superior to traditional libraries.

Please first [Install](/index.php/Install "Install") the [intel-mkl](https://aur.archlinux.org/packages/intel-mkl/)<sup><small>AUR</small></sup> package available from [AUR](/index.php/AUR "AUR"), then the [r-mkl](https://aur.archlinux.org/packages/r-mkl/)<sup><small>AUR</small></sup> package.

**Note:**

*   if you install the [r-mkl](https://aur.archlinux.org/packages/r-mkl/)<sup><small>AUR</small></sup> with **R** already installed, you will be prompted to remove **R**. Once **r-mkl** is installed, please run on **R** console the following command :

`> update.packages(checkBuilt=TRUE)`

*   here are elapsed time in sec from computing 15 tests with default GCC build and icc/MKL build: _274.93 sec_ for GCC build, _21.01 sec_ for icc/MKL build. See [this post](https://stat.ethz.ch/pipermail/r-help/2014-September/421574.html) for more information.

### intel-advisor-xe

[intel-advisor](http://software.intel.com/en-us/intel-advisor-xe) delivers top application performance with C, C++ and Fortran compilers, libraries and analysis tools.

Install the [intel-advisor-xe](https://aur.archlinux.org/packages/intel-advisor-xe/)<sup><small>AUR</small></sup> package.

## See also

*   [RSeek](http://www.rseek.org/) A search engine for R related material.

Retrieved from "[https://wiki.archlinux.org/index.php?title=R&oldid=414617](https://wiki.archlinux.org/index.php?title=R&oldid=414617)"