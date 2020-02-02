Related articles

*   [Color output in console#man](/index.php/Color_output_in_console#man "Color output in console")

[man pages](https://en.wikipedia.org/wiki/Man_page "wikipedia:Man page")—abbreviation for "manual pages"—are the form of documentation that is available on almost all UNIX-like operating systems, including Arch Linux. The command used to display them is `man`.

In spite of their scope, man pages are designed to be self-contained documents, consequentially limiting themselves to referring to other man pages when discussing related subjects. This is in sharp contrast with the hyperlink-aware [Info documents](/index.php/Info_manual "Info manual"), GNU's attempt at replacing the traditional man page format.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Accessing man pages](#Accessing_man_pages)
*   [3 Format](#Format)
*   [4 Searching manuals](#Searching_manuals)
    *   [4.1 Building the manual cache with mandb](#Building_the_manual_cache_with_mandb)
    *   [4.2 Searching for expressions in manuals](#Searching_for_expressions_in_manuals)
    *   [4.3 Getting one-line descriptions with whatis](#Getting_one-line_descriptions_with_whatis)
*   [5 Page width](#Page_width)
*   [6 Reading local man pages](#Reading_local_man_pages)
    *   [6.1 Viewer applications](#Viewer_applications)
    *   [6.2 Conversion to HTML](#Conversion_to_HTML)
        *   [6.2.1 mandoc](#mandoc)
        *   [6.2.2 man2html](#man2html)
        *   [6.2.3 man -H](#man_-H)
        *   [6.2.4 roffit](#roffit)
    *   [6.3 Conversion to PDF](#Conversion_to_PDF)
*   [7 Online man pages](#Online_man_pages)
*   [8 Noteworthy man pages](#Noteworthy_man_pages)
*   [9 See also](#See_also)

## Installation

[man-db](https://www.archlinux.org/packages/?name=man-db) implements *man* on Arch Linux, and [less](/index.php/Core_utilities#Essentials "Core utilities") is the default pager used with *man*.

[man-pages](https://www.archlinux.org/packages/?name=man-pages) provides the Linux man pages.

## Accessing man pages

To read a man page, simply enter:

```
$ man *page_name*

```

Manuals are sorted into several [sections](https://en.wikipedia.org/wiki/Man_page#Manual_sections "wikipedia:Man page"). For a full listing see the section entitled "Sections of the manual pages" in [man-pages(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/man-pages.7).

Man pages are usually referred to by their name, followed by their section number in parentheses. Often there are multiple man pages of the same name, such as [man(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/man.1) and [man(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/man.7). In this case, give man the section number followed by the name of the man page, for example:

```
$ man 5 passwd

```

to read the man page on `/etc/passwd`, rather than the `passwd` utility.

## Format

Man pages all follow a fairly standard format, which helps in navigating them. See the section entitled "Sections within a manual page" in [man-pages(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/man-pages.7).

## Searching manuals

Even though the `man` utility allows users to display man pages, and search their contents via *less*, a problem arises when one knows not the exact name of the desired manual page in the first place! Fortunately, the `-k` or `--apropos` options can be used to search the manual page descriptions for instances of a given keyword.

### Building the manual cache with mandb

The search feature is provided by a dedicated cache, otherwise all searches would give the *nothing appropriate* result. By default, maintenance of that cache is handled by `man-db.service` which gets periodically triggered by `man-db.timer`. You can manually (re)generate the cache or update it by running:

```
# mandb

```

### Searching for expressions in manuals

For example, to search for man pages related to "password":

```
$ man -k password

```

or:

```
$ man --apropos password

```

This is equivalent to calling the `apropos` command:

```
$ apropos password

```

The given keyword is interpreted as a regular expression by default.

If you want to do a more in-depth search by matching the keywords found in the whole articles, you can use the `-K` option:

```
$ man -K password

```

### Getting one-line descriptions with whatis

One-line descriptions of man pages in the man-db cache can be displayed using the `whatis` command. For example, for a brief description of the man page sections about `ls`, type:

 `$ whatis ls` 
```
ls (1p)              - list directory contents
ls (1)               - list directory contents

```

## Page width

The man page width is controlled by the `MANWIDTH` environment variable.

If the number of columns in the terminal is too small (e.g. the window width is narrow), the line breaks will be wrong. This can be very disturbing for reading. You can fix this by setting the MANWIDTH on `man` invocation. With `Bash`, that would be:

 `~/.bashrc` 
```
man() {
    local width=$(tput cols)
    [ $width -gt $MANWIDTH ] && width=$MANWIDTH
    env MANWIDTH=$width \
    man "$@"
}

```

## Reading local man pages

Instead of the standard interface, using browsers such as [lynx](https://www.archlinux.org/packages/?name=lynx) and [Firefox](/index.php/Firefox "Firefox") to view man pages allows users to reap info pages' main benefit of hyperlinked text. Alternatives include the following:

### Viewer applications

*   **GNOME Help** — Help viewer for [GNOME](/index.php/GNOME "GNOME"). It can show man pages via `yelp man:<name>` or the undocumented `CTRL+L` keybinding from an existing window.

	[https://wiki.gnome.org/Apps/Yelp](https://wiki.gnome.org/Apps/Yelp) || [yelp](https://www.archlinux.org/packages/?name=yelp)

*   **KHelpCenter** — Application to show [KDE](/index.php/KDE "KDE") Applications' documentation. Man pages are in *UNIX manual pages* or by running `khelpcenter man:<name>`.

	[https://userbase.kde.org/KHelpCenter](https://userbase.kde.org/KHelpCenter) || [khelpcenter](https://www.archlinux.org/packages/?name=khelpcenter)

*   **[Konqueror](https://en.wikipedia.org/wiki/Konqueror "wikipedia:Konqueror")** — KDE file manager and web browser. It can show man pages via `man:<name>`.

	[https://konqueror.org/](https://konqueror.org/) || [konqueror](https://www.archlinux.org/packages/?name=konqueror)

*   **xman** — Provides a categorized look at man pages.

	[https://xorg.freedesktop.org/](https://xorg.freedesktop.org/) || [xorg-xman](https://www.archlinux.org/packages/?name=xorg-xman)

### Conversion to HTML

#### mandoc

Install the [mandoc](https://aur.archlinux.org/packages/mandoc/) package. To convert a page, for example `free(1)`:

```
$ mandoc -Thtml -Ostyle=style.css /usr/share/man/man1/free.1.gz > free.html

```

Now open the file called `free.html` in your favourite browser.

#### man2html

First, install [man2html](https://www.archlinux.org/packages/?name=man2html) from the official repositories.

Now, convert a man page:

```
$ man free | man2html -compress -cgiurl man$section/$title.$section$subsection.html > ~/man/free.html

```

Another use for `man2html` is exporting to raw, printer-friendly text:

```
$ man free | man2html -bare > ~/free.txt

```

#### man -H

The GNU implementation of man in the Arch repositories also has the ability to do this on its own:

```
$ man -H free

```

This will read your `BROWSER` [environment variable](/index.php/Environment_variable "Environment variable") to determine the browser. You can override this by passing the binary to the `-H` option.

#### roffit

First install [roffit](https://aur.archlinux.org/packages/roffit/) from [AUR](/index.php/AUR "AUR").

To convert a man page:

```
$ gunzip -c /usr/share/man/man1/free.1.gz | roffit > free.html

```

### Conversion to PDF

man pages have always been printable: they are written in troff, which is fundamentally a typesetting language. If you have [ghostscript](https://www.archlinux.org/packages/?name=ghostscript) installed, you can convert a man page to PDF using `man -t <manpage> | ps2pdf - <pdf>`.

Caveats: Fonts are generally limited to Times at hardcoded sizes. There are no hyperlinks. Some man pages were specifically designed for terminal viewing, and won't look right in PS or PDF form.

## Online man pages

There are several online databases of man pages, including:

*   [man7.org](http://man7.org/linux/man-pages/index.html)—The Linux man-pages project. Upstream of the [man-pages](https://www.archlinux.org/packages/?name=man-pages) package.
*   [Arch manual pages](https://jlk.fjfi.cvut.cz/arch/manpages/)—contains man pages from Arch Linux packages. Used for [man page links](/index.php/Template:Man "Template:Man") from the wiki.
*   [manned.org](https://manned.org/)—collection from various Linux distributions, BSD, etc., with multiple package versions
*   [linux.die.net](https://linux.die.net/man/)
*   [man.cx](https://man.cx/)
*   [Debian man pages](https://manpages.debian.org/)
*   [Ubuntu man pages](http://manpages.ubuntu.com/)
*   [DragonFlyBSD man pages](https://leaf.dragonflybsd.org/cgi/web-man)
*   [FreeBSD man pages](https://www.freebsd.org/cgi/man.cgi)
*   [NetBSD man pages](http://netbsd.gw.com/cgi-bin/man-cgi)
*   [OpenBSD man pages](https://man.openbsd.org)
*   [Mac OS X man pages](https://developer.apple.com/documentation/Darwin/Reference/ManPages/index.html)
*   [Plan 9 Manual — Volume 1](http://man.cat-v.org/plan_9/)
*   [Inferno Manual — Volume 1](http://man.cat-v.org/inferno/)
*   [Storage Foundation man pages](http://sfdoccentral.symantec.com/sf/5.0MP3/linux/manpages/index.html)
*   [The UNIX and Linux forums man page repository](https://www.unix.com/man-page-repository.php)

**Tip:** You can use the `!archman` DuckDuckGo [!Bang](https://duckduckgo.com/bang.html) to search through the [Arch Linux man pages](https://jlk.fjfi.cvut.cz/arch/manpages/) directly.

**Warning:** Some distributions provide patched or outdated man pages that differ from those provided by Arch. Exercise caution when using online man pages.

## Noteworthy man pages

Here follows a non-exhaustive list of noteworthy pages that might help you understand a lot of things more in-depth. Some of them might serve as a good reference (like the ASCII table).

*   [ascii(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ascii.7)
*   [boot(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/boot.7)
*   [charsets(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/charsets.7)
*   [chmod(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chmod.1)
*   [credentials(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/credentials.7)
*   [fstab(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fstab.5)
*   [hier(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hier.7)
*   [systemd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.1)
*   [locale(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.1p), [locale(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.5), [locale(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.7)
*   [printf(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/printf.3)
*   [proc(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/proc.5)
*   [regex(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/regex.7)
*   [signal(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/signal.7)
*   [term(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/term.5), [term(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/term.7)
*   [termcap(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/termcap.5)
*   [terminfo(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/terminfo.5)
*   [utf-8(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/utf-8.7)

More generally, have a look at [category 7 (miscellaneous) pages](http://man7.org/linux/man-pages/dir_section_7.html):

```
$ man -s 7 -k ".*" 

```

Arch Linux specific pages:

*   [archlinux(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/archlinux.7)
*   [mkinitcpio(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpio.8)
*   [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8)
*   [pacman-key(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman-key.8)
*   [pacman.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.conf.5)

## See also

*   [man page - Gentoo wiki article](https://wiki.gentoo.org/wiki/Man_page)
*   [Write The Fine Manual with pod2man](https://linuxtidbits.wordpress.com/2013/08/21/wtfm-write-the-fine-manual-with-pod2man-text-converter/)