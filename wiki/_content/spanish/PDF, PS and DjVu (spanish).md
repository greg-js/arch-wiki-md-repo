**Estado de la traducción**
Este artículo es una traducción de [PDF, PS and DjVu](/index.php/PDF,_PS_and_DjVu "PDF, PS and DjVu"), revisada por última vez el **2020-02-13**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=PDF,_PS_and_DjVu&diff=0&oldid=597443) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Este artículo cubre el software para ver, editar y convertir [PDF](https://en.wikipedia.org/wiki/es:PDF "wikipedia:es:PDF"), [PostScript](https://en.wikipedia.org/wiki/es:PostScript "wikipedia:es:PostScript") (PS), [DjVu](https://en.wikipedia.org/wiki/es:DjVu "wikipedia:es:DjVu") (*déjà vu*) y archivos [XPS](https://en.wikipedia.org/wiki/es:Open_XML_Paper_Specification "wikipedia:es:Open XML Paper Specification").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Motores](#Motores)
*   [2 Visores](#Visores)
    *   [2.1 Framebuffer](#Framebuffer)
    *   [2.2 Gráficos](#Gráficos)
        *   [2.2.1 Comparativa](#Comparativa)
        *   [2.2.2 PDF forms](#PDF_forms)
*   [3 Anotación](#Anotación)
*   [4 Edición gráfica de PDF](#Edición_gráfica_de_PDF)
    *   [4.1 Editores básicos](#Editores_básicos)
    *   [4.2 Herramientas de corte](#Herramientas_de_corte)
    *   [4.3 Editores avanzados](#Editores_avanzados)
*   [5 Herramientas PDF](#Herramientas_PDF)
    *   [5.1 Crea un PDF a partir de imágenes](#Crea_un_PDF_a_partir_de_imágenes)
    *   [5.2 Concatenar PDFs](#Concatenar_PDFs)
    *   [5.3 Convertir un PDF a texto](#Convertir_un_PDF_a_texto)
    *   [5.4 Descifrar un PDF](#Descifrar_un_PDF)
    *   [5.5 Cifrar un PDF](#Cifrar_un_PDF)
    *   [5.6 Extraer imágenes de un PDF](#Extraer_imágenes_de_un_PDF)
    *   [5.7 Extraer un rango de página del PDF, dividir el documento PDF de varias páginas](#Extraer_un_rango_de_página_del_PDF,_dividir_el_documento_PDF_de_varias_páginas)
    *   [5.8 Imponiendo un PDF](#Imponiendo_un_PDF)
    *   [5.9 Inspeccionar metadatos](#Inspeccionar_metadatos)
    *   [5.10 Optimizar, reducir el tamaño de un PDF](#Optimizar,_reducir_el_tamaño_de_un_PDF)
    *   [5.11 Rasterizar un PDF](#Rasterizar_un_PDF)
    *   [5.12 División de páginas PDF](#División_de_páginas_PDF)
    *   [5.13 Añadir firma.png o imagen a una de las páginas del PDF](#Añadir_firma.png_o_imagen_a_una_de_las_páginas_del_PDF)
*   [6 Herramientas DjVu](#Herramientas_DjVu)
    *   [6.1 Convertir DjVu a imágenes](#Convertir_DjVu_a_imágenes)
    *   [6.2 Procesando imágenes](#Procesando_imágenes)
    *   [6.3 Crear DjVu desde imágenes](#Crear_DjVu_desde_imágenes)
*   [7 Herramientas PostScript](#Herramientas_PostScript)
    *   [7.1 ps2pdf](#ps2pdf)
*   [8 Bibliotecas](#Bibliotecas)
    *   [8.1 Python](#Python)
*   [9 Véase también](#Véase_también)

## Motores

*   **[Poppler](https://en.wikipedia.org/wiki/es:Poppler_(software) [poppler-data](https://www.archlinux.org/packages/?name=poppler-data).

	[https://poppler.freedesktop.org/](https://poppler.freedesktop.org/) || [poppler](https://www.archlinux.org/packages/?name=poppler)

*   **libspectre** — Pequeña biblioteca para renderizar documentos PostScript.

	[https://www.freedesktop.org/wiki/Software/libspectre](https://www.freedesktop.org/wiki/Software/libspectre) || [libspectre](https://www.archlinux.org/packages/?name=libspectre)

*   **[Ghostscript](https://en.wikipedia.org/wiki/es:Ghostscript "wikipedia:es:Ghostscript")** — Intérprete para PostScript y PDF. Proporciona la interfaz de línea de órdenes [gs(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gs.1), véase también `/usr/share/doc/ghostscript/*/Use.htm` ([online](https://ghostscript.com/doc/current/Use.htm)), junto con muchos scripts como *ps2pdf* y *pdf2ps*.

	[https://ghostscript.com/](https://ghostscript.com/) || [ghostscript](https://www.archlinux.org/packages/?name=ghostscript)

*   **DjVuLibre** — Suite para crear, manipular y ver documentos DjVu.

	[http://djvu.sourceforge.net/](http://djvu.sourceforge.net/) || [djvulibre](https://www.archlinux.org/packages/?name=djvulibre)

*   **libgxps** — Biblioteca basada en GObject para manejar y renderizar documentos XPS.

	[https://wiki.gnome.org/Projects/libgxps](https://wiki.gnome.org/Projects/libgxps) || [libgxps](https://www.archlinux.org/packages/?name=libgxps)

## Visores

### Framebuffer

*   **fbgs** — Visor de PostScript/pdf de los pobres para la consola framebuffer de Linux.

	[https://www.kraxel.org/blog/linux/fbida/](https://www.kraxel.org/blog/linux/fbida/) || [fbida](https://www.archlinux.org/packages/?name=fbida)

*   **fbpdf** — Pequeño visor de framebuffer PDF y DjVu basado en MuPDF, con atajos de teclado [Vim](/index.php/Vim_(Espa%C3%B1ol) "Vim (Español)") y escrito en C

	[http://repo.or.cz/w/fbpdf.git](http://repo.or.cz/w/fbpdf.git) || [fbpdf-git](https://aur.archlinux.org/packages/fbpdf-git/)

*   **JFBView** — Framebuffer PDF y visor de imágenes. Las características incluyen controles tipo Vim, zoom para ajustar, una vista TOC (esquema), renderizado rápido de subprocesos múltiples y pre-almacenamiento en caché asíncrono. Originalmente una bifurcación de *fbpdf* llamada *jfbpdf*, ahora completamente reescrita.

	[https://seasonofcode.com/pages/jfbview.html](https://seasonofcode.com/pages/jfbview.html) || [jfbview](https://aur.archlinux.org/packages/jfbview/)

### Gráficos

**Nota:** Algunos [navegadores web](/index.php/Web_browser_(Espa%C3%B1ol) "Web browser (Español)") puede mostrar archivos PDF, por ejemplo con [PDF.js](/index.php/Browser_plugins_(Espa%C3%B1ol)#PDF.js "Browser plugins (Español)").

*   **[Adobe Reader](https://en.wikipedia.org/wiki/es:Adobe_Reader "wikipedia:es:Adobe Reader")** — Visor de archivos PDF propietario ofrecido por Adobe. Descontinuado para Linux.

	[http://www.adobe.com/products/reader.html](http://www.adobe.com/products/reader.html) || [acroread](https://aur.archlinux.org/packages/acroread/)

*   **apvlv** — Visor de documentos ligero con atajos de teclado [Vim](/index.php/Vim_(Espa%C3%B1ol) "Vim (Español)"). Soporta PDF, DjVu, UMD y TXT.

	[https://naihe2010.github.io/apvlv/](https://naihe2010.github.io/apvlv/) || [apvlv](https://aur.archlinux.org/packages/apvlv/)

*   **Atril** — Visor de documentos multi-página simple para MATE. Soporta DjVu, DVI, EPS, EPUB, PDF, PostScript, TIFF, XPS y Comicbook.

	[https://github.com/mate-desktop/atril](https://github.com/mate-desktop/atril) || [atril](https://www.archlinux.org/packages/?name=atril)

*   **DjView** — Visor para documentos DjVu.

	[http://djvu.sourceforge.net/djview4.html](http://djvu.sourceforge.net/djview4.html) || [djview](https://www.archlinux.org/packages/?name=djview)

*   **ePDFView** — Visor de documentos PDF ligero utilizando las bibliotecas Poppler y GTK. Desarrollo detenido.

	[http://freecode.com/projects/epdfview](http://freecode.com/projects/epdfview) || [epdfview](https://www.archlinux.org/packages/?name=epdfview)

*   **[Emacs](/index.php/Emacs_(Espa%C3%B1ol) "Emacs (Español)")** — Véase también [pdf-tools](https://github.com/politza/pdf-tools) para mejorar el soporte de pdf y el [paquete djvu](https://elpa.gnu.org/packages/djvu.html) para soporte djvu.

	[https://www.gnu.org/software/emacs/](https://www.gnu.org/software/emacs/) || [emacs](https://www.archlinux.org/packages/?name=emacs)

*   **[Evince](https://en.wikipedia.org/wiki/es:Evince "wikipedia:es:Evince")** — Visor de documentos para GNOME. Soporta DjVu, DVI, EPS, PDF, PostScript, TIFF, XPS y Comicbook.

	[https://wiki.gnome.org/Apps/Evince](https://wiki.gnome.org/Apps/Evince) || [evince](https://www.archlinux.org/packages/?name=evince)

*   **[Foxit Reader](https://en.wikipedia.org/wiki/es:Foxit_Reader "wikipedia:es:Foxit Reader")** — Pequeño, rápido (comparado con Acrobat) visor propietario de PDF.

	[https://www.foxitsoftware.com/pdf-reader/](https://www.foxitsoftware.com/pdf-reader/) || [foxitreader](https://aur.archlinux.org/packages/foxitreader/)

*   **gv** — Interfaz gráfica de usuario para el intérprete Ghostscript que permite ver y navegar por documentos PostScript y PDF.

	[https://www.gnu.org/software/gv/](https://www.gnu.org/software/gv/) || [gv](https://www.archlinux.org/packages/?name=gv)

*   **[llpp](/index.php/Llpp "Llpp")** — Lector de PDF muy rápido basado en MuPDF, que admite desplazamiento continuo de páginas, marcadores y búsqueda de texto en todo el documento.

	[http://repo.or.cz/w/llpp.git](http://repo.or.cz/w/llpp.git) || [llpp](https://www.archlinux.org/packages/?name=llpp)

*   **[MuPDF](/index.php/MuPDF "MuPDF")** — Visor muy rápido de EPUB, FictionBook, PDF, XPS y Comicbook escrito en C portable. Como característica soporta tipografía CJK.

	[https://mupdf.com/](https://mupdf.com/) || [mupdf](https://www.archlinux.org/packages/?name=mupdf)

*   **[Okular](https://en.wikipedia.org/wiki/es:Okular "wikipedia:es:Okular")** — Visor de documentos universal para KDE. Soporta CHM, Comicbook, DjVu, DVI, EPUB, FictionBook, Mobipocket, ODT, PDF, Plucker, PostScript, TIFF y XPS.

	[https://okular.kde.org/](https://okular.kde.org/) || [okular](https://www.archlinux.org/packages/?name=okular)

*   **pdfpc** — Presentador de Consola con soporte multimonitor para archivos PDF.

	[https://pdfpc.github.io/](https://pdfpc.github.io/) || [pdfpc](https://www.archlinux.org/packages/?name=pdfpc)

*   **qpdfview** — Visor de documentos con pestañas. Utiliza Poppler para soporte PDF, libspectre para soporte PS, DjVuLibre para soporte DjVu, CUPS para soporte de impresión y el Qt toolkit para su interfaz.

	[https://launchpad.net/qpdfview](https://launchpad.net/qpdfview) || [qpdfview](https://www.archlinux.org/packages/?name=qpdfview)

*   **[Xpdf](https://en.wikipedia.org/wiki/Xpdf "wikipedia:Xpdf")** — Visor que puede decodificar LZW y leer PDFs cifrados.

	[http://www.xpdfreader.com/](http://www.xpdfreader.com/) || [xpdf](https://www.archlinux.org/packages/?name=xpdf)

*   **Xreader** — Visor de documentos que forma parte del proyecto X-Apps. Soporta DjVu, DVI, EPUB, PDF, PostScript, TIFF, XPS y Comicbook.

	[https://github.com/linuxmint/xreader/](https://github.com/linuxmint/xreader/) || [xreader](https://www.archlinux.org/packages/?name=xreader)

*   **[Zathura](/index.php/Zathura "Zathura")** — Visor de documentos altamente personalizable y funcional (basado en plugin). Soporta PDF, DjVu, PostScript y Comicbook.

	[https://pwmt.org/projects/zathura/](https://pwmt.org/projects/zathura/) || [zathura](https://www.archlinux.org/packages/?name=zathura)

#### Comparativa

| Nombre | PDF | PostScript | DjVu | XPS | PDF Forms | Licencia |
| [Adobe Reader](https://en.wikipedia.org/wiki/es:Adobe_Reader "wikipedia:es:Adobe Reader") | personalizado | ✘ | ✘ | ✘ | ✔ | propietario |
| apvlv | Poppler | ✘ | DjVuLibre | ✘ | ✘ | GPLv2 |
| Atril | Poppler | libspectre | DjVuLibre | libgxps | ✔ | GPLv2 |
| DjView | ✘ | ✘ | DjVuLibre | ✘ | ✘ | GPLv2 |
| [Emacs](/index.php/Emacs_(Espa%C3%B1ol) "Emacs (Español)") | Ghostscript* | DjVuLibre* | ✘ | ✘ | GPLv3 |
| ePDFView | Poppler | ✘ | ✘ | ✘ | ✘ | GPLv2 |
| [Evince](https://en.wikipedia.org/wiki/es:Evince "wikipedia:es:Evince") | Poppler | libspectre | DjVuLibre | libgxps | ✔ | GPLv2 |
| [Foxit Reader](https://en.wikipedia.org/wiki/es:Foxit_Reader "wikipedia:es:Foxit Reader") | personalizado | ✘ | ✘ | ✘ | ✔ | propietario |
| gv | Ghostscript | ✘ | ✘ | ✘ | GPLv3 |
| [llpp](/index.php/Llpp "Llpp") | libmupdf | ✘ | ✘ | libmupdf | ✔ | GPLv3 |
| [MuPDF](/index.php/MuPDF "MuPDF") | personalizado | ✘ | ✘ | custom | ✔ | AGPLv3 |
| [Okular](https://en.wikipedia.org/wiki/es:Okular "wikipedia:es:Okular") | Poppler | libspectre | DjVuLibre | custom | ✔ | GPL, LGPL |
| pdfpc | Poppler | ✘ | ✘ | ✘ | ✘ | GPLv2 |
| qpdfview | Poppler | libspectre* | DjVuLibre* | ✘ | ✔ | GPLv2 |
| [Xpdf](https://en.wikipedia.org/wiki/Xpdf "wikipedia:Xpdf") | personalizado | ✘ | ✘ | ✘ | ✘ | GPLv3 |
| Xreader | Poppler | libspectre* | DjVuLibre* | libgxps* | ✔ | GPLv2 |
| [Zathura](/index.php/Zathura "Zathura") | Poppler* / libmupdf* | libspectre* | DjVuLibre* | libmupdf* | ✘ | zlib |

	(* significa opcional)

#### PDF forms

La columna *PDF Forms* en la tabla anterior se refiere al soporte [AcroForms](https://en.wikipedia.org/wiki/PDF#AcroForms (*Ver > Barras de herramientas > Controles de formulario*) y los [editores de PDF avanzados](#Editores_avanzados).

El formato propietario y en desuso [XFA](https://en.wikipedia.org/wiki/PDF#Adobe_XML_Forms_Architecture_.28XFA.29 "wikipedia:PDF") para formularios, no es totalmente compatible con Poppler[[1]](https://gitlab.freedesktop.org/poppler/poppler/issues/199)[[2]](https://gitlab.freedesktop.org/poppler/poppler/issues/530) y solo es soportado por [Adobe Reader](#Gráficos) y [Master PDF Editor](#Editores_avanzados).

## Anotación

*   **flpsed** — Un anotador PostScript y PDF, solo soporta cajas de texto.

	[http://flpsed.org/flpsed.html](http://flpsed.org/flpsed.html) || [flpsed](https://aur.archlinux.org/packages/flpsed/)

Véase también [List of applications/Documents#Stylus note-taking](/index.php/List_of_applications/Documents#Stylus_note-taking "List of applications/Documents").

## Edición gráfica de PDF

*   [Scribus](/index.php/Scribus_(Espa%C3%B1ol) "Scribus (Español)") puede importar y exportar PDF; el texto se importa como polígonos.[[3]](https://wiki.scribus.net/canvas/Importing_PDF_files_as_Vector_Graphics)
*   [LibreOffice Draw](/index.php/LibreOffice_(Espa%C3%B1ol) "LibreOffice (Español)") puede importar y exportar PDF; el texto se importa como texto; las fuentes incrustadas se sustituyen.[[4]](https://bugs.documentfoundation.org/show_bug.cgi?id=82163)[[5]](https://ask.libreoffice.org/en/question/38991/garbled-text-when-opening-pdfs-in-draw/)
*   [Inkscape](/index.php/Inkscape "Inkscape") puede importar una sola página desde un PDF y exportar a PDF; el texto se importa como glifos clonados o texto; con este último se sustituyen las fuentes incrustadas.
*   Editores gráficos como [GIMP](/index.php/GIMP_(Espa%C3%B1ol) "GIMP (Español)") y [krita](https://www.archlinux.org/packages/?name=krita) también pueden importar y exportar archivos PDF a costa de la [rasterización](https://en.wikipedia.org/wiki/es:Rasterizaci%C3%B3n "wikipedia:es:Rasterización").

### Editores básicos

*   **PDF Arranger** — Ayuda a fusionar o dividir documentos PDF y rotar, recortar y reorganizar páginas. Es una bifurcación mantenida de PDF-Shuffler.

	[https://github.com/jeromerobert/pdfarranger](https://github.com/jeromerobert/pdfarranger) || [pdfarranger](https://www.archlinux.org/packages/?name=pdfarranger)

*   **PDF Chain** — Interfaz GTK para [PDFtk](#Herramientas_PDF), escrito en C++, soportando concatenación, ráfaga, marcas de agua, archivos adjuntos y más.

	[http://pdfchain.sourceforge.net/](http://pdfchain.sourceforge.net/) || [pdfchain](https://aur.archlinux.org/packages/pdfchain/)

*   **PDF Mix Tool** — Interfaz Qt para [PoDoFo](#Bibliotecas), escrito en C++, soporta división, fusión, rotación y mezclado de archivos PDF.

	[https://scarpetta.eu/pdfmixtool/](https://scarpetta.eu/pdfmixtool/) || [pdfmixtool](https://www.archlinux.org/packages/?name=pdfmixtool)

*   **PDF Mod** — Reordenar, rotar y eliminar páginas, exportar imágenes de un documento, editar el título, el tema, el autor y las palabras clave, y combinar documentos mediante arrastrar y soltar.

	[https://wiki.gnome.org/Attic/PdfMod](https://wiki.gnome.org/Attic/PdfMod) || [pdfmod](https://www.archlinux.org/packages/?name=pdfmod)

*   **PDFsam** — Aplicación de código abierto, escrita en Java, soporta fusión, división y rotación.

	[https://pdfsam.org/](https://pdfsam.org/) || [pdfsam](https://www.archlinux.org/packages/?name=pdfsam)

*   **PDF Slicer** — Aplicación simple para extraer, fusionar, rotar y reordenar páginas de documentos PDF.

	[https://junrrein.github.io/pdfslicer/](https://junrrein.github.io/pdfslicer/) || [pdfslicer](https://aur.archlinux.org/packages/pdfslicer/)

*   **PDF Tricks** — Aplicación simple y eficiente para pequeñas manipulaciones en archivos PDF utilizando Ghostscript.

	[https://github.com/muriloventuroso/pdftricks](https://github.com/muriloventuroso/pdftricks) || [pdftricks](https://www.archlinux.org/packages/?name=pdftricks)

### Herramientas de corte

*   **briss** — GUI de Java para recortar páginas de documentos PDF en una o más regiones seleccionadas.

	[http://sourceforge.net/projects/briss/](http://sourceforge.net/projects/briss/) || [briss](https://aur.archlinux.org/packages/briss/)

*   **krop** — Herramienta gráfica simple para recortar las páginas de archivos PDF.

	[http://arminstraub.com/software/krop](http://arminstraub.com/software/krop) || [krop](https://aur.archlinux.org/packages/krop/)

*   **PdfHandoutCrop** — Herramienta para recortar folletos en PDF con varias páginas por hoja.

	[https://cges30901.github.io/pdfhandoutcrop/](https://cges30901.github.io/pdfhandoutcrop/) || [pdfhandoutcrop](https://aur.archlinux.org/packages/pdfhandoutcrop/)

### Editores avanzados

*   **Master PDF Editor** — Editor de PDF funcional y propietario. Gratis para uso no comercial.

	[https://code-industry.net/free-pdf-editor/](https://code-industry.net/free-pdf-editor/) || [masterpdfeditor](https://aur.archlinux.org/packages/masterpdfeditor/)

*   **PDF Studio** — Editor de PDF propietario todo-en-uno similar a Adobe Acrobat.

	[https://www.qoppa.com/pdfstudio/](https://www.qoppa.com/pdfstudio/) || [pdfstudio](https://aur.archlinux.org/packages/pdfstudio/)

## Herramientas PDF

*   **[PDFtk](https://en.wikipedia.org/wiki/es:PDFtk "wikipedia:es:PDFtk")** — Herramienta simple para hacer cosas cotidianas con documentos PDF.

	[http://www.pdfhacks.com/pdftk](http://www.pdfhacks.com/pdftk) || [pdftk](https://www.archlinux.org/packages/?name=pdftk)

*   **Stapler** — Alternativa ligera a PDFtk utilizando la biblioteca [PyPDF2](#Python).

	[https://github.com/hellerbarde/stapler](https://github.com/hellerbarde/stapler) || [stapler](https://aur.archlinux.org/packages/stapler/), [stapler-git](https://aur.archlinux.org/packages/stapler-git/)

*   **[QPDF](https://en.wikipedia.org/wiki/QPDF "wikipedia:QPDF")** — Sistema de transformación de PDF con conservación de contenido.

	[https://github.com/qpdf/qpdf](https://github.com/qpdf/qpdf) || [qpdf](https://www.archlinux.org/packages/?name=qpdf)

*   **pdfgrep** — Utilidad de línea de órdenes para buscar texto en archivos PDF.

	[https://pdfgrep.org/](https://pdfgrep.org/) || [pdfgrep](https://www.archlinux.org/packages/?name=pdfgrep)

*   **pdf2svg** — Convierte archivos PDF a archivos SVG.

	[http://www.cityinthesky.co.uk/opensource/pdf2svg/](http://www.cityinthesky.co.uk/opensource/pdf2svg/) || [pdf2svg](https://www.archlinux.org/packages/?name=pdf2svg)

*   **mupdf-tools** — Herramientas desarrolladas como parte de MuPDF, contienen [mutool(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mutool.1) y *muraster*.

	[https://mupdf.com](https://mupdf.com) || [mupdf-tools](https://www.archlinux.org/packages/?name=mupdf-tools)

*   [pdfjam](http://mirrors.ctan.org/support/pdfjam/PDFjam-README.html) de [texlive-core](https://www.archlinux.org/packages/?name=texlive-core) se puede usar para agrupar (*n-up*), unir, rotar y voltear archivos PDF y organizarlos en un formato adecuado para la encuadernación de libros.
*   [Ghostscript](#Motores)

### Crea un PDF a partir de imágenes

Con [GraphicsMagick](/index.php/GraphicsMagick_(Espa%C3%B1ol) "GraphicsMagick (Español)"):

```
$ gm convert 1.jpg 2.jpg 3.jpg out.pdf

```

### Concatenar PDFs

Con Ghostscript:

```
$ gs -dNOPAUSE -sDEVICE=pdfwrite -sOUTPUTFILE=out.pdf -dBATCH 1.pdf 2.pdf 3.pdf

```

Con PDFtk:

```
$ pdftk 1.pdf 2.pdf 3.pdf cat output out.pdf

```

Con Poppler:

```
$ pdfunite 1.pdf 2.pdf 3.pdf out.pdf

```

Con QPDF:

```
$ qpdf --empty --pages 1.pdf 2.pdf 3.pdf -- out.pdf

```

### Convertir un PDF a texto

Con Poppler y manteniendo el diseño:

```
$ pdftotext -layout in.pdf out.txt

```

Véase también [pdftotext(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pdftotext.1).

### Descifrar un PDF

Esta sección enumera los comandos para descifrar un PDF en un archivo sin cifrar. Tenga en cuenta que la mayoría de [visores PDF](#Visores) también soportan archivos PDF cifrados.

Con PDFtk:

```
$ pdftk in.pdf input_pw *contraseña* output out.pdf

```

Con Poppler a PostScript:

```
$ pdftops -upw *contraseña* in.pdf out.ps

```

Con QPDF:

```
$ qpdf --decrypt --password=*contraseña* in.pdf out.pdf

```

**Sugerencia:** Las contraseñas olvidadas pueden recuperarse con [pdfcrack](https://www.archlinux.org/packages/?name=pdfcrack), véase [pdfcrack(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pdfcrack.1).

### Cifrar un PDF

La *contraseña_de_usuario* se utiliza para el cifrado, la *contraseña_de_propietario* para restringir las operaciones una vez que se descifra el documento, para más información, véase [Wikipedia:PDF#Security and signatures](https://en.wikipedia.org/wiki/PDF#Security_and_signatures "wikipedia:PDF").

Con PDFtk:

```
$ pdftk in.pdf output out.pdf user_pw *contraseña*

```

Con [PoDoFo](#Bibliotecas):

```
$ podofoencrypt -u *contraseña_de_usuario* -o *contraseña_de_propietario* in.pdf out.pdf

```

Con QPDF:

```
$ qpdf --encrypt *contraseña_de_usuario* *contraseña_de_propietario* *longitud_de_la_clave* -- in.pdf out.pdf

```

donde `*longitud_de_la_clave*` puede ser 40, 128 ó 256.

### Extraer imágenes de un PDF

Con Poppler a JPEG:

```
$ pdfimages *entrada*.pdf -j *prefijo_salida*

```

### Extraer un rango de página del PDF, dividir el documento PDF de varias páginas

Con Ghostscript como un solo archivo[[6]](https://forums.freebsd.org/threads/split-pdf-file.58902/#post-336971)

```
$ gs -sDEVICE=pdfwrite -dNOPAUSE -dBATCH -dSAFER -dFirstPage=*primero* -dLastPage=*último* -sOutputFile=*salida*.pdf *entrada*.pdf

```

Con PDFtk como un solo archivo:

```
$ pdftk *entrada*.pdf cat *primero*-*último* output *salida*.pdf

```

Con Poppler como archivos separados:

```
$ pdfseparate -f *primero* -l *último* *entrada*.pdf *prefijo_salida*-%d.pdf

```

Con QPDF como un solo archivo:

```
$ qpdf --empty --pages *entrada*.pdf *primero*-*último* -- *salida*.pdf

```

### Imponiendo un PDF

La [imposición](https://en.wikipedia.org/wiki/es:Imposici%C3%B3n "wikipedia:es:Imposición") PDF puede hacerse con [pdfjam](#Herramientas_PDF), por ejemplo, el desperdicio de papel se puede reducir con *pdfnup* y *pdfbook* se puede utilizar para organizar archivos PDF en un formato adecuado para encuadernación de libros.

### Inspeccionar metadatos

Con [ExifTool](/index.php/ExifTool "ExifTool"):

```
$ exiftool archivo.pdf

```

Con Poppler:

```
$ pdfinfo archivo.pdf

```

### Optimizar, reducir el tamaño de un PDF

Con Ghostscript uno de:

```
$ ps2pdf -dPDFSETTINGS=/screen in.pdf out.pdf
$ gs -dNOPAUSE -dBATCH -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/printer -sOutputFile=out.pdf in.pdf

```

Para distintas configuraciones véase la [documentación](https://www.ghostscript.com/doc/9.22/VectorDevices.htm#PSPDF_IN).

También está [shrinkpdf](https://aur.archlinux.org/packages/shrinkpdf/), un script que envuelve gs.

### Rasterizar un PDF

Con [GraphicsMagick](/index.php/GraphicsMagick_(Espa%C3%B1ol) "GraphicsMagick (Español)") para convertir una página específica:

```
$ gm convert -density *dpi* *entrada*.pdf[*página*] *salida*.jpg

```

Con Poppler para convertir todas las páginas:

```
$ pdftoppm -jpeg -r *dpi* *entrada*.pdf *prefijo_salida*

```

Con Poppler para convertir una página específica:

```
$ pdftoppm -jpeg -r *dpi* -f *página* -singlefile *entrada*.pdf *prefijo_salida*

```

### División de páginas PDF

Con mupdf-tools para dividir cada página verticalmente en dos páginas:

```
$ mutool poster -y 2 in.pdf out.pdf

```

Se puede utilizar para deshacer [imposiciones](#Imponiendo_un_PDF) simples.

### Añadir firma.png o imagen a una de las páginas del PDF

Para añadir una imagen en cualquier ubicación en un PDF se puede hacer con imagemagick (convertir), xv, y pdftk. Un script está [aquí](http://emmanuel.branlard.free.fr/work/linux/dev/SignPDF/SignPDF) y otros consejos están [aquí](https://unix.stackexchange.com/questions/85873/how-can-i-add-a-signature-png-to-a-pdf-in-linux).

## Herramientas DjVu

*   [DjVuLibre](#Motores) proporciona muchas herramientas de línea de órdenes, como por ejemplo [ddjvu(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ddjvu.1).
*   **img2djvu** — Codificador DjVu de una sola pasada basado en DjVu Libre e ImageMagick.

	[https://github.com/ashipunov/img2djvu](https://github.com/ashipunov/img2djvu) || [img2djvu-git](https://aur.archlinux.org/packages/img2djvu-git/)

*   **pdf2djvu** — Crea archivos DjVu a partir de archivos PDF.

	[https://jwilk.net/software/pdf2djvu](https://jwilk.net/software/pdf2djvu) || [pdf2djvu](https://www.archlinux.org/packages/?name=pdf2djvu)

### Convertir DjVu a imágenes

Divide Djvu en páginas separadas:

```
$ djvmcvt -i input.djvu /ruta/al/directorio/de/salida output-index.djvu

```

Convierte páginas Djvu en imágenes:

```
$ ddjvu --format=tiff page.djvu page.tiff

```

Convierte páginas Djvu en PDF:

```
$ ddjvu --format=pdf inputfile.djvu ouputfile.pdf

```

También puedes utilizar *--page* para exportar páginas específicas:

```
$ ddjvu --format=tiff --page=1-10 input.djvu output.tiff

```

esto convertirá las páginas de 1 a 10 en un archivo tiff.

### Procesando imágenes

Puedes utilizar [scantailor](https://www.archlinux.org/packages/?name=scantailor) para:

*   corregir la orientación
*   dividir páginas
*   enderezar
*   recortar
*   ajustar márgenes

### Crear DjVu desde imágenes

Hay un script útil en [img2djvu-git](https://aur.archlinux.org/packages/img2djvu-git/).

```
$ img2djvu -c1 -d600 -v1 ./salida

```

esto creará `out.djvu` con 600 DPI de todos los archivos en en directorio `./salida`.

Alternativamente, puede probar [didjvu](https://aur.archlinux.org/packages/didjvu/), que parece crear archivos más pequeños especialmente en imágenes con fondo bien definido.

## Herramientas PostScript

*   **pstotext** — Convierte archivos PostScript a texto.

	[http://www.cs.wisc.edu/~ghost/doc/pstotext.htm](http://www.cs.wisc.edu/~ghost/doc/pstotext.htm) || [pstotext](https://www.archlinux.org/packages/?name=pstotext)

*   [Ghostscript](#Motores)

### ps2pdf

*ps2pdf* es una envoltura alrededor de ghostscript para convertir PostScript a PDF:

```
$ ps2pdf -sPAPERSIZE=a4 -dOptimize=true -dEmbedAllFonts=true YourPSFile.ps

```

Explicación:

*   `-sPAPERSIZE=something` define el tamaño del papel. Para valores válidos de PAPERSIZE, véase [[7]](http://ghostscript.com/doc/current/Use.htm#Known_paper_sizes).
*   `-dOptimize=true` permite que el PDF creado se optimice para la carga.
*   `-dEmbedAllFonts=true` hace que las fuentes se vean siempre bonitas.

**Nota:** No puede elegir la orientación del papel en ps2pdf. Si su archivo PS de entrada está en buen estado, ya contiene la información de orientación. Si está intentando utilizar un archivo PS encapsulado, tendrá problemas si no cabe en el `-sPAPERSIZE` especificado, porque los archivos EPS generalmente no contienen información de orientación del papel. Una solución es crear un nuevo documento en la configuración de ghostscript (llámelo p.e. "slide") y utilícelo como `-sPAPERSIZE=slide`.

## Bibliotecas

*   **libharu** — Biblioteca C para generar documentos PDF.

	[https://github.com/libharu/libharu](https://github.com/libharu/libharu) || [libharu](https://www.archlinux.org/packages/?name=libharu), Lua binding: [lua-hpdf](https://aur.archlinux.org/packages/lua-hpdf/)

*   **PoDoFo** — Una biblioteca de C++ para trabajar con el formato de archivo PDF.

	[http://podofo.sourceforge.net](http://podofo.sourceforge.net) || [podofo](https://www.archlinux.org/packages/?name=podofo)

### Python

*   **PDFMiner** — Utilidades para extraer, analizar datos de texto de archivos PDF. Incluye pdf2txt, dumppdf, y latin2ascii

	[http://www.unixuser.org/~euske/python/pdfminer/](http://www.unixuser.org/~euske/python/pdfminer/) || [pdfminer](https://aur.archlinux.org/packages/pdfminer/), [python-pdfminer.six](https://aur.archlinux.org/packages/python-pdfminer.six/)

*   **pdfrw** — Una biblioteca puramente Python que lee y escribe archivos PDF.

	[https://github.com/pmaupin/pdfrw](https://github.com/pmaupin/pdfrw) || [python-pdfrw](https://www.archlinux.org/packages/?name=python-pdfrw), [python2-pdfrw](https://aur.archlinux.org/packages/python2-pdfrw/)

*   **PyPDF2** — Una biblioteca puramente Python construida como un toolkit PDF.

	[https://mstamy2.github.com/PyPDF2](https://mstamy2.github.com/PyPDF2) || [python-pypdf2](https://aur.archlinux.org/packages/python-pypdf2/), [python2-pypdf2](https://aur.archlinux.org/packages/python2-pypdf2/)

*   **PyX** — Biblioteca de Python para la creación de archivos PostScript y PDF.

	[http://pyx.sourceforge.net](http://pyx.sourceforge.net) || [python-pyx](https://www.archlinux.org/packages/?name=python-pyx), [python2-pyx](https://www.archlinux.org/packages/?name=python2-pyx)

*   **ReportLab** — Una solución comprobada de generación de PDF.

	[https://bitbucket.org/rptlab/reportlab](https://bitbucket.org/rptlab/reportlab) || [python-reportlab](https://www.archlinux.org/packages/?name=python-reportlab), [python2-reportlab](https://aur.archlinux.org/packages/python2-reportlab/)

## Véase también

*   [List of applications/Documents#Readers and viewers](/index.php/List_of_applications/Documents#Readers_and_viewers "List of applications/Documents")
*   [List of applications/Documents#OCR software](/index.php/List_of_applications/Documents#OCR_software "List of applications/Documents")
*   [Wikipedia:List of PDF software](https://en.wikipedia.org/wiki/List_of_PDF_software "wikipedia:List of PDF software")