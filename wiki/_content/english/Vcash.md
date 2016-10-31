Vcash is a decentralized currency.

## Installation

Vcash currently only compiles correctly using gcc-5, when compiled with gcc-6 it exits with a segfault error.

To avoid this problem, [Install](/index.php/Install "Install") the [gcc5](https://www.archlinux.org/packages/?name=gcc5) package, and then follow the instruction at the project GitHub page for manual compiling at Linux, when requested to run bjam use the toolbox=gcc-5 instead of toolbox=gcc parameter.