This article is meant to guide (Arch)linux users to use PDF forms. Some of the information here is from [this](https://bbs.archlinux.org/viewtopic.php?id=52084) thread.

## Contents

*   [1 Usage](#Usage)
    *   [1.1 Cabaret Stage](#Cabaret_Stage)
    *   [1.2 flpsed](#flpsed)
    *   [1.3 Inkscape](#Inkscape)

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