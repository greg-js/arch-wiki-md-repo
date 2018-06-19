Related articles

*   [GIMP/CMYK support](/index.php/GIMP/CMYK_support "GIMP/CMYK support")

[GIMP](https://www.gimp.org/) is one of many in the [List of applications/Multimedia#Raster graphics editors](/index.php/List_of_applications/Multimedia#Raster_graphics_editors "List of applications/Multimedia").

## Contents

*   [1 Installation](#Installation)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 GIMP PDF editing doesn't work](#GIMP_PDF_editing_doesn.27t_work)
    *   [2.2 Green text](#Green_text)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [gimp](https://www.archlinux.org/packages/?name=gimp) package.

**Tip:** The GIMP implements a plug-in system and the repositories ([official](https://www.archlinux.org/packages/?sort=&q=gimp&maintainer=&flagged=), [AUR](https://aur.archlinux.org/packages/?O=0&SeB=nd&K=gimp&outdated=off&SB=n&SO=a&PP=50&do_Search=Go)) contain more plug-ins than listed in the package's optional depends.

## Troubleshooting

### GIMP PDF editing doesn't work

GIMP requires the [poppler-glib](https://www.archlinux.org/packages/?name=poppler-glib) library for editing PDF files. Without this library GIMP will say that a PDF file is "unrecognized" when an attempt to open a PDF is made.

### Green text

Add the following to `~/.gimp-2.8/fonts.conf` if you see green tint around letters with antialiasing enabled:

```
 <?xml version='1.0'?>
 <!DOCTYPE fontconfig SYSTEM 'fonts.dtd'>
 <fontconfig>
   <match target="font">
     <edit name="rgba" mode="assign">
       <const>none</const>
     </edit>
   </match>
 </fontconfig>

```

## See also

*   [Wikipedia:GIMP](https://en.wikipedia.org/wiki/GIMP "wikipedia:GIMP")
*   [debian:GIMP](https://wiki.debian.org/GIMP "debian:GIMP")
*   [Resources | GIMP Magazine](https://gimpmagazine.org/resources/) - Index of GIMP resources, tutorials, communities