[Digikam](https://en.wikipedia.org/wiki/Digikam "wikipedia:Digikam") is a KDE-based image organizer with built-in editing features via a plugin architecture.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Gnome Installations](#Gnome_Installations)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Unreadable tool tips](#Unreadable_tool_tips)

## Installation

[Install](/index.php/Install "Install") [digikam](https://www.archlinux.org/packages/?name=digikam).

### Gnome Installations

Additionally, in order to allow icons to work (no missing icons) correctly for gnome desktop environment you must install the KDE icons and theme as below with the qt5 settings program.

[Install](/index.php/Install "Install") [oxygen](https://www.archlinux.org/packages/?name=oxygen) [oxygen-icons](https://www.archlinux.org/packages/?name=oxygen-icons) [qt5ct](https://www.archlinux.org/packages/?name=qt5ct)

Once installed you must edit (or create if you do not have one) your `~/.profile` to export the appropriate Environmental Variable:

 `~/.profile` 
```
...
export QT_QPA_PLATFORMTHEME="qt5ct"

```

After editing the profile logout and back in run [qt5ct](https://www.archlinux.org/packages/?name=qt5ct) in the terminal. Select Style: Oxygen under the Appearance tab and Oxygen under the Icon Theme tab. Press apply and then OK to save your changes.

After this you can run digikam as normal and the icons will be correct.

## Troubleshooting

### Unreadable tool tips

DigiKam has its own widget style setting. If tooltips are either blank (empty rectangles), or unreadable due to a poor foreground and background combination, choose a different widget style:

1.  Navigate to *Settings* > *Configure digiKam* > *Miscellaneous*
2.  Now in *Widget Style*, choose *"Cleanlooks"*

This will have a simple, readable white text on black background in the tool tip.