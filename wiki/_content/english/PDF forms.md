This article is meant to guide (Arch)linux users to use PDF forms. Some of the information here is from [this](https://bbs.archlinux.org/viewtopic.php?id=52084) thread.

## Contents

*   [1 Reading and filling PDF forms](#Reading_and_filling_PDF_forms)
    *   [1.1 Cabaret Stage](#Cabaret_Stage)
    *   [1.2 flpsed](#flpsed)
    *   [1.3 Inkscape](#Inkscape)

## Reading and filling PDF forms

### Cabaret Stage

[Cabaret Stage](https://www.cabaret-solutions.com/download-area) claims to be able to read, fill, and save PDF forms.

### flpsed

Quoting flpsed’s author: “**[flpsed](http://www.ecademix.com/JohannesHofmann/flpsed.html)** is a WYSIWYG PostScript annotator. You can’t remove or modify existing elements of a document. But flpsed lets you add arbitrary text lines to existing PostScript documents [...]. Added lines can later be re-edited with flpsed. [...] flpsed is useful for filling in forms, adding notes etc.”

And quoting the aforementioned [thread](https://bbs.archlinux.org/viewtopic.php?pid=556501#p556501): “flpsed, in the AUR, will place text on top of a plain pdf (without the special form fields). (Note: it took me a while to figure out how to move or edit text that has already been placed, but all you have to do is click on the first letter in the field. If you click on the middle of the field, nothing will happen)”

[flpsed](https://aur.archlinux.org/packages/flpsed/) is available from the [AUR](/index.php/AUR "AUR").

### Inkscape

[Inkscape](http://www.inkscape.org/) is an image editing program that can be used to fill PDF forms by importing the PDF file and simply inserting text fields where you want them to be. Its not really filling the form (the fields will probably still be blank if the forms are to be read electronically), but should work well enough if you intend to print them.