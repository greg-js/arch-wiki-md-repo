Related articles

*   [llpp](/index.php/Llpp "Llpp")

[MuPDF](https://en.wikipedia.org/wiki/MuPDF "w:MuPDF") is a lightweight PDF viewer and toolkit written in portable C. It also reads XPS, OpenXPS and ePub documents.

The renderer in MuPDF is tailored for high quality anti-aliased graphics. It renders text with metrics and spacing accurate to within fractions of a pixel for the highest fidelity in reproducing the look of a printed page on screen.

MuPDF supports all static functions required by PDF 1.7 and is a lightweight alternative to poppler based pdf applications.

## Installation

[Install](/index.php/Install "Install") the [mupdf](https://www.archlinux.org/packages/?name=mupdf) package, [mupdf-gl](https://www.archlinux.org/packages/?name=mupdf-gl) for the OpenGL backend, or [mupdf-git](https://aur.archlinux.org/packages/mupdf-git/) for the development version.

## Usage

The application is ran from the command-line with `mupdf filename.pdf`. Supported arguments are `-d *password*` for required passwords, `-z N%` for the Zoomlevel and `-p N` for the first selected page. See [mupdf(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mupdf.1) for details.

Navigation within a file works through keyboard shortcuts and mouse interaction.

When zoomed in, the document can be moved by using the left mouse button. Pressing the right mouse button while moving the mouse will mark an area, and all text will be copied and can be inserted by clicking the middle mouse button.

Press `I` to invert colours with [mupdf-gl](https://www.archlinux.org/packages/?name=mupdf-gl) and `/` to search.

## See also

*   [MuPDF website](http://mupdf.com/)
*   [Poppler website](http://poppler.freedesktop.org/)
*   [Page „PDF reference“ from Adobe](http://www.adobe.com/devnet/pdf/pdf_reference.html)