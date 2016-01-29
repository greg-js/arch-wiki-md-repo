# Djvu

From [Wikipedia's DjVu Page](http://en.wikipedia.org/wiki/DjVu):

NaN

NaN

NaN

## Contents

*   [1 How It Works](#How_It_Works)
*   [2 Installation](#Installation)
*   [3 DjVu Manipulations](#DjVu_Manipulations)
    *   [3.1 Convert DjVu to images](#Convert_DjVu_to_images)
    *   [3.2 Processing Images](#Processing_Images)
    *   [3.3 Make DjVu from Images](#Make_DjVu_from_Images)

## How It Works

From [MobileRead Wiki's DjVU Page](http://wiki.mobileread.com/wiki/DJVU)

NaN

```
   Foreground layer includes text, line art and other thin, low-color elements.
   Background layer includes photos, graphics, tint, and paper texture. Areas of the background that are covered by the foreground are smoothly interpolated to minimize coding costs. Lower resolution is used on this layer. 

```

NaN

NaN

NaN

NaN

NaN

NaN

## Installation

There are several packages that can be installed to enable use of the DjVu format.

*   [djvulibre](https://www.archlinux.org/packages/?name=djvulibre) a suite to create, manipulate and view DjVu documents.
*   [pdf2djvu](https://www.archlinux.org/packages/?name=pdf2djvu) a tool used to create DjVu files from PDF files.
*   [djview](https://www.archlinux.org/packages/?name=djview) a portable DjVu viewer and browser plugin.

Read each tool's man to find additional information.

## DjVu Manipulations

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

You can also use _--page_ to export specific pages:

```
 ddjvu --format=tiff --page=1-10 input.djvu output.tiff

```

this will convert pages from 1 to 10 into one tiff file.

### Processing Images

You can use [scantailor](https://www.archlinux.org/packages/?name=scantailor) to:

*   fix orientation
*   split pages
*   deskew
*   crop
*   adjust margins

### Make DjVu from Images

There is a useful script [img2djvu-git](https://aur.archlinux.org/packages/img2djvu-git/)<sup><small>AUR</small></sup>.

```
 img2djvu -c1 -d600 -v1 ./out

```

it will create 600dpi out.djvu from all files in ./out directory.

Alternatively, you can try [didjvu](http://jwilk.net/software/didjvu), which seems to create smaller files especially on images with well defined background.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Djvu&oldid=410527](https://wiki.archlinux.org/index.php?title=Djvu&oldid=410527)"