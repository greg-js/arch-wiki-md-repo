This article covers software to view, edit and convert [PDF](https://en.wikipedia.org/wiki/PDF "wikipedia:PDF"), [PostScript](https://en.wikipedia.org/wiki/PostScript "wikipedia:PostScript") (PS), [DjVu](https://en.wikipedia.org/wiki/DjVu "wikipedia:DjVu") (*déjà vu*) and [XPS](https://en.wikipedia.org/wiki/Open_XML_Paper_Specification "wikipedia:Open XML Paper Specification") files.

## Contents

*   [1 Engines](#Engines)
*   [2 Viewers](#Viewers)
    *   [2.1 Framebuffer](#Framebuffer)
    *   [2.2 Graphical](#Graphical)
        *   [2.2.1 Comparison](#Comparison)
        *   [2.2.2 PDF forms](#PDF_forms)
*   [3 Annotation](#Annotation)
*   [4 Graphical PDF editing](#Graphical_PDF_editing)
    *   [4.1 Simple editors](#Simple_editors)
    *   [4.2 Cropping tools](#Cropping_tools)
    *   [4.3 Advanced editors](#Advanced_editors)
*   [5 PDF tools](#PDF_tools)
    *   [5.1 Create a PDF from images](#Create_a_PDF_from_images)
    *   [5.2 Concatenate PDFs](#Concatenate_PDFs)
    *   [5.3 Convert a PDF to text](#Convert_a_PDF_to_text)
    *   [5.4 Decrypt a PDF](#Decrypt_a_PDF)
    *   [5.5 Encrypt a PDF](#Encrypt_a_PDF)
    *   [5.6 Extract images from a PDF](#Extract_images_from_a_PDF)
    *   [5.7 Extract page range from PDF](#Extract_page_range_from_PDF)
    *   [5.8 Imposing a PDF](#Imposing_a_PDF)
    *   [5.9 Inspecting metadata](#Inspecting_metadata)
    *   [5.10 Optimize a PDF](#Optimize_a_PDF)
    *   [5.11 Rasterize a PDF](#Rasterize_a_PDF)
    *   [5.12 Splitting PDF pages](#Splitting_PDF_pages)
*   [6 DjVu tools](#DjVu_tools)
    *   [6.1 Convert DjVu to images](#Convert_DjVu_to_images)
    *   [6.2 Processing images](#Processing_images)
    *   [6.3 Make DjVu from images](#Make_DjVu_from_images)
*   [7 PostScript tools](#PostScript_tools)
    *   [7.1 ps2pdf](#ps2pdf)
*   [8 Libraries](#Libraries)
    *   [8.1 Python](#Python)
*   [9 See also](#See_also)

## Engines

*   **[Poppler](https://en.wikipedia.org/wiki/Poppler_(software) "wikipedia:Poppler (software)")** — PDF rendering library based on Xpdf. For CJK (Chinese, Japanese, Korean) support with Poppler, [install](/index.php/Install "Install") [poppler-data](https://www.archlinux.org/packages/?name=poppler-data).

	[https://poppler.freedesktop.org/](https://poppler.freedesktop.org/) || [poppler](https://www.archlinux.org/packages/?name=poppler)

*   **libspectre** — Small library for rendering Postscript documents.

	[https://www.freedesktop.org/wiki/Software/libspectre](https://www.freedesktop.org/wiki/Software/libspectre) || [libspectre](https://www.archlinux.org/packages/?name=libspectre)

*   **[Ghostscript](https://en.wikipedia.org/wiki/Ghostscript "wikipedia:Ghostscript")** — Interpreter for PostScript and PDF. Provides the [gs(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gs.1) command-line interface, see also `/usr/share/doc/ghostscript/*/Use.htm` ([online](https://ghostscript.com/doc/current/Use.htm)), along with many wrapper scripts like *ps2pdf* and *pdf2ps*.

	[https://ghostscript.com/](https://ghostscript.com/) || [ghostscript](https://www.archlinux.org/packages/?name=ghostscript)

*   **DjVuLibre** — Suite to create, manipulate and view DjVu documents.

	[http://djvu.sourceforge.net/](http://djvu.sourceforge.net/) || [djvulibre](https://www.archlinux.org/packages/?name=djvulibre)

*   **libgxps** — GObject based library for handling and rendering XPS documents.

	[https://wiki.gnome.org/Projects/libgxps](https://wiki.gnome.org/Projects/libgxps) || [libgxps](https://www.archlinux.org/packages/?name=libgxps)

## Viewers

### Framebuffer

*   **fbgs** — Poor man's PostScript/pdf viewer for the linux framebuffer console.

	[https://www.kraxel.org/blog/linux/fbida/](https://www.kraxel.org/blog/linux/fbida/) || [fbida](https://www.archlinux.org/packages/?name=fbida)

*   **fbpdf** — Small framebuffer PDF and DjVu viewer based off of MuPDF, with [Vim](/index.php/Vim "Vim") keybindings and written in C

	[http://repo.or.cz/w/fbpdf.git](http://repo.or.cz/w/fbpdf.git) || [fbpdf-git](https://aur.archlinux.org/packages/fbpdf-git/)

*   **JFBView** — Framebuffer PDF and image viewer. Features include Vim-like controls, zoom-to-fit, a TOC (outline) view, fast multi-threaded rendering and asynchronous pre-caching. Originally a fork of *fbpdf* called *jfbpdf*, now completely rewritten.

	[https://seasonofcode.com/pages/jfbview.html](https://seasonofcode.com/pages/jfbview.html) || [jfbview](https://aur.archlinux.org/packages/jfbview/)

### Graphical

**Note:** Some [web browsers](/index.php/Web_browser "Web browser") can display PDF files, for example with [PDF.js](/index.php/Browser_plugins#PDF.js "Browser plugins").

*   **[Adobe Reader](https://en.wikipedia.org/wiki/Adobe_Reader "wikipedia:Adobe Reader")** — Proprietary PDF file viewer offered by Adobe. Discontinued for Linux.

	[http://www.adobe.com/products/reader.html](http://www.adobe.com/products/reader.html) || [acroread](https://aur.archlinux.org/packages/acroread/)

*   **apvlv** — Lightweight document viewer with [Vim](/index.php/Vim "Vim") keybindings. Supports PDF, DjVu, UMD and TXT.

	[https://naihe2010.github.io/apvlv/](https://naihe2010.github.io/apvlv/) || [apvlv](https://aur.archlinux.org/packages/apvlv/)

*   **Atril** — Simple multi-page document viewer for MATE. Supports DjVu, DVI, EPS, EPUB, PDF, PostScript, TIFF, XPS and Comicbook.

	[https://github.com/mate-desktop/atril](https://github.com/mate-desktop/atril) || [atril](https://www.archlinux.org/packages/?name=atril)

*   **DjView** — Viewer for DjVu documents.

	[http://djvu.sourceforge.net/djview4.html](http://djvu.sourceforge.net/djview4.html) || [djview](https://www.archlinux.org/packages/?name=djview)

*   **ePDFView** — Lightweight PDF document viewer using the Poppler and GTK+ libraries. Development stopped.

	[http://freecode.com/projects/epdfview](http://freecode.com/projects/epdfview) || [epdfview](https://www.archlinux.org/packages/?name=epdfview)

*   **[Emacs](/index.php/Emacs "Emacs")** — See also [pdf-tools](https://github.com/politza/pdf-tools) for improved pdf support and the [djvu package](https://elpa.gnu.org/packages/djvu.html) for djvu support.

	[https://www.gnu.org/software/emacs/](https://www.gnu.org/software/emacs/) || [emacs](https://www.archlinux.org/packages/?name=emacs)

*   **[Evince](https://en.wikipedia.org/wiki/Evince "wikipedia:Evince")** — Document viewer for GNOME. Supports DjVu, DVI, EPS, PDF, PostScript, TIFF, XPS and Comicbook.

	[https://wiki.gnome.org/Apps/Evince](https://wiki.gnome.org/Apps/Evince) || [evince](https://www.archlinux.org/packages/?name=evince)

*   **[Foxit Reader](https://en.wikipedia.org/wiki/Foxit_Reader "wikipedia:Foxit Reader")** — Small, fast (compared to Acrobat) proprietary PDF viewer.

	[https://www.foxitsoftware.com/pdf-reader/](https://www.foxitsoftware.com/pdf-reader/) || [foxitreader](https://aur.archlinux.org/packages/foxitreader/)

*   **gv** — Graphical user interface for the Ghostscript interpreter that allows to view and navigate through PostScript and PDF documents.

	[https://www.gnu.org/software/gv/](https://www.gnu.org/software/gv/) || [gv](https://www.archlinux.org/packages/?name=gv)

*   **[llpp](/index.php/Llpp "Llpp")** — Very fast PDF reader based off of MuPDF, that supports continuous page scrolling, bookmarking, and text search through the whole document.

	[http://repo.or.cz/w/llpp.git](http://repo.or.cz/w/llpp.git) || [llpp](https://www.archlinux.org/packages/?name=llpp)

*   **[MuPDF](/index.php/MuPDF "MuPDF")** — Very fast EPUB, FictionBook, PDF, XPS and Comicbook viewer written in portable C. Features CJK font support.

	[https://mupdf.com/](https://mupdf.com/) || [mupdf](https://www.archlinux.org/packages/?name=mupdf)

*   **[Okular](https://en.wikipedia.org/wiki/Okular "wikipedia:Okular")** — Universal document viewer for KDE. Supports CHM, Comicbook, DjVu, DVI, EPUB, FictionBook, Mobipocket, ODT, PDF, Plucker, PostScript, TIFF and XPS.

	[https://okular.kde.org/](https://okular.kde.org/) || [okular](https://www.archlinux.org/packages/?name=okular)

*   **pdfpc** — Presenter console with multi-monitor support for PDF files.

	[https://pdfpc.github.io/](https://pdfpc.github.io/) || [pdfpc](https://www.archlinux.org/packages/?name=pdfpc)

*   **qpdfview** — Tabbed document viewer. It uses Poppler for PDF support, libspectre for PS support, DjVuLibre for DjVu support, CUPS for printing support and the Qt toolkit for its interface.

	[https://launchpad.net/qpdfview](https://launchpad.net/qpdfview) || [qpdfview](https://www.archlinux.org/packages/?name=qpdfview)

*   **[Xpdf](https://en.wikipedia.org/wiki/Xpdf "wikipedia:Xpdf")** — Viewer that can decode LZW and read encrypted PDFs.

	[http://www.xpdfreader.com/](http://www.xpdfreader.com/) || [xpdf](https://www.archlinux.org/packages/?name=xpdf)

*   **Xreader** — Document viewer part of the X-Apps Project. Supports DjVu, DVI, EPUB, PDF, PostScript, TIFF, XPS, Comicbook.

	[https://github.com/linuxmint/xreader/](https://github.com/linuxmint/xreader/) || [xreader](https://www.archlinux.org/packages/?name=xreader)

*   **[Zathura](/index.php/Zathura "Zathura")** — Highly customizable and functional document viewer (plugin based). Supports PDF, DjVu, PostScript and Comicbook.

	[https://pwmt.org/projects/zathura/](https://pwmt.org/projects/zathura/) || [zathura](https://www.archlinux.org/packages/?name=zathura)

#### Comparison

| Name | PDF | PostScript | DjVu | XPS | PDF forms | License |
| [Adobe Reader](https://en.wikipedia.org/wiki/Adobe_Reader "wikipedia:Adobe Reader") | custom | ✘ | ✘ | ✘ | ✔ | proprietary |
| apvlv | Poppler | ✘ | DjVuLibre | ✘ | ✘ | GPLv2 |
| Atril | Poppler | libspectre | DjVuLibre | libgxps | ✔ | GPLv2 |
| DjView | ✘ | ✘ | DjVuLibre | ✘ | ✘ | GPLv2 |
| [Emacs](/index.php/Emacs "Emacs") | Ghostscript* | DjVuLibre* | ✘ | ✘ | GPLv3 |
| ePDFView | Poppler | ✘ | ✘ | ✘ | ✘ | GPLv2 |
| [Evince](https://en.wikipedia.org/wiki/Evince "wikipedia:Evince") | Poppler | libspectre | DjVuLibre | libgxps | ✔ | GPLv2 |
| [Foxit Reader](https://en.wikipedia.org/wiki/Foxit_Reader "wikipedia:Foxit Reader") | custom | ✘ | ✘ | ✘ | ✔ | proprietary |
| gv | Ghostscript | ✘ | ✘ | ✘ | GPLv3 |
| [llpp](/index.php/Llpp "Llpp") | libmupdf | ✘ | ✘ | libmupdf | ✔ | GPLv3 |
| [MuPDF](/index.php/MuPDF "MuPDF") | custom | ✘ | ✘ | custom | ✔ | AGPLv3 |
| [Okular](https://en.wikipedia.org/wiki/Okular "wikipedia:Okular") | Poppler | libspectre | DjVuLibre | custom | ✔ | GPL, LGPL |
| pdfpc | Poppler | ✘ | ✘ | ✘ | ✘ | GPLv2 |
| qpdfview | Poppler | libspectre* | DjVuLibre* | ✘ | ✔ | GPLv2 |
| [Xpdf](https://en.wikipedia.org/wiki/Xpdf "wikipedia:Xpdf") | custom | ✘ | ✘ | ✘ | ✘ | GPLv3 |
| Xreader | Poppler | libspectre* | DjVuLibre* | libgxps* | ✔ | GPLv2 |
| [Zathura](/index.php/Zathura "Zathura") | Poppler* / libmupdf* | libspectre* | DjVuLibre* | libmupdf* | ✔ | zlib |

	(* means optional)

#### PDF forms

The *PDF forms* column in the above table refers to [AcroForms](https://en.wikipedia.org/wiki/PDF#AcroForms "wikipedia:PDF") support. If you do not need your input to be directly extractable from the PDF, you can also use the applications in [#Annotation](#Annotation) or [#Graphical PDF editing](#Graphical_PDF_editing) to put text on top of a PDF. PDF forms can be created with [LibreOffice Writer](/index.php/LibreOffice "LibreOffice") (*View > Toolbars > Form Controls*) and the [advanced PDF editors](#Advanced_editors).

The proprietary and deprecated [XFA](https://en.wikipedia.org/wiki/PDF#Adobe_XML_Forms_Architecture_.28XFA.29 "wikipedia:PDF") format for forms, is not fully support by Poppler[[1]](https://gitlab.freedesktop.org/poppler/poppler/issues/199)[[2]](https://gitlab.freedesktop.org/poppler/poppler/issues/530) and only supported by [Adobe Reader](#Graphical) and [Master PDF Editor](#Advanced_editors).

## Annotation

*   **flpsed** — A PostScript and PDF annotator, only supports text boxes.

	[http://flpsed.org/flpsed.html](http://flpsed.org/flpsed.html) || [flpsed](https://aur.archlinux.org/packages/flpsed/)

See also [List of applications/Documents#Stylus note-taking](/index.php/List_of_applications/Documents#Stylus_note-taking "List of applications/Documents").

## Graphical PDF editing

*   [Scribus](/index.php/Scribus "Scribus") can import and export PDF; text is imported as polygons.[[3]](https://wiki.scribus.net/canvas/Importing_PDF_files_as_Vector_Graphics)
*   [LibreOffice Draw](/index.php/LibreOffice "LibreOffice") can import and export PDF; text is imported as text; embedded fonts are substituted.[[4]](https://bugs.documentfoundation.org/show_bug.cgi?id=82163)[[5]](https://ask.libreoffice.org/en/question/38991/garbled-text-when-opening-pdfs-in-draw/)
*   [Inkscape](/index.php/Inkscape "Inkscape") can import a single page from a PDF and export to PDF; text is imported as cloned glyphs or text; with the latter embedded fonts are substituted.
*   Graphics editors like [GIMP](/index.php/GIMP "GIMP") and [krita](https://www.archlinux.org/packages/?name=krita) can also import and export PDFs at the cost of [rasterization](https://en.wikipedia.org/wiki/Raster_graphics "wikipedia:Raster graphics").

### Simple editors

*   **pdfarranger** — Helps merge or split pdf documents and rotate, crop and rearrange pages. It's a maintained fork of PDF-Shuffler.

	[https://github.com/jeromerobert/pdfarranger](https://github.com/jeromerobert/pdfarranger) || [pdfarranger](https://www.archlinux.org/packages/?name=pdfarranger)

*   **PDF Chain** — GTK front-end for [PDFtk](#PDF_tools), written in C++, supporting concatenation, burst, watermarks, attaching files and more.

	[http://pdfchain.sourceforge.net/](http://pdfchain.sourceforge.net/) || [pdfchain](https://aur.archlinux.org/packages/pdfchain/)

*   **PDF Mix Tool** — Qt front-end for [PoDoFo](#Libraries), written in C++, supports splitting, merging, rotating and mixing PDF files.

	[https://scarpetta.eu/pdfmixtool/](https://scarpetta.eu/pdfmixtool/) || [pdfmixtool](https://aur.archlinux.org/packages/pdfmixtool/)

*   **PDF Mod** — Reorder, rotate, and remove pages, export images from a document, edit the title, subject, author, and keywords, and combine documents via drag and drop.

	[https://wiki.gnome.org/Apps/PdfMod](https://wiki.gnome.org/Apps/PdfMod) || [pdfmod](https://www.archlinux.org/packages/?name=pdfmod)

*   **PDFsam** — Open source application, written in Java, supports merging, splitting and rotating.

	[https://pdfsam.org/](https://pdfsam.org/) || [pdfsam](https://www.archlinux.org/packages/?name=pdfsam)

### Cropping tools

*   **briss** — Java GUI to crop pages of PDF documents to one or more regions selected.

	[http://sourceforge.net/projects/briss/](http://sourceforge.net/projects/briss/) || [briss](https://aur.archlinux.org/packages/briss/)

*   **krop** — Simple graphical tool to crop the pages of PDF files.

	[http://arminstraub.com/software/krop](http://arminstraub.com/software/krop) || [krop](https://aur.archlinux.org/packages/krop/)

*   **PdfHandoutCrop** — Tool to crop pdf handout with multiple pages per sheet.

	[https://cges30901.github.io/pdfhandoutcrop/](https://cges30901.github.io/pdfhandoutcrop/) || [pdfhandoutcrop](https://aur.archlinux.org/packages/pdfhandoutcrop/)

### Advanced editors

*   **Master PDF Editor** — Functional proprietary PDF editor. Free for non-commercial use.

	[https://code-industry.net/free-pdf-editor/](https://code-industry.net/free-pdf-editor/) || [masterpdfeditor](https://aur.archlinux.org/packages/masterpdfeditor/), [masterpdfeditor-qt4](https://aur.archlinux.org/packages/masterpdfeditor-qt4/) for older version without restrictions

*   **PDF Studio** — All-in-one proprietary PDF editor similar to Adobe Acrobat.

	[https://www.qoppa.com/pdfstudio/](https://www.qoppa.com/pdfstudio/) || [pdfstudio](https://aur.archlinux.org/packages/pdfstudio/)

## PDF tools

*   **[PDFtk](https://en.wikipedia.org/wiki/PDFtk "wikipedia:PDFtk")** — Simple tool for doing everyday things with PDF documents

	[http://www.pdfhacks.com/pdftk](http://www.pdfhacks.com/pdftk) || [pdftk](https://aur.archlinux.org/packages/pdftk/), [pdftk-bin](https://aur.archlinux.org/packages/pdftk-bin/)

*   **Stapler** — Light alternative to PDFtk using the [PyPDF2](#Python) library.

	[https://github.com/hellerbarde/stapler](https://github.com/hellerbarde/stapler) || [stapler](https://aur.archlinux.org/packages/stapler/), [stapler-git](https://aur.archlinux.org/packages/stapler-git/)

*   **[QPDF](https://en.wikipedia.org/wiki/QPDF "wikipedia:QPDF")** — Content-preserving PDF transformation system.

	[https://github.com/qpdf/qpdf](https://github.com/qpdf/qpdf) || [qpdf](https://www.archlinux.org/packages/?name=qpdf)

*   **pdfgrep** — Commandline utility to search text in PDF files.

	[https://pdfgrep.org/](https://pdfgrep.org/) || [pdfgrep](https://www.archlinux.org/packages/?name=pdfgrep)

*   **pdf2svg** — Convert PDF files to SVG files.

	[http://www.cityinthesky.co.uk/opensource/pdf2svg/](http://www.cityinthesky.co.uk/opensource/pdf2svg/) || [pdf2svg](https://www.archlinux.org/packages/?name=pdf2svg)

*   **mupdf-tools** — Tools developed as part of MuPDF, contains [mutool(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mutool.1) and *muraster*.

	[https://mupdf.com](https://mupdf.com) || [mupdf-tools](https://www.archlinux.org/packages/?name=mupdf-tools)

*   [pdfjam](http://mirrors.ctan.org/support/pdfjam/PDFjam-README.html) from [texlive-core](https://www.archlinux.org/packages/?name=texlive-core) can be used to n-up, join, rotate and flip PDFs and arrange them into a format suitable for book binding.
*   [Ghostscript](#Engines)

### Create a PDF from images

With [GraphicsMagick](/index.php/GraphicsMagick "GraphicsMagick"):

```
$ gm convert 1.jpg 2.jpg 3.jpg out.pdf

```

### Concatenate PDFs

With Ghostscript:

```
$ gs -dNOPAUSE -sDEVICE=pdfwrite -sOUTPUTFILE=out.pdf -dBATCH 1.pdf 2.pdf 3.pdf

```

With PDFtk:

```
$ pdftk 1.pdf 2.pdf 3.pdf cat output out.pdf

```

With Poppler:

```
$ pdfunite 1.pdf 2.pdf 3.pdf out.pdf

```

With QPDF:

```
$ qpdf --empty --pages 1.pdf 2.pdf 3.pdf -- out.pdf

```

### Convert a PDF to text

With Poppler and maintaining the layout:

```
$ pdftotext -layout in.pdf out.txt

```

See also [pdftotext(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pdftotext.1).

### Decrypt a PDF

This section lists commands to decrypt a PDF to an unencrypted file. Note that most [PDF viewers](#Viewers) also support encrypted PDFs.

With PDFtk:

```
$ pdftk in.pdf input_pw *password* output out.pdf

```

With Poppler to PostScript:

```
$ pdftops -upw *password* in.pdf out.ps

```

With QPDF:

```
$ qpdf --decrypt --password=*password* in.pdf out.pdf

```

**Tip:** Forgotten passwords might be recovered with [pdfcrack](https://www.archlinux.org/packages/?name=pdfcrack), see [pdfcrack(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pdfcrack.1).

### Encrypt a PDF

The *user password* is used for encryption, the *owner password* to restrict operations once the document is decrypted, for more information, see [Wikipedia:PDF#Security and signatures](https://en.wikipedia.org/wiki/PDF#Security_and_signatures "wikipedia:PDF").

With PDFtk:

```
$ pdftk in.pdf output out.pdf user_pw *password*

```

With [PoDoFo](#Libraries):

```
$ podofoencrypt -u *user_password* -o *owner_password* in.pdf out.pdf

```

With QPDF:

```
$ qpdf --encrypt *user_password* *owner_password* *key_length* -- in.pdf out.pdf

```

where `*key_length*` can be 40, 128 or 256.

### Extract images from a PDF

With Poppler to JPEG:

```
$ pdfimages *infile*.pdf -j *outfileroot*

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

### Imposing a PDF

PDF [Imposition](https://en.wikipedia.org/wiki/Imposition "wikipedia:Imposition") can be done with [pdfjam](#PDF_tools), for example paper waste can be reduced with *pdfnup* and *pdfbook* can be used to arrange PDFs into a format suitable for book binding.

### Inspecting metadata

With [ExifTool](/index.php/ExifTool "ExifTool"):

```
$ exiftool file.pdf

```

With Poppler:

```
$ pdfinfo file.pdf

```

### Optimize a PDF

With Ghostscript:

```
$ ps2pdf -dPDFSETTINGS=/screen in.pdf out.pdf

```

For different settings see the [documentation](https://www.ghostscript.com/doc/9.22/VectorDevices.htm#PSPDF_IN).

There is also [shrinkpdf](https://aur.archlinux.org/packages/shrinkpdf/), a third-party wrapper script.

### Rasterize a PDF

With [GraphicsMagick](/index.php/GraphicsMagick "GraphicsMagick") to convert a specific page:

```
$ gm convert -density *dpi* *infile*.pdf[*page*] *outfile*.jpg

```

With Poppler to convert all pages:

```
$ pdftoppm -jpeg -r *dpi* *infile*.pdf *outfileroot*

```

With Poppler to convert a specific page:

```
$ pdftoppm -jpeg -r *dpi* -f *page* -singlefile *infile*.pdf *outfileroot*

```

### Splitting PDF pages

With mupdf-tools to split every page vertically into two pages:

```
$ mutool poster -y 2 in.pdf out.pdf

```

Can be used to undo simple [imposition](#Imposing_a_PDF).

## DjVu tools

*   [DjVuLibre](#Engines) provides many command-line tools, like [ddjvu(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ddjvu.1) for example.
*   **img2djvu** — Single-pass DjVu encoder based on DjVu Libre and ImageMagick

	[https://github.com/ashipunov/img2djvu](https://github.com/ashipunov/img2djvu) || [img2djvu-git](https://aur.archlinux.org/packages/img2djvu-git/)

*   **pdf2djvu** — Creates DjVu files from PDF files.

	[https://jwilk.net/software/pdf2djvu](https://jwilk.net/software/pdf2djvu) || [pdf2djvu](https://www.archlinux.org/packages/?name=pdf2djvu)

### Convert DjVu to images

Break Djvu into separate pages:

```
djvmcvt -i input.djvu /path/to/out/dir output-index.djvu

```

Convert Djvu pages into images:

```
ddjvu --format=tiff page.djvu page.tiff

```

Convert Djvu pages into PDF:

```
ddjvu --format=pdf inputfile.djvu ouputfile.pdf

```

You can also use *--page* to export specific pages:

```
ddjvu --format=tiff --page=1-10 input.djvu output.tiff

```

this will convert pages from 1 to 10 into one tiff file.

### Processing images

You can use [scantailor](https://www.archlinux.org/packages/?name=scantailor) to:

*   fix orientation
*   split pages
*   deskew
*   crop
*   adjust margins

### Make DjVu from images

There is a useful script [img2djvu-git](https://aur.archlinux.org/packages/img2djvu-git/).

```
img2djvu -c1 -d600 -v1 ./out

```

it will create 600dpi out.djvu from all files in ./out directory.

Alternatively, you can try [didjvu](https://aur.archlinux.org/packages/didjvu/), which seems to create smaller files especially on images with well defined background.

## PostScript tools

*   **pstotext** — Converts PostScript files to text.

	[http://www.cs.wisc.edu/~ghost/doc/pstotext.htm](http://www.cs.wisc.edu/~ghost/doc/pstotext.htm) || [pstotext](https://www.archlinux.org/packages/?name=pstotext)

*   [Ghostscript](#Engines)

### ps2pdf

*ps2pdf* is a wrapper around ghostscript to convert PostScript to PDF:

```
$ ps2pdf -sPAPERSIZE=a4 -dOptimize=true -dEmbedAllFonts=true YourPSFile.ps

```

Explanation:

*   with `-sPAPERSIZE=something` you define the paper size. For valid PAPERSIZE values, see [[6]](http://ghostscript.com/doc/current/Use.htm#Known_paper_sizes).
*   `-dOptimize=true` let's the created PDF be optimised for loading
*   `-dEmbedAllFonts=true` makes the fonts look always nice

**Note:** You cannot choose the paper orientation in ps2pdf. If your input PS file is healthy, it already contains the orientation information. If you are trying to use an Encapsulated PS file, you will have problems, if it does not fit in the `-sPAPERSIZE` you specified, because EPS files usually do not contain paper orientation informaiton. a workaround is creating a new paper in ghostscript settings (call it e.g. "slide") and use it as `-sPAPERSIZE=slide`.

## Libraries

*   **libharu** — C library for generating PDF documents.

	[https://github.com/libharu/libharu](https://github.com/libharu/libharu) || [libharu](https://www.archlinux.org/packages/?name=libharu), Lua binding: [lua-hpdf](https://aur.archlinux.org/packages/lua-hpdf/)

*   **PoDoFo** — A C++ library to work with the PDF file format.

	[http://podofo.sourceforge.net](http://podofo.sourceforge.net) || [podofo](https://www.archlinux.org/packages/?name=podofo)

### Python

*   **PDFMiner** — Utils to extract, analyze text data of PDF files. Includes pdf2txt, dumppdf, and latin2ascii

	[http://www.unixuser.org/~euske/python/pdfminer/](http://www.unixuser.org/~euske/python/pdfminer/) || [pdfminer](https://aur.archlinux.org/packages/pdfminer/), [python-pdfminer.six](https://aur.archlinux.org/packages/python-pdfminer.six/)

*   **pdfrw** — A pure Python library that reads and writes PDFs.

	[https://github.com/pmaupin/pdfrw](https://github.com/pmaupin/pdfrw) || [python-pdfrw](https://www.archlinux.org/packages/?name=python-pdfrw), [python2-pdfrw](https://www.archlinux.org/packages/?name=python2-pdfrw)

*   **PyPDF2** — A pure-Python library built as a PDF toolkit.

	[https://mstamy2.github.com/PyPDF2](https://mstamy2.github.com/PyPDF2) || [python-pypdf2](https://www.archlinux.org/packages/?name=python-pypdf2), [python2-pypdf2](https://aur.archlinux.org/packages/python2-pypdf2/)

*   **PyX** — Python library for the creation of PostScript and PDF files.

	[http://pyx.sourceforge.net](http://pyx.sourceforge.net) || [python-pyx](https://www.archlinux.org/packages/?name=python-pyx), [python2-pyx](https://www.archlinux.org/packages/?name=python2-pyx)

*   **ReportLab** — A proven industry-strength PDF generating solution

	[https://bitbucket.org/rptlab/reportlab](https://bitbucket.org/rptlab/reportlab) || [python-reportlab](https://www.archlinux.org/packages/?name=python-reportlab), [python2-reportlab](https://www.archlinux.org/packages/?name=python2-reportlab)

## See also

*   [List of applications/Documents#Readers and viewers](/index.php/List_of_applications/Documents#Readers_and_viewers "List of applications/Documents")
*   [List of applications/Documents#OCR software](/index.php/List_of_applications/Documents#OCR_software "List of applications/Documents")
*   [Wikipedia:List of PDF software](https://en.wikipedia.org/wiki/List_of_PDF_software "wikipedia:List of PDF software")