This article covers software to view, edit and convert [PDF](https://en.wikipedia.org/wiki/PDF "wikipedia:PDF"), [PostScript](https://en.wikipedia.org/wiki/PostScript "wikipedia:PostScript") (PS) and [DjVu](https://en.wikipedia.org/wiki/DjVu "wikipedia:DjVu") (*déjà vu*) files.

## Contents

*   [1 Engines](#Engines)
*   [2 Viewers](#Viewers)
    *   [2.1 Discontinued](#Discontinued)
    *   [2.2 Framebuffer](#Framebuffer)
*   [3 Annotation](#Annotation)
*   [4 PDF editors](#PDF_editors)
*   [5 Command-line tools](#Command-line_tools)
    *   [5.1 DjVu tools](#DjVu_tools)
    *   [5.2 Optimize a PDF](#Optimize_a_PDF)
    *   [5.3 Encrypt a PDF](#Encrypt_a_PDF)
    *   [5.4 Decrypt a PDF](#Decrypt_a_PDF)
    *   [5.5 Concatenate PDFs](#Concatenate_PDFs)
    *   [5.6 Extract page range from PDF](#Extract_page_range_from_PDF)
    *   [5.7 Rasterize a PDF](#Rasterize_a_PDF)
*   [6 Libraries](#Libraries)
    *   [6.1 Python](#Python)
*   [7 See also](#See_also)

## Engines

[Poppler](https://en.wikipedia.org/wiki/Poppler_(software) ([poppler](https://www.archlinux.org/packages/?name=poppler)) is a PDF rendering library based on Xpdf. It supports AcroForms, but not full XFA forms.[[1]](https://gitlab.freedesktop.org/poppler/poppler/issues/199)[[2]](https://gitlab.freedesktop.org/poppler/poppler/issues/530) For CJK (Chinese, Japanese, Korean) support with Poppler, [install](/index.php/Install "Install") [poppler-data](https://www.archlinux.org/packages/?name=poppler-data).

[libspectre](https://www.freedesktop.org/wiki/Software/libspectre) ([libspectre](https://www.archlinux.org/packages/?name=libspectre)) is a small library for rendering Postscript documents.

[Ghostscript](https://en.wikipedia.org/wiki/Ghostscript "wikipedia:Ghostscript") ([ghostscript](https://www.archlinux.org/packages/?name=ghostscript)) is an interpreter for PostScript and PDF.

[DjVuLibre](http://djvu.sourceforge.net/) ([djvulibre](https://www.archlinux.org/packages/?name=djvulibre)) is a suite to create, manipulate and view DjVu documents.

## Viewers

**Note:** Some [web browsers](/index.php/Web_browser "Web browser") can display PDF files, for example with [PDF.js](/index.php/Browser_plugins#PDF.js "Browser plugins").

| Name | Package | PDF | PostScript | DjVu | License | Note |
| [apvlv](https://naihe2010.github.io/apvlv/) | [apvlv](https://aur.archlinux.org/packages/apvlv/) | Poppler | – | DjVuLibre | GPLv2 | Has [Vim](/index.php/Vim "Vim") keybindings, supports UMD and TXT files. |
| [Atril](https://github.com/mate-desktop/atril) | [atril](https://www.archlinux.org/packages/?name=atril) | Poppler | libspectre | DjVuLibre | GPLv2 | Fork of Evince, part of [MATE](/index.php/MATE "MATE"), supports DVI, EPS, EPUB, TIFF, XPS and Comicbook. |
| [DjView](http://djvu.sourceforge.net/djview4.html) | [djview](https://www.archlinux.org/packages/?name=djview) | – | – | DjVuLibre | GPLv2 | By the developers of DjVuLibre. |
| [Evince](https://en.wikipedia.org/wiki/Evince "wikipedia:Evince") | [evince](https://www.archlinux.org/packages/?name=evince) | Poppler | libspectre | DjVuLibre | GPLv2 | Part of [GNOME](/index.php/GNOME "GNOME"), supports DVI, EPS, TIFF, XPS and Comicbook. |
| [Foxit Reader](https://en.wikipedia.org/wiki/Foxit_Reader "wikipedia:Foxit Reader") | [foxitreader](https://aur.archlinux.org/packages/foxitreader/) | custom | – | – | proprietary | Small and fast (compared to Acrobat) proprietary PDF viewer. |
| [gv](https://www.gnu.org/software/gv/) | [gv](https://www.archlinux.org/packages/?name=gv) | Ghostscript | – | GPLv3 | Graphical user interface for the Ghostscript interpreter. |
| [llpp](/index.php/Llpp "Llpp") | [llpp](https://www.archlinux.org/packages/?name=llpp) | libmupdf | – | – | GPLv3 | Based on MuPDF, supports continuous page scrolling and bookmarking. |
| [MuPDF](/index.php/MuPDF "MuPDF") | [mupdf](https://www.archlinux.org/packages/?name=mupdf) | custom | – | – | AGPLv3 | Supports EPUB, FictionBook, XPS, Comicbook and CJK. |
| [Okular](https://en.wikipedia.org/wiki/Okular "wikipedia:Okular") | [okular](https://www.archlinux.org/packages/?name=okular) | Poppler | libspectre | DjVuLibre | GPL, LGPL | Part of [KDE](/index.php/KDE "KDE"), supports CHM, Comicbook, DVI, EPUB, FictionBook, Mobipocket, ODT, Plucker, TIFF and XPS. |
| [pdfpc](https://pdfpc.github.io/) | [pdfpc](https://www.archlinux.org/packages/?name=pdfpc) | Poppler | – | – | GPLv2 | Presenter console with multi-monitor support for PDF files. |
| [qpdfview](https://launchpad.net/qpdfview) | [qpdfview](https://www.archlinux.org/packages/?name=qpdfview) | Poppler | libspectre* | DjVuLibre* | GPLv2 | Tabbed Qt interface, supports CUPS printing. |
| [Xpdf](https://en.wikipedia.org/wiki/Xpdf "wikipedia:Xpdf") | [xpdf](https://www.archlinux.org/packages/?name=xpdf) | custom | – | – | GPLv3 | Can decode LZW and read encrypted PDFs. |
| [Xreader](https://github.com/linuxmint/xreader/) | [xreader](https://www.archlinux.org/packages/?name=xreader) | Poppler | libspectre* | DjVuLibre* | GPLv2 | Fork of Evince, developed by Linux Mint, supports DVI, EPUB, TIFF, XPS and Comicbook. |
| [Zathura](/index.php/Zathura "Zathura") | [zathura](https://www.archlinux.org/packages/?name=zathura) | Poppler* / libmupdf* | libspectre* | DjVuLibre* | zlib | Customizable with plugins, functional, supports Comicbook. |

	(* means optional)

### Discontinued

*   **[Adobe Reader](https://en.wikipedia.org/wiki/Adobe_Reader "wikipedia:Adobe Reader")** — Discontinued proprietary PDF file viewer by Adobe, supports both AcroForms and XFA forms.

	[https://www.adobe.com/products/reader.html](https://www.adobe.com/products/reader.html) || [acroread](https://aur.archlinux.org/packages/acroread/)

*   **ePDFView** — Lightweight PDF document viewer using the Poppler and GTK+ libraries. Development stopped.

	[http://freecode.com/projects/epdfview](http://freecode.com/projects/epdfview) || [epdfview](https://www.archlinux.org/packages/?name=epdfview)

### Framebuffer

*   **fbgs** — Poor man's PostScript/pdf viewer for the linux framebuffer console.

	[https://www.kraxel.org/blog/linux/fbida/](https://www.kraxel.org/blog/linux/fbida/) || [fbida](https://www.archlinux.org/packages/?name=fbida)

*   **fbpdf** — Small framebuffer PDF and DjVu viewer based off of MuPDF, with [Vim](/index.php/Vim "Vim") keybindings and written in C

	[http://repo.or.cz/w/fbpdf.git](http://repo.or.cz/w/fbpdf.git) || [fbpdf-git](https://aur.archlinux.org/packages/fbpdf-git/)

*   **JFBView** — Framebuffer PDF and image viewer. Features include Vim-like controls, zoom-to-fit, a TOC (outline) view, fast multi-threaded rendering and asynchronous pre-caching. Originally a fork of *fbpdf* called *jfbpdf*, now completely rewritten.

	[https://seasonofcode.com/pages/jfbview.html](https://seasonofcode.com/pages/jfbview.html) || [jfbview](https://aur.archlinux.org/packages/jfbview/)

## Annotation

*   **Cournal** — Collaborative note taking and journal application using a stylus. It allows multiple users to annotate PDF files in real-time.

	[https://github.com/flyser/cournal](https://github.com/flyser/cournal) || [cournal](https://aur.archlinux.org/packages/cournal/)

*   **flpsed** — A PostScript and PDF annotator, only supports text boxes.

	[http://flpsed.org/flpsed.html](http://flpsed.org/flpsed.html) || [flpsed](https://aur.archlinux.org/packages/flpsed/)

*   **Xournal** — Application for notetaking, sketching and keeping a journal using a stylus. Capable of annotating existing PDF files as well.

	[http://xournal.sourceforge.net/](http://xournal.sourceforge.net/) || [xournal](https://www.archlinux.org/packages/?name=xournal)

*   **Xournal++** — Notetaking software designed around a tablet. C++ rewrite of Xournal with PDF annotation support.

	[https://github.com/xournalpp/xournalpp](https://github.com/xournalpp/xournalpp) || [xournalpp-git](https://aur.archlinux.org/packages/xournalpp-git/)

## PDF editors

This section lists applications dedicated to lossless PDF manipulation. Note that other applications like [LibreOffice Draw](/index.php/LibreOffice "LibreOffice"), [Inkscape](/index.php/Inkscape "Inkscape"), [GIMP](/index.php/GIMP "GIMP") or [krita](https://www.archlinux.org/packages/?name=krita) can also import and export PDFs.

*   **Master PDF Editor** — Functional proprietary PDF editor. Free for non-commercial use.

	[https://code-industry.net/free-pdf-editor/](https://code-industry.net/free-pdf-editor/) || [masterpdfeditor](https://aur.archlinux.org/packages/masterpdfeditor/), [masterpdfeditor-qt4](https://aur.archlinux.org/packages/masterpdfeditor-qt4/) for older version without restrictions

*   **PDF Chain** — Graphical interface allowing to manipulate PDF documents (concatenate, burst, watermark, attach files...).

	[http://pdfchain.sourceforge.net/](http://pdfchain.sourceforge.net/) || [pdfchain](https://aur.archlinux.org/packages/pdfchain/)

*   **PDF Mix Tool** — Application to split, merge, rotate and mix PDF files.

	[https://scarpetta.eu/pdfmixtool/](https://scarpetta.eu/pdfmixtool/) || [pdfmixtool](https://aur.archlinux.org/packages/pdfmixtool/)

*   **PDF Mod** — Reorder, rotate, and remove pages, export images from a document, edit the title, subject, author, and keywords, and combine documents via drag and drop.

	[https://wiki.gnome.org/Apps/PdfMod](https://wiki.gnome.org/Apps/PdfMod) || [pdfmod](https://www.archlinux.org/packages/?name=pdfmod)

*   **PDFsam** — Merge, split, rotate, convert, edit, sign PDF files.

	[https://pdfsam.org/](https://pdfsam.org/) || [pdfsam](https://www.archlinux.org/packages/?name=pdfsam)

*   **PDF-Shuffler** — Combine, split, rotate and reorder PDF documents. Uses Python and GTK2.

	[https://sourceforge.net/projects/pdfshuffler/](https://sourceforge.net/projects/pdfshuffler/) || [pdfshuffler](https://www.archlinux.org/packages/?name=pdfshuffler)

*   **PDF Studio** — All-in-one proprietary PDF editor similar to Adobe Acrobat.

	[https://www.qoppa.com/pdfstudio/](https://www.qoppa.com/pdfstudio/) || [pdfstudio](https://aur.archlinux.org/packages/pdfstudio/)

## Command-line tools

*   **[PDFtk](https://en.wikipedia.org/wiki/PDFtk "wikipedia:PDFtk")** — Pdftk is a simple tool for doing everyday things with PDF documents

	[http://www.pdfhacks.com/pdftk](http://www.pdfhacks.com/pdftk) || [pdftk](https://aur.archlinux.org/packages/pdftk/), [pdftk-bin](https://aur.archlinux.org/packages/pdftk-bin/)

*   **[QPDF](https://en.wikipedia.org/wiki/QPDF "wikipedia:QPDF")** — A content-preserving PDF transformation system.

	[https://github.com/qpdf/qpdf](https://github.com/qpdf/qpdf) || [qpdf](https://www.archlinux.org/packages/?name=qpdf)

*   **pdfgrep** — Commandline utility to search text in PDF files.

	[https://pdfgrep.org/](https://pdfgrep.org/) || [pdfgrep](https://www.archlinux.org/packages/?name=pdfgrep)

*   **pdf2svg** — Convert PDF files to SVG files.

	[http://www.cityinthesky.co.uk/opensource/pdf2svg/](http://www.cityinthesky.co.uk/opensource/pdf2svg/) || [pdf2svg](https://www.archlinux.org/packages/?name=pdf2svg)

*   **mupdf-tools** — Tools developed as part of MuPDF, contains [mutool(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mutool.1) and *muraster*.

	[https://mupdf.com](https://mupdf.com) || [mupdf-tools](https://www.archlinux.org/packages/?name=mupdf-tools)

*   [gs(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gs.1) from Ghostscript, see also `/usr/share/doc/ghostscript/*/Use.htm` ([online](https://ghostscript.com/doc/current/Use.htm)). Ghostscript also provides many wrapper scripts like *ps2pdf* and *pdf2ps*.

### DjVu tools

*   DjVuLibre provides many command-line tools, like [ddjvu(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ddjvu.1) for example.
*   **pdf2djvu** — Creates DjVu files from PDF files.

	[https://jwilk.net/software/pdf2djvu](https://jwilk.net/software/pdf2djvu) || [pdf2djvu](https://www.archlinux.org/packages/?name=pdf2djvu)

*   **img2djvu** — Single-pass DjVu encoder based on DjVu Libre and ImageMagick

	[https://github.com/ashipunov/img2djvu](https://github.com/ashipunov/img2djvu) || [img2djvu-git](https://aur.archlinux.org/packages/img2djvu-git/)

### Optimize a PDF

With Ghostscript:

```
$ gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/screen -dNOPAUSE -dQUIET -dBATCH -sOutputFile=out.pdf in.pdf

```

### Encrypt a PDF

The *user password* is used for encryption, the *owner password* to restrict operations once the document is decrypted, for more information, see [Wikipedia:PDF#Security and signatures](https://en.wikipedia.org/wiki/PDF#Security_and_signatures "wikipedia:PDF").

With PDFtk:

```
$ pdftk in.pdf output out.pdf user_pw *password*

```

With QPDF:

```
$ qpdf --encrypt *user_password* *owner_password* *key_length* -- in.pdf out.pdf

```

where `*key_length*` can be 40, 128 or 256.

### Decrypt a PDF

With PDFtk:

```
$ pdftk in.pdf input_pw *password* output out.pdf

```

With QPDF:

```
$ qpdf --decrypt --password=*password* in.pdf out.pdf

```

With Poppler to PostScript:

```
$ pdftops -upw *password* in.pdf out.ps

```

**Tip:** Forgotten passwords might be recovered with [pdfcrack](https://www.archlinux.org/packages/?name=pdfcrack), see [pdfcrack(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pdfcrack.1).

### Concatenate PDFs

With PDFtk:

```
$ pdftk one.pdf two.pdf three.pdf cat output out.pdf

```

With Poppler:

```
$ pdfunite one.pdf two.pdf three.pdf out.pdf

```

With QPDF:

```
$ qpdf --empty --pages one.pdf two.pdf three.pdf -- out.pdf

```

### Extract page range from PDF

With PDFtk as a single file:

```
$ pdftk *infile*.pdf cat *first*-*last* output *outfile*.pdf

```

With Poppler as separate files:

```
$ pdfseparate -f *first* -l *last* *infile*.pdf *outfileroot*-%d.pdf

```

With QPDF as a single file:

```
$ qpdf --empty --pages *infile*.pdf *first*-*last* -- *outfile*.pdf

```

### Rasterize a PDF

With [GraphicsMagick](/index.php/GraphicsMagick "GraphicsMagick") to convert a specific page:

```
$ gm convert -density *dpi* *infile*.pdf[*page*] *outfile*.jpg

```

With Poppler to convert all pages:

```
$ pdftoppm -jpeg -r *dpi* in.pdf *infile*.pdf *outfileroot*

```

With Poppler to convert a specific page:

```
$ pdftoppm -jpeg -r *dpi* in.pdf -f *page* -singlefile *infile*.pdf *outfileroot*

```

## Libraries

*   **libharu** — C library for generating PDF documents.

	[https://github.com/libharu/libharu](https://github.com/libharu/libharu) || [libharu](https://www.archlinux.org/packages/?name=libharu), Lua binding: [lua-hpdf](https://aur.archlinux.org/packages/lua-hpdf/)

### Python

*   **pdfrw** — A pure Python library that reads and writes PDFs.

	[https://github.com/pmaupin/pdfrw](https://github.com/pmaupin/pdfrw) || [python-pdfrw](https://www.archlinux.org/packages/?name=python-pdfrw), [python2-pdfrw](https://www.archlinux.org/packages/?name=python2-pdfrw)

*   **PyPDF2** — PDF toolkit

	[https://mstamy2.github.com/PyPDF2](https://mstamy2.github.com/PyPDF2) || [python-pypdf2](https://aur.archlinux.org/packages/python-pypdf2/)

*   **PyX** — Python library for the creation of PostScript and PDF files.

	[http://pyx.sourceforge.net](http://pyx.sourceforge.net) || [python-pyx](https://www.archlinux.org/packages/?name=python-pyx), [python2-pyx](https://www.archlinux.org/packages/?name=python2-pyx)

*   **ReportLab** — A proven industry-strength PDF generating solution

	[https://bitbucket.org/rptlab/reportlab](https://bitbucket.org/rptlab/reportlab) || [python-reportlab](https://www.archlinux.org/packages/?name=python-reportlab), [python2-reportlab](https://www.archlinux.org/packages/?name=python2-reportlab)

## See also

*   [Wikipedia:List of PDF software](https://en.wikipedia.org/wiki/List_of_PDF_software "wikipedia:List of PDF software")