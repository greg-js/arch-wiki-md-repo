JDownloader is a Download Manager written in Java. JDownloader can download normal files, but also files from online file hosting services like Rapidshare.com.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Running](#Running)
*   [2 Configuration](#Configuration)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Making JDownloader faster](#Making_JDownloader_faster)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Application not resizing with WM, menus immediately closing](#Application_not_resizing_with_WM.2C_menus_immediately_closing)
*   [5 See also](#See_also)

## Installation

Install [jdownloader2](https://aur.archlinux.org/packages/jdownloader2/) from the [AUR](/index.php/AUR "AUR").

For running JDownloader you need [Java](/index.php/Java "Java") installed. OpenJDK is recommended, it works flawlessly with jDownloader.

### Running

Use the command jdownloader to start JDownloader. When you just installed JDownloader from AUR, this will run the update tool to download some required files for JDownloader, else this will start JDownloader directly.

## Configuration

When you first start JDownloader you can choose your preferred language and also your download directory. On the next window, JDownloader asks you if you want to install FlashGot, a Firefox extension. I recommend clicking on Cancel. If you want this extension, you can still download it through [the official mozilla addons website](http://addons.mozilla.org).

If you enable the Light(GTK) theme and the fonts appear to lack anti-aliasing, modify `~/.bashrc` as appropriate following the directions [here](/index.php/Java_Fonts_-_Sun_JRE#Anti-aliasing "Java Fonts - Sun JRE").

## Tips and tricks

### Making JDownloader faster

In its default configuration, JDownloader is very slow and uses a lot of resources. You can atleast make it a bit faster by applying the following changes in the Settings Tab.

Choose General and then turn the logging level to OFF.

Choose User Interface and then switch the style to Light(GTK). (If you're using GNOME).

## Troubleshooting

### Application not resizing with WM, menus immediately closing

see [Java#Applications not resizing with WM, menus immediately closing](/index.php/Java#Applications_not_resizing_with_WM.2C_menus_immediately_closing "Java")

## See also

[List of applications/Internet#Web content downloaders](/index.php/List_of_applications/Internet#Web_content_downloaders "List of applications/Internet")