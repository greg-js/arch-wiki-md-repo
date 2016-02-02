# JDownloader

JDownloader is a Download Manager written in Java. JDownloader can download normal files, but also files from online file hosting services like Rapidshare.com.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Running](#Running)
*   [2 Configuration](#Configuration)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Making JDownloader faster](#Making_JDownloader_faster)
*   [4 Alternatives](#Alternatives)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Application not resizing with WM, menus immediately closing](#Application_not_resizing_with_WM.2C_menus_immediately_closing)

## Installation

Install [jdownloader2](https://aur.archlinux.org/packages/jdownloader2/) from the [AUR](/index.php/AUR "AUR").

For running JDownloader you need Java installed. OpenJDK is recommended, it works flawlessly with jDownloader.

### Running

Use the command jdownloader to start JDownloader. When you just installed JDownloader from AUR, this will run the update tool to download some required files for JDownloader, else this will start JDownloader directly.

## Configuration

When you first start JDownloader you can choose your preferred language and also your download directory. On the next window, JDownloader asks you if you want to install FlashGot, a Firefox extension. I recommend clicking on Cancel. If you want this extension, you can still download it through [the official mozilla addons website](http://addons.mozilla.org).

If you enable the Light(GTK) theme and the fonts appear to lack anti-aliasing, modify `~/.bashrc` as appropriate following the directions [here](https://wiki.archlinux.org/index.php/Java_Fonts_-_Sun_JRE#Anti-aliasing).

## Tips and tricks

### Making JDownloader faster

In its default configuration, JDownloader is very slow and uses a lot of resources. You can atleast make it a bit faster by applying the following changes in the Settings Tab.

Choose General and then turn the logging level to OFF.

Choose User Interface and then switch the style to Light(GTK). (If you're using GNOME).

## Alternatives

[Tucan Manager](http://tucaneando.com/index.html) available in the AUR through the [tucan](https://aur.archlinux.org/packages/tucan/) package.

[uGet](http://ugetdm.com/) available in the [official repositories](/index.php/Official_repositories "Official repositories") through the [uget](https://www.archlinux.org/packages/?name=uget) package (GTK).

[pyLoad](/index.php/PyLoad "PyLoad") available in AUR: [pyload](https://aur.archlinux.org/packages/pyload/).

[plowshare](https://github.com/mcrapet/plowshare) available in AUR: [plowshare-git](https://aur.archlinux.org/packages/plowshare-git/) (CLI).

[FreeRapid Downloader](http://wordrider.net/freerapid/) available in AUR: [freerapid](https://aur.archlinux.org/packages/freerapid/) (Java).

## Troubleshooting

### Application not resizing with WM, menus immediately closing

see [Java#Applications not resizing with WM, menus immediately closing](/index.php/Java#Applications_not_resizing_with_WM.2C_menus_immediately_closing "Java")

Retrieved from "[https://wiki.archlinux.org/index.php?title=JDownloader&oldid=414048](https://wiki.archlinux.org/index.php?title=JDownloader&oldid=414048)"