# man page

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**man pages** (abbreviation for "manual pages") are the extensive documentation that comes preinstalled with almost all substantial UNIX-like operating systems, including Arch Linux. The command used to display them is `man`.

In spite of their scope, man pages are designed to be self-contained documents, consequentially limiting themselves to referring to other man pages when discussing related subjects. This is in sharp contrast with the hyperlink-aware info files, GNU's attempt at replacing the traditional man page format.

[less](/index.php/Core_utilities#less "Core utilities") is the default pager used with _man_.

## Contents

*   [1 Accessing Man Pages](#Accessing_Man_Pages)
*   [2 Format](#Format)
*   [3 Searching manuals](#Searching_manuals)
*   [4 Colored man pages](#Colored_man_pages)
    *   [4.1 Using less (Recommended)](#Using_less_.28Recommended.29)
        *   [4.1.1 If less doesn't display color man pages](#If_less_doesn.27t_display_color_man_pages)
    *   [4.2 Using most (Not recommended)](#Using_most_.28Not_recommended.29)
    *   [4.3 Colored man pages on xterm or rxvt-unicode](#Colored_man_pages_on_xterm_or_rxvt-unicode)
        *   [4.3.1 xterm](#xterm)
        *   [4.3.2 rxvt-unicode](#rxvt-unicode)
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

## Accessing Man Pages

To read a man page, simply enter:

```
$ man _page_name_

```

Manuals are sorted into several sections:

1.  General commands
2.  System calls (functions provided by the kernel)
3.  Library calls (C library functions)
4.  Special files (usually found in /dev) and drivers
5.  File formats and conventions
6.  Games
7.  Miscellaneous (including conventions)
8.  System administration commands (usually requiring root privileges) and daemons

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

Man pages all follow a fairly standard format, which helps in navigating them. Some sections which are often present include:

*   NAME - The name of the command and a one-line statement of its purpose.
*   SYNOPSIS - A list of the options and arguments a command takes or the parameters the function takes and its header file.
*   DESCRIPTION - A more in depth description of a command or function's purpose and workings.
*   EXAMPLES - Common examples, usually ranging from the simple to the relatively complex.
*   OPTIONS - Descriptions of each of the options a command takes and what they do.
*   EXIT STATUS - The meanings of different exit codes.
*   FILES - Files related to a command or function.
*   BUGS - Problems with the command or function that are pending repair. Also known as KNOWN BUGS.
*   SEE ALSO - A list of related commands or functions.
*   AUTHOR, HISTORY, COPYRIGHT, LICENSE, WARRANTY - Information about the program, its past, its terms of use, and its creator.

## Searching manuals

Whilst the `man` utility allows users to display man pages, and search their contents via _less_, a problem arises when one knows not the exact name of the desired manual page in the first place! Fortunately, the `-k` or `--apropos` options can be used to search the manual page descriptions for instances of a given keyword.

The research feature is provided by a dedicated cache. By default you may not have any cache built and all your searches will give you the _nothing appropriate_ result. You can generate the cache or update it by running

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

Color-enabled man pages allow for a clearer presentation and easier digestion of the content. There are two prevalent methods for achieving colored man pages: using `less`, or opting for `most`.

### Using less (Recommended)

<small>_Source: [Less Colors For Man Pages | Linux Tidbits](http://linuxtidbits.wordpress.com/2009/03/23/less-colors-for-man-pages/)_</small>

This method has the advantage that `less` has a bigger feature set than `most`, and is the default for viewing man pages.

Add the following to a shell configuration file. For [Bash](/index.php/Bash "Bash") it would be:

 `~/.bashrc` 

```
man() {
    env LESS_TERMCAP_mb=$'\E[01;31m' \
    LESS_TERMCAP_md=$'\E[01;38;5;74m' \
    LESS_TERMCAP_me=$'\E[0m' \
    LESS_TERMCAP_se=$'\E[0m' \
    LESS_TERMCAP_so=$'\E[38;5;246m' \
    LESS_TERMCAP_ue=$'\E[0m' \
    LESS_TERMCAP_us=$'\E[04;38;5;146m' \
    man "$@"
}

```

To see the changes in your Man Pages (without restarting bash or linux), you may run:

```
# source ~/.bashrc

```

For [Fish](/index.php/Fish "Fish") a basic configuration would be:

 `~/.config/fish/config.fish` 

```
set -xU LESS_TERMCAP_mb (printf "\e[01;31m")      # begin blinking
set -xU LESS_TERMCAP_md (printf "\e[01;31m")      # begin bold
set -xU LESS_TERMCAP_me (printf "\e[0m")          # end mode
set -xU LESS_TERMCAP_se (printf "\e[0m")          # end standout-mode
set -xU LESS_TERMCAP_so (printf "\e[01;44;33m")   # begin standout-mode - info box
set -xU LESS_TERMCAP_ue (printf "\e[0m")          # end underline
set -xU LESS_TERMCAP_us (printf "\e[01;32m")      # begin underline

```

To see the changes in your Man Pages (without restarting fish or linux), you may run:

```
# source ~/.config/fish/config.fish

```

For a detailed explanation on these variables, see [this answer](http://unix.stackexchange.com/questions/108699/documentation-on-less-termcap-variables/108840#108840). To customize the colors, see [Wikipedia:ANSI escape code](https://en.wikipedia.org/wiki/ANSI_escape_code "wikipedia:ANSI escape code") for reference.

#### If less doesn't display color man pages

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** Which terminals on which systems don't support [SGR escape sequences](https://en.wikipedia.org/wiki/ANSI_escape_code#SGR "wikipedia:ANSI escape code")? Old versions of _less_ are not supported on Arch. Anyway, this option _disables_ colors, and everything _might_ have been just fine until the above has been applied. (Discuss in [Talk:Man page#](https://wiki.archlinux.org/index.php/Talk:Man_page))

On some systems, terminals don't understand SGR escape sequences, and older versions of `less` (without the -R option) don't understand SGR either. `Groff` offers a few solutions to fix this. The easiest one is to set and export the variable `GROFF_NO_SGR` in your terminal environment:

```
 export GROFF_NO_SGR=1

```

This tells `groff` to make adjustments when it is passed a man page for formatting.

### Using most (Not recommended)

The basic function of 'most' is similar to `less` and `more`, but it has a smaller feature set. Configuring most to use colors is easier than using less, but additional configuration is necessary to make most behave like less. Install [most](https://www.archlinux.org/packages/?name=most) using [pacman](/index.php/Pacman "Pacman"):

```
# pacman -S most

```

Edit `/etc/man_db.conf`, uncomment the pager definition and change it to:

```
DEFINE     pager     most -s

```

Test the new setup by typing:

```
$ man whatever_man_page

```

Modifying the color values requires editing `~/.mostrc` (creating the file if it is not present) or editing `/etc/most.conf` for system-wide changes. Example `~/.mostrc`:

```
% Color settings
color normal lightgray black
color status yellow blue
color underline yellow black
color overstrike brightblue black

```

Another example showing keybindings similar to `less` (jump to line is set to 'J'):

```
% less-like keybindings
unsetkey "^K"
unsetkey "g"
unsetkey "G"
unsetkey ":"

setkey next_file ":n"
setkey find_file ":e"
setkey next_file ":p"
setkey toggle_options ":o"
setkey toggle_case ":c"
setkey delete_file ":d"
setkey exit ":q"

setkey bob "g"
setkey eob "G"
setkey down "e"
setkey down "E"
setkey down "j"
setkey down "^N"
setkey up "y"
setkey up "^Y"
setkey up "k"
setkey up "^P"
setkey up "^K"
setkey page_down "f"
setkey page_down "^F"
setkey page_up "b"
setkey page_up "^B"
setkey other_window "z"
setkey other_window "w"
setkey search_backward "?"
setkey bob "p"
setkey goto_mark "'"
setkey find_file "E"
setkey edit "v"

```

### Colored man pages on xterm or rxvt-unicode

<small>_Source: [XFree resources file for XTerm program](http://pub.ligatura.org/fs/xfree86/xresources/xterm)_</small><sup>[[dead link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot") 2013-09-10]</sup>

A quick way to add color to manual pages viewed on [xterm](https://www.archlinux.org/packages/?name=xterm)/`uxterm` or [rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode) is to modify `~/.Xresources`.

#### xterm

```
*VT100.colorBDMode:     true
*VT100.colorBD:         red
*VT100.colorULMode:     true
*VT100.colorUL:         cyan

```

which _replaces_ the decorations with the colors. Also add:

```
*VT100.veryBoldColors: 6

```

if you want colors and decorations (bold or underline) _at the same time_. See `man xterm` for a description of the `veryBoldColors` resource.

#### rxvt-unicode

```
URxvt.colorIT:      #87af5f
URxvt.colorBD:      #d7d7d7
URxvt.colorUL:      #87afd7

```

Run:

```
$ xrdb -load ~/.Xresources

```

Launch a new `xterm/uxterm` or `rxvt-unicode` and you should see colorful man pages. This combination puts colors to **bold** and <u>underlined</u> words in `xterm/uxterm` or to **bold**, <u>underlined</u>, and _italicized_ text in `rxvt-unicode`. You can play with different combinations of these attributes (see the [sources](http://pub.ligatura.org/fs/xfree86/xresources/xterm)<sup>[[dead link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot") 2013-09-10]</sup> of this item).

## Dynamic page width

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** How is this dynamic? If you later resize the terminal window, the line breaks will still become wrong. (Discuss in [Talk:Man page#](https://wiki.archlinux.org/index.php/Talk:Man_page))

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

Instead of the standard interface, using browsers such as [lynx](https://www.archlinux.org/packages/?name=lynx) and [Firefox](/index.php/Firefox "Firefox") to view man pages allows users to reap info pages' main benefit: hyperlinked text.

[KDE](/index.php/KDE "KDE") users can read man pages in Konqueror using:

```
man:<name>

```

From the [Official repositories](/index.php/Official_repositories "Official repositories") come two other possibilities:

1\. [xorg-xman](https://www.archlinux.org/packages/?name=xorg-xman) provides a categorized look at man pages in [X](/index.php/X "X").

2\. The [GNOME](/index.php/GNOME "GNOME") Help Browser [yelp](https://www.archlinux.org/packages/?name=yelp) is a more neat way but has some dependencies.

### Converting to browser-readable HTML

#### mdocml

Install [mdocml](https://aur.archlinux.org/packages/mdocml/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/mdocml)]</sup> from [AUR](/index.php/AUR "AUR"). To convert a page, for example `free(1)`:

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

First install [roffit](https://aur.archlinux.org/packages/roffit/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/roffit)]</sup> from [AUR](/index.php/AUR "AUR").

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
*   [_Debian GNU/Linux man pages_](http://manpages.debian.net/)
*   [_DragonFlyBSD manual pages_](http://leaf.dragonflybsd.org/cgi/web-man)
*   [_FreeBSD Hypertext Man Pages_](http://www.freebsd.org/cgi/man.cgi)
*   [_Linux and Solaris 10 Man Pages_](http://www.manpages.spotlynx.com/)
*   [_Linux/FreeBSD Man Pages_](http://manpagehelp.net) with user comments
*   [_Linux man pages at die.net_](http://linux.die.net/man/)
*   [The Linux man-pages project at kernel.org](http://www.kernel.org/doc/man-pages/)
*   [_NetBSD manual pages_](http://netbsd.gw.com/cgi-bin/man-cgi)
*   [_Mac OS X Manual Pages_](http://developer.apple.com/documentation/Darwin/Reference/ManPages/index.html)
*   [_On-line UNIX manual pages_](http://unixhelp.ed.ac.uk/alphabetical/index.html)
*   [_OpenBSD manual pages_](http://www.openbsd.org/cgi-bin/man.cgi)
*   [_Plan 9 Manual — Volume 1_](http://man.cat-v.org/plan_9/)
*   [_Inferno Manual — Volume 1_](http://man.cat-v.org/inferno/)
*   [_Storage Foundation Man Pages_](http://sfdoccentral.symantec.com/sf/5.0MP3/linux/manpages/index.html)
*   [_The UNIX and Linux Forums Man Page Repository_](http://www.unix.com/man-page/OpenSolaris/1/man/)
*   [_Ubuntu Manpage Repository_](http://manpages.ubuntu.com/)

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

Retrieved from "[https://wiki.archlinux.org/index.php?title=Man_page&oldid=407234](https://wiki.archlinux.org/index.php?title=Man_page&oldid=407234)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [System administration](/index.php/Category:System_administration "Category:System administration")

Hidden categories:

*   [Pages or sections flagged with Template:Accuracy](/index.php/Category:Pages_or_sections_flagged_with_Template:Accuracy "Category:Pages or sections flagged with Template:Accuracy")
*   [Pages with dead links](/index.php/Category:Pages_with_dead_links "Category:Pages with dead links")
*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")