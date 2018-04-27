[xdg-utils](https://www.freedesktop.org/wiki/Software/xdg-utils/) ([xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils)) provides the official utilities for managing [XDG MIME Applications](/index.php/XDG_MIME_Applications "XDG MIME Applications").

*   [xdg-desktop-menu(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-desktop-menu.1) - Install desktop menu items
*   [xdg-desktop-icon(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-desktop-icon.1) - copies [desktop entries](/index.php/Desktop_entries "Desktop entries") to the user's desktop
*   [xdg-email(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-email.1) - Compose a new email in the user's preferred email client, potentially with subject and other info filled in
*   [xdg-icon-resource(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-icon-resource.1) - Install icon resources
*   [xdg-mime(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-mime.1) - Query and install MIME types and associations
*   [xdg-open(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-open.1) - Open a file or URI in the user's preferred application
*   [xdg-screensaver(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-screensaver.1) - Enable, disable, or suspend the screensaver
*   [xdg-settings(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-settings.1) - Get or set the default web browser and URL handlers

## xdg-mime

See [xdg-mime(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-mime.1).

Determine a file's MIME type:

```
$ xdg-mime query filetype photo.jpeg
image/jpeg

```

Determine the default application for a MIME type:

```
$ xdg-mime query default image/jpeg
gimp.desktop

```

Change the default application for a MIME type:

```
$ xdg-mime default feh.desktop image/jpeg

```

## xdg-open

xdg-open is a [resource opener](/index.php/Resource_opener "Resource opener") that implements [XDG MIME Applications](/index.php/XDG_MIME_Applications "XDG MIME Applications") and is used by many programs, see [xdg-open(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-open.1) for the usage.

xdg-open is desktop-environment-independent in the sense that it attempts to use each environment's native default application tool.

If no desktop environment is detected, MIME type detection falls back to using [file](https://www.archlinux.org/packages/?name=file) which—ironically—does not implement the XDG standard. If you want xdg-open to use [XDG MIME Applications](/index.php/XDG_MIME_Applications "XDG MIME Applications") without a desktop environment, you will need to [install](/index.php/Install "Install") [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) or switch to one of the [resource openers](/index.php/Resource_opener "Resource opener") that support [XDG MIME Applications](/index.php/XDG_MIME_Applications "XDG MIME Applications").

## xdg-settings

See [xdg-settings(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-settings.1).

Shortcut to open all web MIME types with a single application:

```
$ xdg-settings set default-web-browser firefox.desktop

```

Shortcut for setting the default application for a URL scheme:

```
$ xdg-settings set default-url-scheme-handler irc xchat.desktop

```