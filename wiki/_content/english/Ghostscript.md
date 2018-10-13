[Ghostscript](https://en.wikipedia.org/wiki/Ghostscript "wikipedia:Ghostscript") is an interpreter for PostScript and PDF.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 ps2pdf](#ps2pdf)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [ghostscript](https://www.archlinux.org/packages/?name=ghostscript) package.

## Usage

See [gs(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gs.1).

### ps2pdf

*ps2pdf* is a wrapper around ghostscript to convert PostScript to PDF:

```
$ ps2pdf -sPAPERSIZE=a4 -dOptimize=true -dEmbedAllFonts=true YourPSFile.ps

```

Explanation:

*   with `-sPAPERSIZE=something` you define the paper size. For valid PAPERSIZE values, see [[1]](http://ghostscript.com/doc/current/Use.htm#Known_paper_sizes).
*   `-dOptimize=true` let's the created PDF be optimised for loading
*   `-dEmbedAllFonts=true` makes the fonts look always nice

**Note:** You cannot choose the paper orientation in ps2pdf. If your input PS file is healthy, it already contains the orientation information. If you are trying to use an Encapsulated PS file, you will have problems, if it does not fit in the `-sPAPERSIZE` you specified, because EPS files usually do not contain paper orientation informaiton. a workaround is creating a new paper in ghostscript settings (call it e.g. "slide") and use it as `-sPAPERSIZE=slide`.

## See also

*   [Official website](https://www.ghostscript.com/)