# YAGF

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [List of applications#OCR software](/index.php/List_of_applications#OCR_software "List of applications")

[YAGF](http://sourceforge.net/projects/yagf-ocr/) is a graphical interface for the [cuneiform](https://en.wikipedia.org/wiki/CuneiForm_(software) "wikipedia:CuneiForm (software)") OCR program on the Linux platform. With YAGF you can scan images via XSane, perform images preprocessing and recognize texts using cuneiform from a single command centre. YAGF also makes it easy to scan and recognize several images sequentially.

## Contents

*   [1 Installation](#Installation)
*   [2 Supported languages](#Supported_languages)
*   [3 Usage](#Usage)
    *   [3.1 Images acquisition](#Images_acquisition)
    *   [3.2 Images preprocessing](#Images_preprocessing)
    *   [3.3 The text recognition](#The_text_recognition)
*   [4 See also](#See_also)

## Installation

YAGF requires Qt 4 and the [aspell](https://www.archlinux.org/packages/?name=aspell) spellchecking package. If you want to acquire images from a scanner into YAGF directly, you should install [XSane](/index.php/SANE "SANE") software. And of course you will need cuneiform for the text recognition.

[Install](/index.php/Install "Install") [yagf](https://www.archlinux.org/packages/?name=yagf) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Supported languages

Next languages are available for recognition: Czech,Danish, Dutch, English, Estonian, French, German, Hungarian, Italian, Latvian, Lithuanian, Polish, Portuguese, Romanian, Russian Spanish, Swedish, Ukrainian

## Usage

Digitizing text with YAGF consists of several stages: images acquisition, images preprocessing (if necessary), the recognition itself, and saving the results.

### Images acquisition

You can recognize text from the images stored on your hard drive, or you can scan new images and pass them to YAGF directly. Use File/Open Image... command to load an image from your hard drive. YAGF supports all major raster graphics formats (JPEG, PNG, BMP, TIFF, GIF, PNM, PPM, PBM). If the loaded file's name is in the form _nameXXX.ext_, where _XXX_ is some number, you can move between previous/next file in the series with the navigation buttons. For example, if you have loaded the file named _MyPage06.jpg_, the "Move to next image" button will try to open the file _MyPage07.jpg_. All the opened images will be displayed on the image bar.

You can acquire images direct;y from a scanner using XSane. While in YAGF, choose File/Scan command. XSane program will be started. Set up the scanning options with XSane and press XSane's _Scan_ button. When the scanning is done the scanned image is opened in the YAGF image viewing window. If you want to scan several pages, you can repeat these operation several times. Each time the last scanned image will be shown in the YAGF image viewing window. You can move to previous images using navigation buttons. You can keep XSane window open while working with YAGF. When you exit YAGF this window will be closed automatically. In order to navigate between scanned images use navigation buttons as it was described above. All acquired images are shown as thumbnails on the image bar on the left. You can save these images into a separate directory using Save button on the image bar.

### Images preprocessing

There are several preprocessing options available in YAGF. You can rotate loaded images if they are not positioned correctly. Images may be rotated by 90 degrees (counter-) clockwise and by 180 degrees. There are special buttons for this at the top of the image-viewing window. If you do not want to recognize an entire page but rather some part of it, you can select a rectangular block for recognition. The block is selected in the image-viewing window with mouse. The block is resizable, you can resize it by dragging mouse pointer on its edge. While usually the scanned page doesn't fit into the image-viewing window, you can scale an image up or down to make the selection process more convenient. This operation does not change the resolution of the image passed to cuneiform for recognition. You can also scale images using `Ctrl++` and `Ctrl+-` keys combinations or with the mouse wheel while holding `Ctrl` key down. You can change the font size in the text editor window the same way.

### The text recognition

Before recognizing text you should select the recognition language (or a language paire if the document to be recognized is written in several languages).

Each newly recognized text fragment is added to the recognized text editor window at the end of the already recognized text as a new paragraph.

By default YAGF checks spelling in recognized texts using libaspell. Usually aspell is installed in your system with dictionaries for your system's local language and English. If you want to use spell-checking for the texts in other languages, you have to install additional aspell dictionaries (usually available in your system's software repository). You will be warned each time when YAGF cannot find a dictionary for the selected recognition language. Turn spell-checking off if you do not want to see these warnings.

If you have several images opened in your Image bar, you can use batch recognition to recognize text from all the images in a sequence. Click "Recognize All Pages" button. The images will be automatically loaded and recognized one after another and the progress dialog will appear. You can stop the recognition process by clicking the progress dialog's _Abort_ button. Saving the Results

The recognized text may be saved to disc as a text or html file in UTF-8 encoding or copied to the clipboard. The "Copy to Clipboard" btton copies either a selected text fragment or the whole text if no fragment is selected.

## See also

*   [List of applications#OCR software](/index.php/List_of_applications#OCR_software "List of applications")
*   [http://symmetrica.net/cuneiform-linux/yagf-en.html](http://symmetrica.net/cuneiform-linux/yagf-en.html) - YAGF home page
*   [https://launchpad.net/cuneiform-linux](https://launchpad.net/cuneiform-linux) - Linux port of Cuneiform

Retrieved from "[https://wiki.archlinux.org/index.php?title=YAGF&oldid=413954](https://wiki.archlinux.org/index.php?title=YAGF&oldid=413954)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Office](/index.php/Category:Office "Category:Office")