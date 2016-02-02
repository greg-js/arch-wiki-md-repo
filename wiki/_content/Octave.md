# Octave

Related articles

*   [Matlab](/index.php/Matlab "Matlab")
*   [Sage-mathematics](/index.php/Sage-mathematics "Sage-mathematics")
*   [Mathematica](/index.php/Mathematica "Mathematica")

From the [official website](http://www.gnu.org/software/octave/):

	_GNU Octave is a high-level interpreted language, primarily intended for numerical computations. It provides capabilities for the numerical solution of linear and nonlinear problems, and for performing other numerical experiments. It also provides extensive graphics capabilities for data visualization and manipulation. Octave is normally used through its interactive command line interface, but it can also be used to write non-interactive programs. The Octave language is quite similar to Matlab so that most programs are easily portable._

## Contents

*   [1 Installation](#Installation)
*   [2 Octave-Forge](#Octave-Forge)
    *   [2.1 Using Octave's installer](#Using_Octave.27s_installer)
    *   [2.2 Using the AUR](#Using_the_AUR)
*   [3 Plotting](#Plotting)
*   [4 Graphical interfaces](#Graphical_interfaces)
    *   [4.1 Bug in Documentation tab](#Bug_in_Documentation_tab)
*   [5 Reading Microsoft Excel Spreadsheets](#Reading_Microsoft_Excel_Spreadsheets)
    *   [5.1 Converting to an open format](#Converting_to_an_open_format)
    *   [5.2 Reading xls files directly from Octave](#Reading_xls_files_directly_from_Octave)
        *   [5.2.1 Steps necessary to make Java Interface available](#Steps_necessary_to_make_Java_Interface_available)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Zsh Undecodable Token](#Zsh_Undecodable_Token)

## Installation

Octave can be [installed](/index.php/Pacman "Pacman") with the package [octave](https://www.archlinux.org/packages/?name=octave), available in the [official repositories](/index.php/Official_repositories "Official repositories").

**Note:** By default the `octave` command provided by this package attempts to run the gui and fails if you haven't installed [qscintilla](https://www.archlinux.org/packages/?name=qscintilla), which is needed for the gui. To start the command line interface run the `octave-cli` command instead.

## Octave-Forge

Octave provides a set of packages, similar to Matlab's Toolboxes, through [Octave-Forge](http://octave.sourceforge.net/index.html). The complete list of packages is [here](http://octave.sourceforge.net/packages.php).

Packages can be installed directly in Octave, or from the AUR. See below.

### Using Octave's installer

Packages can be managed using Octave's installer. They are installed to ~/octave, or in a system directory with the -global option. To install a package:

```
octave:1> pkg install -forge packagename

```

**Note:** Some Octave's packages, like `control`, need the [gcc-fortran](https://www.archlinux.org/packages/?name=gcc-fortran) ArchLinux's package in order to compile and install.

To uninstall a package:

```
octave:3> pkg uninstall packagename

```

Some packages get loaded automatically by Octave, for those which do not:

```
octave:4> pkg load packagename

```

or

```
octave:5> pkg load all

```

To see which packages have been loaded use `pkg list`, the packages with an asterisk are the ones that are already loaded.

A way to make sure that all packages gets loaded at Octave startup:

 `/usr/share/octave/site/m/startup/octaverc` 

```
## System-wide startup file for Octave.
##
## This file should contain any commands that should be executed each
## time Octave starts for every user at this site. 
 pkg load all
```

### Using the AUR

Some packages may be found in the AUR ([search packages](https://aur.archlinux.org/packages.php?O=0&K=octave-&do_Search=Go)). New Octave-forge packages for Arch can be created semi-automatically using the [Octave-forge helper scripts for Archlinux](https://github.com/drizzd/octave-forge-archlinux#readme).

## Plotting

Octave has two official plotting backends:

*   **[Gnuplot](https://en.wikipedia.org/wiki/Gnuplot "wikipedia:Gnuplot")** — A classic Linux plotting utility.

	[http://www.gnuplot.info/](http://www.gnuplot.info/) || [gnuplot](https://www.archlinux.org/packages/?name=gnuplot)

*   **FLTK Backend** — A new experimental OpenGL backend based on the [FLTK](https://en.wikipedia.org/wiki/FLTK "wikipedia:FLTK") GUI toolkit.

	[http://www.gnu.org/software/octave/](http://www.gnu.org/software/octave/) || [octave](https://www.archlinux.org/packages/?name=octave)

**Note:** To enable the FLTK backend, you need to install the [fltk](https://www.archlinux.org/packages/?name=fltk) package. This package now comes as a dependency of octave.

FLTK is now the default plotting utility, but due to some serious problems with the experimental interface, you may want to re-enable gnuplot.

```
octave:1> graphics_toolkit("gnuplot");

```

To make this change permanent add it to your `~/.octaverc` file.

## Graphical interfaces

Since Octave 3.8, Octave has its own (experimental) GUI based on Qt. Since the 4.0.0 release, it is enabled by default. To start the GUI, just run `octave`.

The following GUIs are unofficial.

*   **Cantor** — A graphical user interface that delegates its mathematical operations to one of several back ends (Scilab, Maxima, Octave and others).

	[http://edu.kde.org/cantor/](http://edu.kde.org/cantor/) || [cantor](https://www.archlinux.org/packages/?name=cantor)

*   **QtOctave** — A Qt frontend for Octave.

	[https://forja.rediris.es/projects/csl-qtoctave/](https://forja.rediris.es/projects/csl-qtoctave/) || [qtoctave](https://aur.archlinux.org/packages/qtoctave/)<sup><small>AUR</small></sup>

### Bug in Documentation tab

As of Octave version 3.8.1, clinking a link in the Documentation tab of the official GUI causes the GUI to freeze. According to [bug report #38305](https://savannah.gnu.org/bugs/?38305), this is caused by a signal handler conflict between Octave and Qt.

One [workaround](https://lists.gnu.org/archive/html/help-octave/2014-03/msg00049.html) is to unzip the Octave Info files located at `/usr/share/info/octave.info*` with the command:

```
# gunzip /usr/share/info/octave.info*

```

Another option is to ignore the Documentation tab and use a different Info reader.

## Reading Microsoft Excel Spreadsheets

There are several ways to read Microsoft Excel files with Octave.

#### Converting to an open format

The easiest way to use `.xls` files in Octave would be to convert them to `.csv` or `.ods` using Calc (limited to 1024 columns) from [LibreOffice](/index.php/LibreOffice "LibreOffice") or [Sheets](http://www.calligra.org/sheets/)(limited to 32768 columns) from the the [Calligra Suite](http://www.calligra-suite.org/).

After the conversion is complete you can use the build-in Octave function `csvread` for `.csv` files:

```
octave:1> csvread('myfile.csv');

```

For `.ods` files the [octave-io](https://aur.archlinux.org/packages/octave-io/)<sup><small>AUR</small></sup> package is necessary which contains the `odsread` function:

```
octave:1> odsread('myfile.ods');

```

For `.xlsx` files you can use the [xlsx2csv](https://aur.archlinux.org/packages/xlsx2csv/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/xlsx2csv)]</sup> package from [AUR](/index.php/AUR "AUR"):

```
 xlsx2csv -t /path/to/save/location -x /path/to/myfile.xlsx 

```

#### Reading xls files directly from Octave

If you must work with XLS files and you cannot convert them to CSV or ODS, for whatever reason, you can use the `xlsread` function from the [octave-io](https://aur.archlinux.org/packages/octave-io/)<sup><small>AUR</small></sup> package.

Since [octave-io](https://aur.archlinux.org/packages/octave-io/)<sup><small>AUR</small></sup> version 1.2.5., an interface called 'OCT' was added, which perform reading .xlsx (not .xls!), ods and .gnumeric without any dependencies. However, the Java-based interface still exist (special for reading .xls files and writing those file formats).

##### Steps necessary to make Java Interface available

The steps necessary to make it work are:

	1\. [Install](/index.php/Install "Install") [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk), available in the [official repositories](/index.php/Official_repositories "Official repositories").

**Note:** A common problem is that Octave cannot find the JDK path. To fix this execute the following commands in your shell:

```
$ export JAVA_HOME=/usr/lib/jvm/java-7-openjdk

```

You may also want to add this to your `~/.bashrc` and append it to your `PATH`.

	2\. Install a Java XLS library for `xlsread`. There are more such libraries available, a comparison can be found at [here](http://octave.org/wiki/index.php?title=IO_package#Comparison_of_interfaces_.26_usage). The recommended library is [apache-poi](https://aur.archlinux.org/packages/apache-poi/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/apache-poi)]</sup>, available in the [AUR](/index.php/AUR "AUR").

To check if Java is working correctly in Octave, see the output of:

```
 octave:1> javaclasspath 
  STATIC JAVA PATH
     - empty -
  DYNAMIC JAVA PATH
     - empty -

```

To load the selected library in Octave, check if it is in the Java path. If not:

```
 octave:1> javaaddpath path/to/file.jar

```

In the case you chose [apache-poi](https://aur.archlinux.org/packages/apache-poi/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/apache-poi)]</sup>, the relevant JAR files can be found in `/usr/share/java/apache-poi/poi-3.x.jar` and `/usr/share/java/apache-poi/poi-ooxml-3.x.jar`.

To check if it works

```
 octave:1> chk_spreadsheet_support 

```

The output should be > 0:

```
                   0 No spreadsheet I/O support found
                 ---------- XLS (Excel) interfaces: ----------
                   1 = COM (ActiveX / Excel)
                   2 = POI (Java / Apache POI)
                   4 = POI+OOXML (Java / Apache POI)
                   8 = JXL (Java / JExcelAPI)
                  16 = OXS (Java / OpenXLS)
                 --- ODS (OpenOffice.org Calc) interfaces ----
                  32 = OTK (Java/ ODF Toolkit)
                  64 = JOD (Java / jOpenDocument)
                 ----------------- XLS & ODS: ----------------
                 128 = UNO (Java / UNO bridge - OpenOffice.org)

```

To make this permanent add the `javaaddpath` commands to your `~/.octaverc` file.

## Troubleshooting

### Zsh Undecodable Token

If you get error

```
undecodable token: b(hex)[23m

```

when printing, install [grml-zsh-config](https://www.archlinux.org/packages/?name=grml-zsh-config) and relogin.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Octave&oldid=416116](https://wiki.archlinux.org/index.php?title=Octave&oldid=416116)"