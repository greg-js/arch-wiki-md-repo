This article is meant to guide (Arch)linux users to use PDF forms. Some of the information here is from [this](https://bbs.archlinux.org/viewtopic.php?id=52084) thread.

## Contents

*   [1 Usage](#Usage)
    *   [1.1 Cabaret Stage](#Cabaret_Stage)
    *   [1.2 flpsed](#flpsed)
    *   [1.3 Inkscape](#Inkscape)
    *   [1.4 Master PDF Editor](#Master_PDF_Editor)
    *   [1.5 Adobe Reader is unstable](#Adobe_Reader_is_unstable)

## Usage

### Cabaret Stage

[Cabaret Stage](https://www.cabaret-solutions.com/pdf-produkte/cabaret-stage) claims to be able to read, fill, and save PDF forms.

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

Version build 3.7.10 could open and fill in forms for Swedish Tax Authority (requiring Adobe Reader 8 or higher) and also save and print the files.

Changes are preserved on saved files and can be modified again in Master PDF Editor. However, when opening the saved file with Evince, one would get a blank page, so corruption of the original file is likely (but this was not tested). The simple and safe workaround is to print to PDF and send the "flat" PDF file if one needs sending across a file.

The package can be [installed](/index.php/Install "Install") with [masterpdfeditor](https://aur.archlinux.org/packages/masterpdfeditor/) and gives the executable pdfeditor.

### Adobe Reader is unstable

Adobe Reader (version 9.5.5-6) is not a viable alternative, as doesn't seem to work on my system.

It starts up, loads the file, spends some 30 seconds fully functional and then crashes without an error message. Not enough time to manage to test any of the forms functions.

As part of weird behaviour, the acceptance of licence message only shows up if Reader is run as root.

The package can be [installed](/index.php/Install "Install") with [acroread](https://aur.archlinux.org/packages/acroread/).