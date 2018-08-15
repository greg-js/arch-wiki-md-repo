Related articles

*   [Matlab](/index.php/Matlab "Matlab")
*   [Sage-mathematics](/index.php/Sage-mathematics "Sage-mathematics")
*   [Mathematica](/index.php/Mathematica "Mathematica")

From the [official website](http://www.gnu.org/software/octave/):

	GNU Octave is a high-level interpreted language, primarily intended for numerical computations. It provides capabilities for the numerical solution of linear and nonlinear problems, and for performing other numerical experiments. It also provides extensive graphics capabilities for data visualization and manipulation. Octave is normally used through its interactive command line interface, but it can also be used to write non-interactive programs. The Octave language is quite similar to Matlab so that most programs are easily portable.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Alternative graphical interfaces](#Alternative_graphical_interfaces)
*   [2 Octave-Forge](#Octave-Forge)
    *   [2.1 Using Octave's installer](#Using_Octave.27s_installer)
    *   [2.2 Using the AUR](#Using_the_AUR)
*   [3 Plotting](#Plotting)
*   [4 Reading Microsoft Excel Spreadsheets](#Reading_Microsoft_Excel_Spreadsheets)
    *   [4.1 Converting to CSV format](#Converting_to_CSV_format)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Zsh Undecodable Token](#Zsh_Undecodable_Token)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [octave](https://www.archlinux.org/packages/?name=octave) package.

Run the GUI app with *octave* or the CLI app with *octave-cli*.

### Alternative graphical interfaces

The default *octave* GUI is included in the [octave](https://www.archlinux.org/packages/?name=octave) package. Alternatively, you can use one of the following unofficial GUIs:

*   **Cantor** — A graphical user interface that delegates its mathematical operations to one of several back ends (Scilab, Maxima, Octave and others).

	[http://edu.kde.org/cantor/](http://edu.kde.org/cantor/) || [cantor](https://www.archlinux.org/packages/?name=cantor)

*   **QtOctave** — A Qt frontend for Octave.

	[https://forja.rediris.es/projects/csl-qtoctave/](https://forja.rediris.es/projects/csl-qtoctave/) || [qtoctave](https://aur.archlinux.org/packages/qtoctave/)

## Octave-Forge

Octave provides a set of packages, similar to Matlab's Toolboxes, through [Octave-Forge](http://octave.sourceforge.net/index.html). The complete list of packages is [here](http://octave.sourceforge.net/packages.php).

Packages can be installed [#Using Octave's installer](#Using_Octave.27s_installer) or [#Using the AUR](#Using_the_AUR).

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

Qt is the default plotting backend:

```
>> available_graphics_toolkits
ans =
{
  [1,1] = fltk
  [1,2] = qt
}
>> graphics_toolkit
ans = qt

```

Alternatively you can use either FLTK or Gnuplot backend (by installing [gnuplot](https://www.archlinux.org/packages/?name=gnuplot)) and running the following command:

```
>> graphics_toolkit("gnuplot");

```

To make this change permanent add it to your `~/.octaverc` file.

## Reading Microsoft Excel Spreadsheets

You can open `.ods`, `.xls` and `.xlsx` files with the `odsread` or `xlsread` function, which requires the [octave-io](https://aur.archlinux.org/packages/octave-io/) package:

```
octave:1> odsread('myfile.ods');
octave:1> xlsread('myfile.xls');
octave:1> xlsread('myfile.xlsx');

```

### Converting to CSV format

Alternatively, first convert the files to `.csv` using [LibreOffice](/index.php/LibreOffice "LibreOffice") Calc ([limited](https://bugs.documentfoundation.org/show_bug.cgi?id=50916) to 1024 columns) or [Calligra Sheets](http://www.calligra.org/sheets/) ([calligra](https://www.archlinux.org/packages/?name=calligra), limited to 32768 columns).

After the conversion is complete you can use the build-in Octave function `csvread` for `.csv` files:

```
octave:1> csvread('myfile.csv');

```

## Troubleshooting

### Zsh Undecodable Token

If you get error

```
undecodable token: b(hex)[23m

```

when printing, install [grml-zsh-config](https://www.archlinux.org/packages/?name=grml-zsh-config) and relogin.

## See also

*   [Wikipedia:GNU Octave](https://en.wikipedia.org/wiki/GNU_Octave "wikipedia:GNU Octave")