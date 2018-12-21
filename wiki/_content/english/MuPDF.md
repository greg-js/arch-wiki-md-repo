Related articles

*   [llpp](/index.php/Llpp "Llpp")
*   [List of applications/Documents#Readers and viewers](/index.php/List_of_applications/Documents#Readers_and_viewers "List of applications/Documents")

[MuPDF](https://en.wikipedia.org/wiki/MuPDF "w:MuPDF") is a lightweight document viewer and toolkit written in portable C. It supports [PDF](/index.php/PDF "PDF"), XPS, EPUB, XHTML, CBZ, and various image formats such as PNG, JPEG, GIF, and TIFF.

The renderer in MuPDF is tailored for high quality anti-aliased graphics. It renders text with metrics and spacing accurate to within fractions of a pixel for the highest fidelity in reproducing the look of a printed page on screen.

MuPDF supports all static functions required by PDF 1.7 and is a lightweight alternative to poppler based pdf applications.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 MuPDF](#MuPDF)
    *   [2.2 MuPDF GL](#MuPDF_GL)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [mupdf](https://www.archlinux.org/packages/?name=mupdf) package or [mupdf-gl](https://www.archlinux.org/packages/?name=mupdf-gl) for the OpenGL backend and [mupdf-git](https://aur.archlinux.org/packages/mupdf-git/) for the development version. For the document manipulation tools install the [mupdf-tools](https://www.archlinux.org/packages/?name=mupdf-tools) package.

## Usage

See `mupdf --help` or [mupdf(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mupdf.1) and [mutool(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mutool.1) for more information.

**Note:** Options for [mupdf](https://www.archlinux.org/packages/?name=mupdf) and [mupdf-gl](https://www.archlinux.org/packages/?name=mupdf-gl) may differ.

The application is started either from the command-line with `mupdf *filename*.pdf` or from a [file manager](/index.php/List_of_applications/Utilities#File_managers "List of applications/Utilities").

**Tip:** MuPDF can be sandboxed with [Firejail](/index.php/Firejail "Firejail").

Navigation within a document works with standard keyboard shortcuts and mouse interaction. For example, `B` and `Space` scroll up and down.

### MuPDF

Supported arguments are `-d *password*` for required passwords, `-z N%` for the zoom level and `-p N` for the first selected page and more.

When zoomed in, the document can be moved by using the left mouse button. Pressing the right mouse button while moving the mouse will mark an area, and all text will be copied and can be inserted by clicking the middle mouse button.

### MuPDF GL

Press `I` to invert colours. See [[1]](https://mupdf.com/docs/manual-mupdf-gl.html) for the manual or press `F1` for help.

## See also

*   [MuPDF website](http://mupdf.com/)
*   [Poppler website](http://poppler.freedesktop.org/)
*   [Page „PDF reference“ from Adobe](http://www.adobe.com/devnet/pdf/pdf_reference.html)