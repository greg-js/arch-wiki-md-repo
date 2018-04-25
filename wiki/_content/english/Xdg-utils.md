[xdg-utils](https://www.freedesktop.org/wiki/Software/xdg-utils/) ([xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils)) provides the official utilities for managing [XDG MIME Applications](/index.php/XDG_MIME_Applications "XDG MIME Applications"). Most importantly, it provides `xdg-open` which many applications use to open a file with its default application. It is desktop-environment-independent in the sense that it attempts to use each environment's native default application tool and provides its own mechanism if no known environment is detected. Examples:

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

See [xdg-open(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-open.1).

Open a file with its default application:

```
$ xdg-open photo.jpeg

```

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

**Tip:** If no desktop environment is detected, MIME type detection falls back to using [file](https://www.archlinux.org/packages/?name=file) which—ironically—does not implement the XDG standard. If you want [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) to work properly without a desktop environment, you will need to install [#perl-file-mimeinfo](#perl-file-mimeinfo) or one of the [#xdg-open alternatives](#xdg-open_alternatives).