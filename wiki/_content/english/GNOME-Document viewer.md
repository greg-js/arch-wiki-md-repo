[Document viewer](https://en.wikipedia.org/wiki/Evince "w:Evince") is specifically designed to support the file following formats: PDF, Postscript, djvu, tiff, dvi, XPS, SyncTex support with gedit, comics books (cbr,cbz,cb7 and cbt). For a comprehensive list of formats supported, see [Supported Document Formats](https://wiki.gnome.org/Apps/Evince/SupportedDocumentFormats).

Document viewer uses the poppler library as a backend.

**Note:** Document viewer was previously known as [Evince](https://wiki.gnome.org/Apps/Evince) until the application was given new descriptive names, one for each supported language. The name *Evince* is still used in numerous places such as the executable name, some package names, some desktop entries, and some GSettings schemas.

## Contents

*   [1 Installation](#Installation)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Printer does not show up](#Printer_does_not_show_up)
    *   [2.2 Zoom-in is limited](#Zoom-in_is_limited)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [evince](https://www.archlinux.org/packages/?name=evince) package, or [evince-git](https://aur.archlinux.org/packages/evince-git/) for the development version. Evince installs the gnome-desktop as a dependency

For a standalone version install [evince-no-gnome](https://aur.archlinux.org/packages/evince-no-gnome/) or the light version [evince-light](https://aur.archlinux.org/packages/evince-light/) for pdf support only.

## Troubleshooting

### Printer does not show up

Simply install [gtk3-print-backends](https://www.archlinux.org/packages/?name=gtk3-print-backends).

### Zoom-in is limited

Increasing the page cache size in gnome settings allows the viewer to zoom in farther on large documents. By default, this setting is set relatively small, presumably to accomodate machines with limited amounts of physical memory.

Get the current value of the setting:

gsettings get org.gnome.Evince page-cache-size

Set a new (bigger) value instead, this results in 1-2 Gb of memory usage on a large document:

gsettings set org.gnome.Evince page-cache-size 2000

## See also

*   [Evince website](https://wiki.gnome.org/Apps/Evince)
*   [Poppler website](http://poppler.freedesktop.org/)
*   [Page "PDF reference" from Adobe](http://www.adobe.com/devnet/pdf/pdf_reference.html)