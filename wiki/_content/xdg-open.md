# xdg-open

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Default applications](/index.php/Default_applications "Default applications")
*   [Environment variables](/index.php/Environment_variables "Environment variables")
*   [Desktop entries](/index.php/Desktop_entries "Desktop entries")

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Default applications](/index.php/Default_applications "Default applications").**

**Notes:** [Talk:Xdg-open#About Merge](/index.php/Talk:Xdg-open#About_Merge "Talk:Xdg-open") (Discuss in [Talk:Xdg-open#](https://wiki.archlinux.org/index.php/Talk:Xdg-open))

**xdg-open** is a desktop-independent tool for configuring the [default applications](/index.php/Default_applications "Default applications") of a user. Many applications invoke the `xdg-open` command internally.

Inside a [desktop environment](/index.php/Desktop_environment "Desktop environment") (like [GNOME](/index.php/GNOME "GNOME"), [KDE](/index.php/KDE "KDE"), or [Xfce](/index.php/Xfce "Xfce")), _xdg-open_ simply passes the arguments to those desktop environment's file-opener application (eg. _gvfs-open_, _kde-open_, or _exo-open_). which means that the associations are left up to the desktop environment.

When no desktop environment is detected (for example when one runs a standalone [window manager](/index.php/Window_manager "Window manager") like eg. [Openbox](/index.php/Openbox "Openbox")), _xdg-open_ will use its own configuration files.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Set the default browser](#Set_the_default_browser)
    *   [2.2 perl-file-mimeinfo](#perl-file-mimeinfo)
*   [3 Drop-in replacements and useful tools](#Drop-in_replacements_and_useful_tools)
    *   [3.1 xdg-open replacements](#xdg-open_replacements)
    *   [3.2 mailcap](#mailcap)
    *   [3.3 mimetype](#mimetype)
    *   [3.4 Environment variables](#Environment_variables)

## Installation

_xdg-open_ is part of the [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) package available in the [official repositories](/index.php/Official_repositories "Official repositories"). It is for use inside a desktop session only, and should not be run as root.

If you run _xdg-open_ without a desktop environment, you should also install [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo), or [xdg-utils-mimeo](https://aur.archlinux.org/packages/xdg-utils-mimeo/)<sup><small>AUR</small></sup> and [mimeo](https://aur.archlinux.org/packages/mimeo/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR") for a faster alternative.

## Configuration

_xdg-open_ is configured by the files mentioned in [Default applications](/index.php/Default_applications#MIME_types_and_desktop_entries "Default applications"). _xdg-mime_ modifies the local file `~/.config/mimeapps.list` and `~/.local/share/applications/mimeapps.list` (deprecated).

To **query** the mime type used by an existing file, use

```
$ xdg-mime query **filetype** _file.ext_

```

Reversely, to query the default [desktop entry](/index.php/Desktop_entry "Desktop entry") associated with a specific mime type, run

```
$ xdg-mime query **default** _mime/type_

```

Examples for _mime/type_ can be:

```
inode/directory (file browser)
image/jpeg (JPEG images)
application/pdf (PDF viewer)
or others

```

To change an associated desktop entry, use:

```
$ xdg-mime **default** _application.desktop_ _mime/type_

```

For example set [Thunar](/index.php/Thunar "Thunar") as the default file browser just run:

```
$ xdg-mime default Thunar.desktop inode/directory

```

This command can take multiple mime-types, allowing related files to be handled by the same program. The example below associates [Emacs](/index.php/Emacs "Emacs") to all known source files:

```
$ xdg-mime default emacs.desktop $(grep '^text/x-*' /usr/share/mime/types)

```

### Set the default browser

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** There are many more MIME types for browsers (Discuss in [Talk:Xdg-open#](https://wiki.archlinux.org/index.php/Talk:Xdg-open))

To set the default application for `http(s)://` web URLs, write

```
$ xdg-mime default _browser_.desktop x-scheme-handler/http
$ xdg-mime default _browser_.desktop x-scheme-handler/https

```

To do so for `.html` files:

```
$ xdg-mime default _browser_.desktop text/html

```

Alternatively, run:

```
$ xdg-settings set default-web-browser _browser_.desktop

```

To test if this was applied successfully, try to open an URL with _xdg-open_ as follows:

```
$ xdg-open [https://archlinux.org](https://archlinux.org)

```

### perl-file-mimeinfo

_xdg-open_ uses [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) as a fallback ("generic") method if no [desktop environment](/index.php/Desktop_environment "Desktop environment") is detected. It can be invoked directly with:

```
$ mimeopen -d /path/to/file

```

You are asked which application to use when opening `/path/to/file`:

```
Please choose a default application for files of type text/plain
       1) notepad  (wine-extension-txt)
       2) Leafpad  (leafpad)
       3) OpenOffice.org Writer  (writer)
       4) gVim  (gvim)
       5) Other...

```

Your answer becomes the default handler for that type of file. Mimeopen is installed as `/usr/bin/vendor_perl/mimeopen`.

## Drop-in replacements and useful tools

### xdg-open replacements

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** There may be some benefit to making this a table, but [Template:App](/index.php/Template:App "Template:App") including upstream URLs gives all needed information in a simple manner (Discuss in [Talk:Xdg-open#](https://wiki.archlinux.org/index.php/Talk:Xdg-open))

<table class="wikitable">

<tbody>

<tr>

<th>Name/Package</th>

<th>Method</th>

<th>Based on</th>

<th>Configuration file</th>

</tr>

<tr>

<td>[busking-git](https://aur.archlinux.org/packages/busking-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/busking-git)]</sup></td>

<td>Regular expressions</td>

<td>[perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo)</td>

<td>custom</td>

</tr>

<tr>

<td>[linopen](https://aur.archlinux.org/packages/linopen/)<sup><small>AUR</small></sup></td>

<td>[file](https://www.archlinux.org/packages/?name=file)</td>

<td>custom</td>

</tr>

<tr>

<td>[mimeo](https://aur.archlinux.org/packages/mimeo/)<sup><small>AUR</small></sup></td>

<td>MIME-type, regular expressions</td>

<td>[file](https://www.archlinux.org/packages/?name=file)</td>

<td>`mimeapps.list`, `defaults.list`; custom is optional</td>

</tr>

<tr>

<td>[mimi-git](https://aur.archlinux.org/packages/mimi-git/)<sup><small>AUR</small></sup></td>

<td>[file](https://www.archlinux.org/packages/?name=file)</td>

<td>custom</td>

</tr>

<tr>

<td>[whippet](https://aur.archlinux.org/packages/whippet/)<sup><small>AUR</small></sup></td>

<td>MIME-type, name, regular expressions</td>

<td>SQLite database or [file](https://www.archlinux.org/packages/?name=file), [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo), etc</td>

<td>custom SQLite database or `mimeapps.list`</td>

</tr>

<tr>

<td>[ayr](https://aur.archlinux.org/packages/ayr/)<sup><small>AUR</small></sup></td>

<td>MIME-type, name, regular expressions</td>

<td>[file](https://www.archlinux.org/packages/?name=file) or [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo), etc</td>

<td>`mimeapps.list`, `defaults.list`</td>

</tr>

<tr>

<td>[sx-open](https://aur.archlinux.org/packages/sx-open/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/sx-open)]</sup></td>

<td>Regular expressions</td>

<td>[file](https://www.archlinux.org/packages/?name=file), bash regex</td>

<td>custom</td>

</tr>

<tr>

<td>[ranger](https://www.archlinux.org/packages/?name=ranger) (rifle command)</td>

<td>MIME-type, name, regular expressions</td>

<td>custom</td>

</tr>

</tbody>

</table>

**Note:** Some of the above packages replace `xdg-utils`. Those that do not can be symbolically linked to _xdg-open_ in the user's `$PATH` above `/usr/bin`, but some applications hard-code the absolute path `/usr/bin/xdg-open`. In this case, install [xdg-utils-no-open](https://aur.archlinux.org/packages/xdg-utils-no-open/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR") and copy the replacement to `/usr/bin/xdg-open`.

### mailcap

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** When using [run-mailcap](https://aur.archlinux.org/packages/run-mailcap/)<sup><small>AUR</small></sup>, _xdg-open_ may refer to it.[[1]](http://cgit.freedesktop.org/xdg/xdg-utils/tree/scripts/xdg-open.in#n266) It should then clearly not be combined with the below file to prevent endless loops. (Discuss in [Talk:Xdg-open#](https://wiki.archlinux.org/index.php/Talk:Xdg-open))

The _.mailcap_ file format is used by mail programs such as [mutt](https://www.archlinux.org/packages/?name=mutt) and [sylpheed](https://www.archlinux.org/packages/?name=sylpheed). To have those programs use _xdg-open_, edit `~/.mailcap`:

 `~/.mailcap` 

```
*/*; xdg-open "%s"

```

### mimetype

_mimetype_ in [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) package can display some mimetype-related information about a file.

For example:

```
$ mimetype file.ext

```

returns the mimetype of a file,

```
$ mimetype -d file.extension

```

returns a description of that mimetype.

When _xdg-open_ fails to detect one of the [desktop environments](/index.php/Desktop_environments "Desktop environments") it knows about, it normally falls back to using `file -i`, which uses only file contents to determine the mimetype, resulting in some file types not being detected correctly. With _mimetype_ available, _xdg-open_ will use that instead, with better detection results, as _mimetype_ uses the information in the [shared mime info database](http://standards.freedesktop.org/shared-mime-info-spec/shared-mime-info-spec-0.18.html).

### Environment variables

Some environment variables, such as `BROWSER`, `DE`, and `DESKTOP_SESSION`, will change the behaviour of the default _xdg-open_. See [Environment variables](/index.php/Environment_variables "Environment variables") for more information.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Xdg-open&oldid=415692](https://wiki.archlinux.org/index.php?title=Xdg-open&oldid=415692)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Desktop environments](/index.php/Category:Desktop_environments "Category:Desktop environments")

Hidden categories:

*   [Pages or sections flagged with Template:Merge](/index.php/Category:Pages_or_sections_flagged_with_Template:Merge "Category:Pages or sections flagged with Template:Merge")
*   [Pages or sections flagged with Template:Accuracy](/index.php/Category:Pages_or_sections_flagged_with_Template:Accuracy "Category:Pages or sections flagged with Template:Accuracy")
*   [Pages or sections flagged with Template:Style](/index.php/Category:Pages_or_sections_flagged_with_Template:Style "Category:Pages or sections flagged with Template:Style")
*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")