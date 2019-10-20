[JDownloader](http://jdownloader.org/) is a download manager written in [Java](/index.php/Java "Java"). JDownloader can download normal files, but also files from online file hosting services like MEGA.nz.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Running](#Running)
*   [2 Configuration](#Configuration)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Downloading files without creating a subdirectory](#Downloading_files_without_creating_a_subdirectory)
    *   [3.2 Changing preferences for individual sites](#Changing_preferences_for_individual_sites)
    *   [3.3 Changing font scale](#Changing_font_scale)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Application not resizing with WM, menus immediately closing](#Application_not_resizing_with_WM,_menus_immediately_closing)
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

### Downloading files without creating a subdirectory

By default jdownloader will create a subdirectory for each file you download in your destination folder. To stop this behaviour go to Settings > Packagiser and untick the predefined rules as desired.

### Changing preferences for individual sites

Preferences for individual sites can be found by going to Settings > Plugins. For example, by changing settings on the youtube.com plugin you could tell jdownloader to only download the audio from youtube links.

### Changing font scale

If font is too small, it can be enlarged by increasing scale factor: *settings > advanced settings > LAFSettings.fontscalefactor* [jd forum](https://board.jdownloader.org/showthread.php?t=73752).

## Troubleshooting

### Application not resizing with WM, menus immediately closing

see [Java#Gray window, applications not resizing with WM, menus immediately closing](/index.php/Java#Gray_window,_applications_not_resizing_with_WM,_menus_immediately_closing "Java")

## See also

[List of applications/Internet#Download managers](/index.php/List_of_applications/Internet#Download_managers "List of applications/Internet").