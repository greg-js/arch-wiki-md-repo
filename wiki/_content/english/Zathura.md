[Zathura](https://en.wikipedia.org/wiki/Zathura_(document_viewer) "w:Zathura (document viewer)") is a highly customizable and functional document viewer. It provides a minimalistic and space saving interface as well as an easy usage that mainly focuses on keyboard interaction. Different file formats are supported through plugins. Support is available for PDF, DJVU, PS and CB files.

## Contents

*   [1 Installation](#Installation)
*   [2 Features](#Features)
*   [3 Useful tips](#Useful_tips)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [zathura](https://www.archlinux.org/packages/?name=zathura) package as well as those packages that provide the wanted file formats:

Available plugin packages are:

*   [zathura-pdf-poppler](https://www.archlinux.org/packages/?name=zathura-pdf-poppler) or [zathura-pdf-mupdf](https://www.archlinux.org/packages/?name=zathura-pdf-mupdf) for PDF support
*   [zathura-djvu](https://www.archlinux.org/packages/?name=zathura-djvu) for DjVu support
*   [zathura-ps](https://www.archlinux.org/packages/?name=zathura-ps) for PostScript support
*   [zathura-cb](https://www.archlinux.org/packages/?name=zathura-cb) for comic book support

## Features

Zathura automatically reloads documents. When working in compiled documents such as those written in LaTeX, Zathura will refresh the output whenever compilation takes place. Zathura has the option of enabling inverse search (using "synctex").

Zathura can adjust the document to best-fit or to fit width, and it can rotate pages. It can view pages side-by-side and has a fullscreen mode. Pages can also be recolored to have a black background and white foreground.

Zathura can search for text and copy text to the primary X selection. It supports bookmarks and can open encrypted files.

The behavior and appearance of Zathura can be customised using a configuration file. Zathura has the ability to execute external shell commands. It can be opened in tabs using tabbed.

## Useful tips

Commands may be entered directly into Zathura by pushing `:`, just like vi.

Enable copy to clipboard

 ` ~/.config/zathura/zathurarc `  `set selection-clipboard clipboard` 

In side-by-side mode, to view the first page on the left side, enter the command `set first-page-column 1:1` into Zathura. This is particularly useful for reading music scans where typesetting optimizes page-turning on certain pages. Like other Zathura commands, this can go in `zathurarc` as well.

## See also

*   [Zathura website](https://pwmt.org/projects/zathura/)
*   [Poppler website](http://poppler.freedesktop.org/)
*   [Page „PDF reference“ from Adobe](http://www.adobe.com/devnet/pdf/pdf_reference.html)
*   [Keyboard shortcuts](https://github.com/pwmt/zathura/blob/master/doc/man/_bindings.txt)