## Contents

*   [1 Installation](#Installation)
*   [2 How do I create a PDF from PS the easy way?](#How_do_I_create_a_PDF_from_PS_the_easy_way.3F)
*   [3 ps2pdf](#ps2pdf)
    *   [3.1 Explanation](#Explanation)
    *   [3.2 Misconceptions](#Misconceptions)

## Installation

[Install](/index.php/Install "Install") the [ghostscript](https://www.archlinux.org/packages/?name=ghostscript) package.

## How do I create a PDF from PS the easy way?

This page should help people who are asking themselves (maybe for the second, third or n-th time) this question and maybe found the answer once but never have written this somewhere or remembered correctly.

## ps2pdf

One command does it all:

```
ps2pdf -sPAPERSIZE=a4 -dOptimize=true -dEmbedAllFonts=true YourPSFile.ps

```

### Explanation

*   ps2pdf is the wrapper to ghostscript (ps2pdf is owned by ghostscript package)
*   with -sPAPERSIZE=something you define the paper size. Wondering about valid PAPERSIZE values? See [here](http://ghostscript.com/doc/current/Use.htm#Known_paper_sizes)
*   -dOptimize=true let's the created PDF be optimised for loading
*   -dEmbedAllFonts=true makes the fonts look always nice

### Misconceptions

*   you cannot choose the paper orientation in ps2pdf. If your input PS file is healthy, it already contains the orientation information. If you are trying to use an Encapsulated PS file, you will have problems, if it does not fit in the -sPAPERSIZE you specified, because EPS files usually do not contain paper orientation informaiton. a workaround is creating a new paper in ghostscript settings (call it e.g. "slide") and use it as -sPAPERSIZE=slide