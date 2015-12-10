# Digikam

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:Digikam#](https://wiki.archlinux.org/index.php/Talk:Digikam))

[Digikam](https://en.wikipedia.org/wiki/Digikam "wikipedia:Digikam") is a KDE-based image organizer with built-in editing features via a plugin architecture.

## Contents

*   [1 Installation](#Installation)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Video playback](#Video_playback)
    *   [2.2 Unreadable tool tips](#Unreadable_tool_tips)

## Installation

[Install](/index.php/Install "Install") [digikam](https://www.archlinux.org/packages/?name=digikam). Optionally, install [kdemultimedia-mplayerthumbs](https://www.archlinux.org/packages/?name=kdemultimedia-mplayerthumbs) to generate thumbnails for video files.

## Troubleshooting

### Video playback

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [KDE#Phonon](/index.php/KDE#Phonon "KDE").**

**Notes:** Not specific to digikam, see also [Help:Style#Official packages](/index.php/Help:Style#Official_packages "Help:Style") (Discuss in [Talk:Digikam#](https://wiki.archlinux.org/index.php/Talk:Digikam))

A [Phonon backend](/index.php/KDE#Phonon "KDE") is installed as a dependency of Digikam, but matching multimedia codecs may be missing. When using the [phonon-qt4-gstreamer](https://www.archlinux.org/packages/?name=phonon-qt4-gstreamer) backend, install one or more of its plugins with `pacman -S gstreamer0.10-{good,bad,ugly,ffmpeg}` .

### Unreadable tool tips

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Uniform_Look_for_Qt_and_GTK_Applications](/index.php/Uniform_Look_for_Qt_and_GTK_Applications "Uniform Look for Qt and GTK Applications").**

**Notes:** This is a general issue with Qt applications (Discuss in [Talk:Digikam#](https://wiki.archlinux.org/index.php/Talk:Digikam))

If tooltips within the user interface are either blank (empty rectangles), or unreadable due to a poor foreground and background combination, choose a different widget style:

1.  Navigate to _Settings_ > _Configure digiKam_ > _Miscellaneous_
2.  Now in _Widget Style_, choose _"Cleanlooks"_

This will have a simple, readable white text on black background in the tool tip.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Digikam&oldid=394157](https://wiki.archlinux.org/index.php?title=Digikam&oldid=394157)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Image manipulation](/index.php/Category:Image_manipulation "Category:Image manipulation")