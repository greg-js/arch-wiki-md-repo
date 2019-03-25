Related articles

*   [Copying text from a terminal](/index.php/Copying_text_from_a_terminal "Copying text from a terminal")
*   [Firefox#Middle-click errors](/index.php/Firefox#Middle-click_errors "Firefox")
*   [GTK+#Disable mouse paste](/index.php/GTK%2B#Disable_mouse_paste "GTK+")
*   [Vim#Clipboard](/index.php/Vim#Clipboard "Vim")

According to [Wikipedia](https://en.wikipedia.org/wiki/Clipboard_(computing) "wikipedia:Clipboard (computing)"):

	The clipboard is a facility used for short-term data storage and/or data transfer between documents or applications, via [copy and paste](https://en.wikipedia.org/wiki/copy_and_paste "wikipedia:copy and paste") operations.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 History](#History)
*   [2 Selections](#Selections)
*   [3 Tools](#Tools)
*   [4 Managers](#Managers)
*   [5 See also](#See_also)

## History

In X10, *cut buffers* were introduced. These were limited buffers that stored arbitrary text and were used by most applications. However, they were inefficient and implementation of them varied, so selections were introduced. Cut buffers are long deprecated, and although some applications (such as [xterm](/index.php/Xterm "Xterm")) may have legacy support for them, it is both not likely and not recommended that they be used.

## Selections

[Freedesktop.org](/index.php/Freedesktop.org "Freedesktop.org") describes the two main *selections* as follows:[[4]](https://specifications.freedesktop.org/clipboards-spec/clipboards-latest.txt)

	PRIMARY

	Used for the currently selected text, even if it is not explicitly copied, and for middle-mouse-click pasting. In some cases, pasting is also possible with a keyboard shortcut.

	CLIPBOARD

	Used for explicit copy/paste commands involving keyboard shortcuts or menu items. Hence, it behaves like the single-clipboard system on Windows. Unlike PRIMARY, it can also handle [multiple data formats](https://stackoverflow.com/questions/3571179/how-does-x11-clipboard-handle-multiple-data-formats).

The majority of programs for [Xorg](/index.php/Xorg "Xorg"), including [Qt](/index.php/Qt "Qt") and [GTK+](/index.php/GTK%2B "GTK+") applications, follow this behavior. While [ICCCM](https://tronche.com/gui/x/icccm/) also defines a SECONDARY selection, it does not have a consensually agreed upon purpose. Despite the naming, all three selections are basically "clipboards". Rather than the old "cut buffers" system where arbitrary applications could modify data stored in the cut buffers, only one application may control or "own" a selection at one time. This prevents inconsistencies in the operation of the selections.

See the [Keyboard shortcuts](/index.php/Keyboard_shortcuts "Keyboard shortcuts") page which lists the default shortcuts in many programs.

It is also important to realize that according to the selection protocols, nothing is copied [until it is pasted](https://unix.stackexchange.com/questions/213840/how-to-toggle-or-turn-off-text-selection-being-sent-to-the-clipboard/213843#213843). For example, if you select some word in a terminal window, close the terminal and then want to paste it somewhere else, it will not work because the terminal is gone and the text has not been copied anywhere. If you want the word to be preserved after closing terminal window, consider installing a [clipboard manager](/index.php/Clipboard_manager "Clipboard manager").

**Note:** [Clipboard managers](#Managers) can significantly change the user experience, for example they might synchronize the PRIMARY and CLIPBOARD selections to emulate a single-clipboard system.

## Tools

This section lists command-line tools to manipulate the clipboards.

*   **sselp** — Simple X selection printer. Prints the X selection to stdout.

	[http://tools.suckless.org/x/sselp](http://tools.suckless.org/x/sselp) || [sselp](https://aur.archlinux.org/packages/sselp/)

*   **xclip** — A lightweight, command-line based interface to the clipboard.

	[https://github.com/astrand/xclip](https://github.com/astrand/xclip) || [xclip](https://www.archlinux.org/packages/?name=xclip)

*   **xsel** — Command-line program for getting and setting the contents of the X selection.

	[http://www.vergenet.net/~conrad/software/xsel/](http://www.vergenet.net/~conrad/software/xsel/) || [xsel](https://www.archlinux.org/packages/?name=xsel)

## Managers

This section lists daemons that track your clipboard, to provide a clipboard history and/or synchronization.

*   **Anamnesis** — Clipboard manager that stores all the clipboard history and offers an interface to do a full-text search. It has both a command line and GUI mode available.

	[http://anamnesis.sourceforge.net/](http://anamnesis.sourceforge.net/) || [anamnesis](https://aur.archlinux.org/packages/anamnesis/)

*   **Autocutsel** — Command line and daemon interfaces to synchronize PRIMARY, `CLIPBOARD` and cut buffer selections.

	[http://www.nongnu.org/autocutsel/](http://www.nongnu.org/autocutsel/) || [autocutsel](https://www.archlinux.org/packages/?name=autocutsel)

*   **Clipboard Indicator** — Clipboard manager extension for GNOME Shell. Adds a clipboard indicator to the top panel, and caches clipboard history.

	[https://github.com/Tudmotu/gnome-shell-extension-clipboard-indicator](https://github.com/Tudmotu/gnome-shell-extension-clipboard-indicator) || [gnome-shell-extension-clipboard-indicator-git](https://aur.archlinux.org/packages/gnome-shell-extension-clipboard-indicator-git/)

*   **ClipIt** — Fork of Parcellite.It has both a command line and GUI mode available.

	[https://github.com/CristianHenzel/ClipIt](https://github.com/CristianHenzel/ClipIt) || [clipit](https://aur.archlinux.org/packages/clipit/)

*   **Clipman** — Clipboard manager plugin for the Xfce4 panel. It keeps the clipboard contents around while it is usually lost when you close an application. It is able to handle text and images, and has a feature to execute actions on specific text selections by matching them against regular expressions.

	[https://goodies.xfce.org/projects/panel-plugins/xfce4-clipman-plugin](https://goodies.xfce.org/projects/panel-plugins/xfce4-clipman-plugin) || [xfce4-clipman-plugin](https://www.archlinux.org/packages/?name=xfce4-clipman-plugin)

*   **ClipManager** — Cross-platform clipboard manager written in Python and Qt.

	[https://github.com/scottwernervt/clipmanager](https://github.com/scottwernervt/clipmanager) || [clipmanager](https://aur.archlinux.org/packages/clipmanager/)

*   **Clipmenu** — Dmenu based clipboard manager

	[https://github.com/cdown/clipmenu/](https://github.com/cdown/clipmenu/) || [clipmenu](https://www.archlinux.org/packages/?name=clipmenu)

*   **Clipster** — A lightweight, command-line-driven clipboard manager, written in Python.

	[https://github.com/mrichar1/clipster](https://github.com/mrichar1/clipster) || [clipster](https://aur.archlinux.org/packages/clipster/), [clipster-git](https://aur.archlinux.org/packages/clipster-git/)

*   **CopyQ** — Clever Qt clipboard manager with searchable and editable history, custom actions on items and command line support.

	[https://github.com/hluk/CopyQ](https://github.com/hluk/CopyQ) || [copyq](https://www.archlinux.org/packages/?name=copyq)

*   **[Glipper](https://en.wikipedia.org/wiki/Glipper "wikipedia:Glipper")** — Clipboard manager for the GNOME desktop with many features and plugin support.

	[https://launchpad.net/glipper](https://launchpad.net/glipper) || [glipper](https://aur.archlinux.org/packages/glipper/)

*   **GPaste** — Clipboard management system that aims at being a new generation Parcellite, with a modular structure split in a couple of libraries and a daemon for adaptability. Offers a GNOME Shell extension and a CLI interface.

	[https://github.com/Keruspe/GPaste](https://github.com/Keruspe/GPaste) || [gpaste](https://www.archlinux.org/packages/?name=gpaste)

*   **[Greenclip](/index.php/Greenclip "Greenclip")** — Simple clipboard manager to be integrated with rofi

	[https://github.com/erebe/greenclip](https://github.com/erebe/greenclip) || [rofi-greenclip](https://aur.archlinux.org/packages/rofi-greenclip/)

*   **[Klipper](https://en.wikipedia.org/wiki/Klipper "wikipedia:Klipper")** — Full featured clipboard manager for the KDE desktop.

	[https://userbase.kde.org/Klipper](https://userbase.kde.org/Klipper) || [plasma-workspace](https://www.archlinux.org/packages/?name=plasma-workspace)

*   **Parcellite** — Lightweight yet feature-rich clipboard manager. It has both a command line and GUI mode available.

	[http://parcellite.sourceforge.net/](http://parcellite.sourceforge.net/) || [parcellite](https://www.archlinux.org/packages/?name=parcellite)

*   **Pasteall** — Clipboard monitor simple and functional (with notifications in Portuguese).

	[https://github.com/ShyPixie/Pasteall](https://github.com/ShyPixie/Pasteall) || [pasteall](https://aur.archlinux.org/packages/pasteall/)

*   **Qlipper** — Lightweight and cross-platform clipboard history applet based on Qt.

	[https://github.com/pvanek/qlipper/](https://github.com/pvanek/qlipper/) || [qlipper](https://aur.archlinux.org/packages/qlipper/)

*   **xclipboard** — Official X clipboard command-line client.

	[https://www.x.org/releases/X11R7.5/doc/man/man1/xclipboard.1.html](https://www.x.org/releases/X11R7.5/doc/man/man1/xclipboard.1.html) || [xorg-xclipboard](https://www.archlinux.org/packages/?name=xorg-xclipboard)

*   **xcmenu** — Clipboard synchronizer developed for window manager users.

	[https://github.com/dindon-sournois/xcmenu](https://github.com/dindon-sournois/xcmenu) || [xcmenu-git](https://aur.archlinux.org/packages/xcmenu-git/)

## See also

*   [Cut-and-paste in X](https://specifications.freedesktop.org/clipboards-spec/clipboards-latest.txt)
*   [X Selections, Cut Buffers, and Kill Rings.](https://www.jwz.org/doc/x-cut-and-paste.html)