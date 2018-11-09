Related articles

*   [List of applications#PDF and DjVu](/index.php/List_of_applications#PDF_and_DjVu "List of applications")

This article is meant to guide (Arch)linux users to use PDF forms. Some of the information here is from [this](https://bbs.archlinux.org/viewtopic.php?id=52084) thread.

## Contents

*   [1 Usage](#Usage)
    *   [1.1 Evince](#Evince)
    *   [1.2 flpsed](#flpsed)
    *   [1.3 Inkscape](#Inkscape)
    *   [1.4 Master PDF Editor](#Master_PDF_Editor)
    *   [1.5 LibreOffice Draw](#LibreOffice_Draw)
    *   [1.6 PDF Studio](#PDF_Studio)
    *   [1.7 Adobe Reader is unstable](#Adobe_Reader_is_unstable)

## Usage

### Evince

**[Evince](https://en.wikipedia.org/wiki/Evince "wikipedia:Evince")** — Document viewer for multiple document formats. Supports PDF, PostScript, DjVu, TIFF and DVI.

	[https://wiki.gnome.org/Apps/Evince](https://wiki.gnome.org/Apps/Evince) || [evince](https://www.archlinux.org/packages/?name=evince)

Easy to use GUI

### flpsed

According to flpsed’s author:

	[flpsed](http://flpsed.org/flpsed.html) is a WYSIWYG PostScript annotator. You can’t remove or modify existing elements of a document. But flpsed lets you add arbitrary text lines to existing PostScript documents [...]. Added lines can later be re-edited with flpsed. [...] flpsed is useful for filling in forms, adding notes etc.

From a [forum thread](https://bbs.archlinux.org/viewtopic.php?pid=556501#p556501):

	flpsed, in the AUR, will place text on top of a plain pdf (without the special form fields).

The package can be [installed](/index.php/Install "Install") with [flpsed](https://aur.archlinux.org/packages/flpsed/).

### Inkscape

[Inkscape](http://www.inkscape.org/) is an image editing program that can be used to fill PDF forms, by importing the PDF file and inserting text fields at the correct location. The fields are likely blank when the forms are read electronically, but it should work well enough for printing.

See [inkscape](/index.php/Inkscape "Inkscape") for more info.

### Master PDF Editor

[Master PDF Editor](https://code-industry.net/) is a PDF editing program that is able to read properly PDF files that "require Adobe Reader 8 or higher" (this is the message that Evince would display when trying to open such files). It is free for non-commercial use.

Version 4.x can open, fill, save and submit PDF forms. In effect it provides the same PDF form functionality as the free version of Adobe Reader on Windows and additionally it can be used to create PDF forms and form elements. Some other PDF features are however disabled in the free version, see its [functionality comparison table](https://code-industry.net/free-pdf-editor/).

Changes are preserved on saved files and can be modified again in Master PDF Editor. However, when opening the saved file with Evince 3.2x, due to bugs in Evince one would get blank parts instead of form elements created or edited with Master PDF. Okular 1.1 shows the form elements correctly but has other general bugs in filling/using form elements.

Note that it cannot properly handle select boxes yet in forms.

The package can be [installed](/index.php/Install "Install") with [masterpdfeditor](https://aur.archlinux.org/packages/masterpdfeditor/).

**Note:** Version 5.x of Master PDF Editor has restricted capabilities on document editing and leaves watermarks when saving documents. To install older 4.x version use [masterpdfeditor-qt4](https://aur.archlinux.org/packages/masterpdfeditor-qt4/) package instead.

### LibreOffice Draw

LibreOffice Draw can open and edit PDF files in much the same manner that Inkscape can. One can then re-export the edited PDF to a new file.

### PDF Studio

[PDF Studio](https://en.wikipedia.org/wiki/PDF_Studio "wikipedia:PDF Studio") is a proprietary, easy to use PDF editor that maintains full compatibility with the PDF Standard.

You can [install](/index.php/Install "Install") it with [pdfstudio](https://aur.archlinux.org/packages/pdfstudio/).

[PDF Studio Viewer](https://www.qoppa.com/pdfstudioviewer/) is a cross-platform PDF reader that is reliable and easy to use. PDF Studio Viewer can annotate PDF documents and fill interactive forms. For more editing features, Qoppa Software publishes PDF Studio Standard and Pro editions.

### Adobe Reader is unstable

Adobe Reader (version 9.5.5-6) is not a viable alternative, as does not seem to work on my system.

It starts up, loads the file, spends some 30 seconds fully functional and then crashes without an error message. Not enough time to manage to test any of the forms functions.

As part of weird behaviour, the acceptance of licence message only shows up if Reader is run as root.

The package can be [installed](/index.php/Install "Install") with [acroread](https://aur.archlinux.org/packages/acroread/).