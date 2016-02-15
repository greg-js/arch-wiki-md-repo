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

A [Phonon backend](/index.php/KDE#Phonon "KDE") is installed as a dependency of Digikam, but matching multimedia codecs may be missing. When using the [phonon-qt4-gstreamer](https://www.archlinux.org/packages/?name=phonon-qt4-gstreamer) backend, install one or more of its plugins with `pacman -S gstreamer0.10-{good,bad,ugly,ffmpeg}` .

### Unreadable tool tips

If tooltips within the user interface are either blank (empty rectangles), or unreadable due to a poor foreground and background combination, choose a different widget style:

1.  Navigate to _Settings_ > _Configure digiKam_ > _Miscellaneous_
2.  Now in _Widget Style_, choose _"Cleanlooks"_

This will have a simple, readable white text on black background in the tool tip.