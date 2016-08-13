**man pages**—abbreviation for "manual pages"—are the extensive documentation that comes preinstalled with almost all substantial UNIX-like operating systems, including Arch Linux. The command used to display them is `man`.

In spite of their scope, man pages are designed to be self-contained documents, consequentially limiting themselves to referring to other man pages when discussing related subjects. This is in sharp contrast with the hyperlink-aware info files, GNU's attempt at replacing the traditional man page format.

[less](/index.php/Core_utilities#less "Core utilities") is the default pager used with *man*.

## Contents

*   [1 Accessing man pages](#Accessing_man_pages)
*   [2 Format](#Format)
*   [3 Searching manuals](#Searching_manuals)
*   [4 Colored man pages](#Colored_man_pages)
*   [5 Dynamic page width](#Dynamic_page_width)
*   [6 Reading local man pages](#Reading_local_man_pages)
    *   [6.1 Converting to browser-readable HTML](#Converting_to_browser-readable_HTML)
        *   [6.1.1 mdocml](#mdocml)
        *   [6.1.2 man2html](#man2html)
        *   [6.1.3 man -H](#man_-H)
        *   [6.1.4 roffit](#roffit)
    *   [6.2 Converting to PDF](#Converting_to_PDF)
*   [7 Online Man Pages](#Online_Man_Pages)
*   [8 Noteworthy manpages](#Noteworthy_manpages)
*   [9 See also](#See_also)

## Accessing man pages

To read a man page, simply enter:

```
$ man *page_name*

```

Manuals are sorted into several sections. For a full listing see the section entitled "Sections of the manual pages" in `man man-pages`.

Man pages are usually referred to by their name, followed by their section number in parentheses. Often there are multiple man pages of the same name, such as man(1) and man(7). In this case, give man the section number followed by the name of the man page, for example:

```
$ man 5 passwd

```

to read the man page on `/etc/passwd`, rather than the `passwd` utility.

One-line descriptions of man pages can be displayed using the `whatis` command. For example, for a brief description of the man page sections about `ls`, type:

 `$ whatis ls` 
```
ls (1p)              - list directory contents
ls (1)               - list directory contents
```

## Format

Man pages all follow a fairly standard format, which helps in navigating them. See the section entitled "Sections within a manual page" in `man man-pages`.

## Searching manuals

Even though the `man` utility allows users to display man pages, and search their contents via *less*, a problem arises when one knows not the exact name of the desired manual page in the first place! Fortunately, the `-k` or `--apropos` options can be used to search the manual page descriptions for instances of a given keyword.

The research feature is provided by a dedicated cache. By default you may not have any cache built and all your searches will give you the *nothing appropriate* result. You can generate the cache or update it by running

```
# mandb

```

You should run it everytime a new manpage is installed.

Now you can begin your search. For example, to search for man pages related to "password":

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

## Colored man pages

See [Color output in console#man](/index.php/Color_output_in_console#man "Color output in console").

## Dynamic page width

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

Feel free to combine this function with the [color settings](#Colored_man_pages).

## Reading local man pages

Instead of the standard interface, using browsers such as [lynx](https://www.archlinux.org/packages/?name=lynx) and [Firefox](/index.php/Firefox "Firefox") to view man pages allows users to reap info pages' main benefit of hyperlinked text. Alternatives include the following:

*   [KDE](/index.php/KDE "KDE") users can read man pages in Konqueror using `man:<name>`.
*   [xorg-xman](https://www.archlinux.org/packages/?name=xorg-xman) provides a categorized look at man pages in [X](/index.php/X "X").
*   The [GNOME](/index.php/GNOME "GNOME") Help Browser [yelp](https://www.archlinux.org/packages/?name=yelp) can be used via `yelp man:<name>`.

### Converting to browser-readable HTML

#### mdocml

Install [mdocml](https://aur.archlinux.org/packages/mdocml/) from [AUR](/index.php/AUR "AUR"). To convert a page, for example `free(1)`:

```
$ gunzip -c /usr/share/man/man1/free.1.gz | mandoc -Thtml -Ostyle=style.css 1> free.html

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

### Converting to PDF

man pages have always been printable: they are written in troff, which is fundamentally a typesetting language. If you have ghostscript installed, converting a man page to PDF is actually very easy: `man -t <manpage> | ps2pdf - <pdf>`. [This google image search](https://www.google.com/search?q=manpage+pdf+troff&num=100&hl=en&prmd=imvns&source=lnms&tbm=isch&sa=X&ei=5BZpUI3oH6rI2AXvx4CoAw&ved=0CAoQ_AUoAQ&biw=1321&bih=1100) should give you an idea of what the result looks like; it may not be to everybody's liking.

Caveats: Fonts are generally limited to Times at hardcoded sizes. There are no hyperlinks. Some man pages were specifically designed for terminal viewing, and won't look right in PS or PDF form.

The following perl script converts man pages to PDFs, caches the PDFs in the `$HOME/.manpdf/` directory, and calls a PDF viewer, specifically [mupdf](https://www.archlinux.org/packages/?name=mupdf).

 `Usage: manpdf [<section>] <manpage>` 
```
#!/usr/bin/perl
use File::stat;

$pdfdir = $ENV{"HOME"}."/.manpdf";
-d $pdfdir || mkdir $pdfdir || die "can't create $pdfdir";
$manpage = $ARGV[0];
chop($manpath = `man -w $manpage`);
die if $?;

$maninfo = stat($manpath) or die;
$manpath =~ s@.*/man./(.*)(\.(gz|bz2))?$@$1@;
$pdfpath = "$pdfdir/$manpath.pdf";
$pdftime = 0;
if (-f $pdfpath) {
    $pdfinfo = stat($pdfpath) or die;
    $pdftime = $pdfinfo->mtime;
}
if (!-f $pdfpath || $maninfo->mtime > $pdftime) {
    system "man -t $manpage | ps2pdf -dPDFSETTINGS=/screen - $pdfpath";
}
die if !-f $pdfpath;
if (!fork) {
    open(STDOUT, "/dev/null");
    open(STDERR, "/dev/null");
    exec "mupdf", "-r", "96", $pdfpath;
    #exec "acroread", $pdfpath;
}

```

## Online Man Pages

There are several online databases of man pages, including:

*   [Man7.org.](http://man7.org/linux/man-pages/index.html) Upstream for Arch Linux's [man-pages](https://www.archlinux.org/packages/?name=man-pages).
*   [*Debian GNU/Linux man pages*](http://manpages.debian.net/)
*   [*DragonFlyBSD manual pages*](http://leaf.dragonflybsd.org/cgi/web-man)
*   [*FreeBSD Hypertext Man Pages*](http://www.freebsd.org/cgi/man.cgi)
*   [*Linux and Solaris 10 Man Pages*](http://www.manpages.spotlynx.com/)
*   [*Linux/FreeBSD Man Pages*](http://manpagehelp.net) with user comments
*   [*Linux man pages at die.net*](http://linux.die.net/man/)
*   [The Linux man-pages project at kernel.org](http://www.kernel.org/doc/man-pages/)
*   [*NetBSD manual pages*](http://netbsd.gw.com/cgi-bin/man-cgi)
*   [*Mac OS X Manual Pages*](http://developer.apple.com/documentation/Darwin/Reference/ManPages/index.html)
*   [*On-line UNIX manual pages*](http://unixhelp.ed.ac.uk/alphabetical/index.html)
*   [*OpenBSD manual pages*](http://www.openbsd.org/cgi-bin/man.cgi)
*   [*Plan 9 Manual — Volume 1*](http://man.cat-v.org/plan_9/)
*   [*Inferno Manual — Volume 1*](http://man.cat-v.org/inferno/)
*   [*Storage Foundation Man Pages*](http://sfdoccentral.symantec.com/sf/5.0MP3/linux/manpages/index.html)
*   [*The UNIX and Linux Forums Man Page Repository*](http://www.unix.com/man-page/OpenSolaris/1/man/)
*   [*Ubuntu Manpage Repository*](http://manpages.ubuntu.com/)

**Warning:** Some distributions provide patched or outdated man pages that differ from those provided by Arch. Exercise caution when using online man pages.

## Noteworthy manpages

Here follows a non-exhaustive list of noteworthy pages that might help you understand a lot of things more in-depth. Some of them might serve as a good reference (like the ascii table).

*   ascii(7)
*   boot(7)
*   charsets(7)
*   chmod(1)
*   credentials(7)
*   fstab(5)
*   hier(7)
*   systemd(1)
*   locale(1P)(5)(7)
*   printf(3)
*   proc(5)
*   regex(7)
*   signal(7)
*   term(5)(7)
*   termcap(5)
*   terminfo(5)
*   utf-8(7)

More generally, have a look at category 7 pages:

```
$ man -s 7 -k ".*" 

```

Arch Linux specific pages:

*   archlinux(7)
*   mkinitcpio(8)
*   pacman(8)
*   pacman-key(8)
*   pacman.conf(5)

## See also

*   [man page - Gentoo wiki article](http://wiki.gentoo.org/wiki/Man_page)
*   [Setting colors for less](http://unix.stackexchange.com/a/147) and [solving related problems](http://unix.stackexchange.com/a/6357) (threads on StackExchange)
*   [Write The Fine Manual with pod2man](https://linuxtidbits.wordpress.com/2013/08/21/wtfm-write-the-fine-manual-with-pod2man-text-converter/)